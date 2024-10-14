# Blob

The deprecated module `x/blob` is the Celestia-compatible module of Sunrise.

This module allows L2 operators to post the data to the Sunrise network. The data will be stored in the Sunrise network until the L2 transactions are finalized in the L1 blockchain.

## Off Chain Blob Data (Data Availability v2)

After successfully launching the Sunrise v1 as a specialized Data Availability Layer for Proof of Liquidity,
we will introduce an upgrade for Blob features in Sunrise v2, to realize the usecases of Data Availability for fully on-chain AI, gaming, social and so on. Gluon will be the first place to realize the full on chain AI with Sunrise DA.

See [Github](https://github.com/sunriselayer/sunrise/tree/main/x/da) for details.

In the Sunrise v1 architecture, `data_hash` is replaced with the merkle root of the erasure-coded data with 2-dimension Reed Solomon encoding. The data means the txs data in the block. Data Availability Sampling technology plays a role of mitigating the running costs of full nodes with big blocks by enabling the light nodes to verify the data availability without downloading the entire block data.

[`CometBFT types.proto`](https://github.com/cometbft/cometbft/blob/main/proto/cometbft/types/v1/types.proto)

```protobuf
// Header defines the structure of a block header.
message Header {
  // basic block info
  cometbft.version.v1.Consensus version  = 1 [(gogoproto.nullable) = false];
  string                        chain_id = 2 [(gogoproto.customname) = "ChainID"];
  int64                         height   = 3;
  google.protobuf.Timestamp     time     = 4 [(gogoproto.nullable) = false, (gogoproto.stdtime) = true];

  // prev block info
  BlockID last_block_id = 5 [(gogoproto.nullable) = false];

  // hashes of block data
  bytes last_commit_hash = 6;  // commit from validators from the last block
  bytes data_hash        = 7;  // transactions

  // hashes from the app output from the prev block
  bytes validators_hash      = 8;   // validators for the current block
  bytes next_validators_hash = 9;   // validators for the next block
  bytes consensus_hash       = 10;  // consensus params for current block
  bytes app_hash             = 11;  // state after txs from the previous block
  bytes last_results_hash    = 12;  // root hash of all results from the txs from the previous block

  // consensus info
  bytes evidence_hash    = 13;  // evidence included in the block
  bytes proposer_address = 14;  // original proposer of the block
}
```

In this design, trivially all full nodes have to transfer and download the txs data in the mempool.
When the sizes of `BlobTx`s get larger, the throughput of the network will be limited by the txs transfer in the mempool. This will be an obstacle to apply the Data Availability technology for the usage of large BLOB data on decentralized applications, for example, fully on-chain AI, gaming, social and so on.

To mitigate this bottleneck, we will do these things:

1. Off chain execution of erasure encoding to generate the erasure-coded BLOB data
1. Using off chain distributed file transfer system / storage like IPFS, Arweave, etc.

In this new design, `MsgPublishData` will have the URI of metadata that has URIs of erasure-coded data shares.
The value is assumed to be the URI of decentralized storage / file transfer system like IPFS `"ipfs://[ipfs-cid]"` or Arweave `"ar://[hash]"`, and it will not be contained by `BlobTx` hence the blob data will not be on-chain of Sunrise.

In the consensus network, erasure encoding is not executed anymore. Only the double hash of erasure coded shard data will be included in `MsgPublishData`.

```protobuf
message MsgPublishData {
  option (cosmos.msg.v1.signer) = "sender";
  string sender = 1;
  string metadata_uri = 2;
  repeated bytes shard_double_hashes = 3;
}

message Metadata {
  uint64 shard_size = 1;
  uint64 shard_count = 2;
  repeated string shard_uris = 3;
}
```

Data Availability will be attested through zero knowledge proof using `shard_double_hashed` by proving that the validators can know the hash of shard data without disclosing them.

Currently it is assumed to do this process in [Vote Extension of ABCI 2.0](https://docs.cosmos.network/main/build/abci/vote-extensions).

In this design, "long term Data Retrievability" is easy to control by using external storage / file system like IPFS and Arweave whereas the Data Retrievability is not guaranteed by other ecosystem which serve Data Availability. The reason why long term Data Retrievability is not guaranteed by other ecosystem which serve Data Availability is that it is not needed to preserve the tx data of Optimistic Rollups after the challenge period for fraud proofs, or ZK Rollups after the submission of validity proofs.

In conclusion, there are benefits:

- The throughput of the network will be increased due to the block size
- Easy to control the long term Data Retrievability
  - Applications for fully on-chain AI, gaming, social and so on can be realized
- The decentralization of the network will be improved

```mermaid
sequenceDiagram
    autonumber
    User ->> Publisher Node: BLOB data
    Publisher Node --> Publisher Node: Erasure coding
    Publisher Node ->> Decentralized Storage: Upload data shards
    Publisher Node ->> Sunrise: MsgPublishData
    Sunrise ->> Validator Set: Start Vote Extension
    Validator Set ->> Sunrise: Vote Data Availability
    Publisher Node ->> Sunrise: Fraud Challenge if it is needed
    Validator Set ->> Sunrise: Zero Knowledge Validity Proof if challenge is submitted
```

## Specification for Zero-Knowledge Proof

### Terms and Notation

- The hash function: $$H$$
- Set of validators: $$ V $$
- Set of data shards: $$ S_d $$
- Set of parity shards: $$ S_p $$
- Set of shards: $$ S $$

$$
  S = S_d \cup S_p
$$

### Overview

This system verifies the possession of data shard hash $$ H(s_i) $$ without exposing $$ H(s_i) $$

### Zero-Knowledge Proof System

The circuit is for one shard $$ s \in S $$.

#### Public Inputs

- $$ H\_{\text{public}}^2(s)$$

#### Private Inputs

- $$ H\_{\text{private}}(s) $$

#### Circuit Constraints

$$
  H_{\text{public}}^2(s) = H(H_{\text{private}}(s))
$$

## The condition of Data Availability

### Notations

- Replication Factor (Based only on data shards): $$ r $$
- Replication Factor (Based on including parity shards): $$ r_p $$

$$
  r_p = r \frac{|S_d|}{|S_d| + |S_p|}
$$

- The number of shards each validator is engaged in: $$ n $$

$$
  n = \text{ceil}\left( r_p \frac{|S_d| + |S_p|}{|V|} \right) = \text{ceil} \left( r\frac{|S_d|}{|V|} \right)
$$

### Requirements for each shard to prove Data Availability

- Set of valid proofs for a shard `s` from validators engaged in this shard: $$ Z_s $$

$$
  \frac{|Z_s|}{r_p} \ge \frac{2}{3}
$$

- Set of shards which satisfy this condition: $$ S^\text{available} $$

### Requirements for tally to prove Data Availability

$$
\begin{aligned}
  \frac{|S^\text{available}|}{|S|} &\ge \frac{|S_d|}{|S_d| + |S_p|} \\
\Rightarrow |S^\text{available}| &\ge |S_d|
\end{aligned}
$$

#### Example parameters

- 10 validators: $$ v*1 , ..., v*{10} $$
- 20 shards: $$ s*1, ..., s*{20} $$
  - 10 data shards
  - 10 parity shards
- $$ r = 6 $$
- $$ r_p = 6 \times \frac{10}{10 + 10} = 3 $$
- Each validator submits 6 shards proofs
  - $$ 3 \times \frac{20}{10} = 6 $$

#### Case A: valid shard `s_1`

- Validator $$ v_1 $$, $$ v_3 $$ and $$ v_9 $$ 's proof contain shard $$ s_1 $$ and other 5 shards
- Validator $$ v_3 $$ failed to contain the validity of shard $$ s_1 $$ in its proof
- However validator $$ v_1 $$ and $$ v_9 $$ succeeded to contain the validity of shard $$ s_1 $$ in its proof, then
  - $$ |Z\_{s_1}| = 2 $$
  - It satisfies $$ \frac{|Z\_{s_1}|}{r_p} \ge \frac{2}{3} $$

#### Case B: invalid shard `s_2`

- Validator $$ v*2 $$, $$ v_4 $$ and $$ v*{10} $$ 's proof contain shard $$ s_2 $$ and other 5 shards
- Validator $$ v_2 $$ and $$ v_4 $$ failed to contain the validity of shard $$ s_2 $$ in its proof
- Only validator $$ v\_{10} $$ succeeded to contain the validity of shard $$ s_2 $$ in its proof, then
  - $$ |Z\_{s_2}| = 1 $$
  - It doesn't satisfy $$ \frac{|Z\_{s_2}|}{r_p} \ge \frac{2}{3} $$

#### Case X: shard s_1, s_3-s_11 are valid with the condition above

- $$ |S^\text{available}| = 10 $$
- $$ |S_d| = 10 $$
- It satisfies $$ |S^\text{available}| \ge |S_d| $$

#### Case Y: Only shard s_1, s_3 are valid with the condition above

- $$ |S^\text{available}| = 2 $$
- $$ |S_d| = 10 $$
- It doesn't satisfy $$ |S^\text{available}| \ge |S_d| $$

### Slashing condition for each validator

- Set of valid proofs from a validator `v` for shards engaging in: $$ Z_v $$

## Comparison Between On-chain DA attestation and Off-chain DA attestation

|                                          | On-chain DA attestation              | Off-chain DA attestation |
| ---------------------------------------- | ------------------------------------ | ------------------------ |
| Data Corruption Durability               | 〇                                   | 〇                       |
| Tx Mempool Scalability                   | ×                                    | 〇                       |
| Data Retrievability Control              | ×                                    | 〇                       |
| Validators Load Mitigation               | ×                                    | 〇                       |
| False-Positive DA Attestation Resistance | 〇                                   | 〇※                      |
| Examples                                 | Celestia, Avail, EigenDA, Sunrise V1 | Sunrise V2, Walrus, 0G   |

### Data Corruption Durability

In both on-chain and off-chain DA attestations, data corruption durability refers to the ability of the system to detect and prevent corruption of the data.

On-chain attestation, such as Celestia or Sunrise V1, ensures that data is durably available because it is stored directly on-chain, and any tampering or loss of data can be immediately detected by validators.

Off-chain attestation (e.g., Sunrise V2) relies on external systems (like IPFS or Arweave) but can still achieve similar durability by verifying the integrity of the data through erasure coding and zero-knowledge proofs.

### Tx Mempool Scalability

Transaction mempool scalability is a major limitation in on-chain DA systems. As the size of transactions (such as `BlobTxs`) grows, the transaction mempool, which temporarily holds pending transactions, can become overloaded, limiting throughput and scalability.

In off-chain DA systems, this limitation is mitigated by storing large amounts of data externally, with only the necessary hashes or metadata being stored on-chain. This allows for greater scalability and the ability to process larger volumes of data without congesting the mempool.

### Data Retrievability Control

In on-chain DA systems, data retrievability is often tied to the consensus mechanism, which means the data must remain available as long as it is needed for consensus (e.g., fraud proofs or validity proofs). However, long-term data retrievability is not always guaranteed once the consensus is finalized.

Off-chain DA systems, such as Sunrise V2, provide more flexible control over data retrievability because the data is stored in decentralized storage systems (like IPFS or Arweave). This allows for longer-term retention of data and better control over how long data remains accessible.

### Validators Load Mitigation

On-chain DA attestation places a heavier load on validators since they are responsible for verifying the data availability directly on-chain. As transaction sizes grow, the computational and storage demands on validators increase, potentially limiting decentralization.

In contrast, off-chain DA attestation significantly reduces the load on validators by outsourcing data storage and retrieval to external systems. Validators only need to verify the availability of data shards through erasure coding and zero-knowledge proofs, which lightens their processing and storage requirements.

### False-Positive DA Attestation Resistance

False-positive DA attestation refers to situations where a system incorrectly attests that data is available when, in reality, it is not.

On-chain DA attestation, used by systems like Celestia and Sunrise V1, has strong resistance to false positives since all the data is stored and verified directly on-chain, making it difficult to falsely claim that data is available when it is not.

In off-chain DA attestation (e.g., Sunrise V2), false-positive resistance is maintained through the use of zero-knowledge proofs and cryptographic commitments like erasure coding. By verifying the double-hashed values of shard data, validators can ensure that the data is indeed available without needing to store or directly access the entire data set. However, there may still be edge cases where off-chain storage solutions or network latency could introduce opportunities for false-positive attestations, though these are minimized by careful design and redundancy in the verification process.
