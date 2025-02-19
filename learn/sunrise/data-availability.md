# Data Availability

Sunrise v2 is designed for high-throughput data availability, offering enhanced scalability and flexibility for applications. To achieve this, Sunrise adopts off-chain BLOB data and executes Erasure Coding for each Blob data, not entire block data.

## Key Features of Sunrise v2

Several enhancements in Sunrise v2 increase throughput, decentralization, and long-term data retrievability:

- **Off-chain Erasure Encoding:** BLOB data is erasure-coded off-chain, minimizing the computational and storage load on validators.

- **Off-chain Storage Integration:** Utilizing decentralized storage solutions such as IPFS and Arweave, data shards are stored externally. MsgPublishData includes only a metadata URI pointing to these erasure-coded data shares, reducing the on-chain block size requirements for Blob transactions and enhancing scalability.

## Design patterns of other DA layers

### Data Availability Committee

Data Availability Committee (DAC) is the traditional method to construct alternative Data Availability layer with low costs.

However, in DAC, it is impossible for clients to verify whether Data Availability attested by the committee is true or false, without downloading entire BLOB data.

### Data Availability Sampling

In the Data Availability layers which adopts Data Availability Sampling (DAS), block data are processed for Erasure Coding. Then clients can verify the Data Availability only with downloading a part of block data, and can verify the inclusion of BLOB data in the block by using Merkle Tree structure.

In typical DAS setup, full nodes must transfer and download transaction data within the mempool.

As BLOB data sizes grow, the network’s throughput could be limited by these transaction transfers, creating challenges for applications handling large BLOB data.

### Sunrise's design

To address these problems in DAC and DAS, Sunrise v2 implements the following solutions:

1. Off-chain Erasure Encoding: Blob data is processed for Erasure Coding in off-chain program, to reduce validator load.
1. BLOB data sharding: Not the entire block data but each BLOB data are processed for Erasure Coding. Clients still can verify the Data Availability for each BLOB data only with repeating to download shards, without downloading entire data. Clients also can verify the inclusion of BLOB in the block by using Merkle Tree structure.
1. External Storage: Blob data is stored on decentralized storage platforms like IPFS and Arweave. Rather than containing blob data on-chain, MsgPublishData holds a metadata URI pointing to erasure-coded data shares.

```protobuf
message MsgPublishData {
  option (cosmos.msg.v1.signer) = "sender";
  string sender = 1 [(cosmos_proto.scalar) = "cosmos.AddressString"];
  string metadata_uri = 2;
  uint64 parity_shard_count = 3;
  repeated bytes shard_double_hashes = 4;
  string data_source_info = 5;
}
```

Data availability is attested with Optimistic way. If the fraud proof is submitted to the Sunrise network, validators will submit Zero-Knowledge Proofs (ZKP) using double-hashed shard data (`shard_double_hashes`), allowing validators to verify the presence of shard data without revealing it. This integration is done through [Vote Extension of ABCI 2.0](https://docs.cosmos.network/main/build/abci/vote-extensions).

### Flow of proof

Submitted data will have one of the following statuses

1. CHALLENGE_PERIOD
1. CHALLENGING
1. VERIFIED
1. REJECTED

- CHALLENGE_PERIOD
It will remain in this status for a certain period of time after it is submitted. It will change to `CHALLENGING` if it is submitted to shards with `MsgInvalidity` above the threshold. Otherwise, it becomes `VERIFIED`.
- CHALLENGING
The data may be invalid. Validators verify that the data is valid and submits proof. If the validated shard meets the criteria, it becomes `VERIFIED`; if not, it becomes `REJECTED`.
The method of talling is explained in [Specification for Zero-Knowledge Proof](#specification-for-zero-knowledge-proof).
- VERIFIED
The MetadataUri of the data is taken into the block and can be referenced externally.
- REJECTED
The data was determined to be invalid as a result of validators' validation. The data is not taken into the block.

### Benefits of Sunrise v2

- **Increased Network Throughput:** Larger block sizes are achievable by reducing on-chain storage needs.
- **Enhanced Data Retrievability:** Storing data off-chain allows for flexible, long-term data retention.
- **Improved Network Decentralization:** By reducing validator load, Sunrise supports a more decentralized network structure.

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

In both on-chain and off-chain DA attestations, _data corruption durability_ refers to the ability of the system to detect and prevent corruption of the data.

On-chain attestation, such as **Celestia or Sunrise V1**, ensures that data is durably available because it is stored directly on-chain, and any tampering or loss of data can be immediately detected by validators.

Off-chain attestation (e.g., **Sunrise V2**) relies on external systems (like **IPFS or Arweave**) but can still achieve similar durability by verifying the integrity of the data through **erasure coding** and **zero-knowledge proofs**.

### Tx Mempool Scalability

_Transaction mempool scalability_ is a major limitation in on-chain DA systems. As the size of BLOB data grows, the transaction mempool, which temporarily holds pending transactions, can become overloaded, limiting throughput and scalability.

In off-chain DA systems, this limitation is mitigated by storing large amounts of data externally, with only the necessary hashes or metadata being stored on-chain. This allows for **greater scalability** and the ability to process larger volumes of data without congesting the mempool.

### Data Retrievability Control

In on-chain DA systems, _data retrievability_ is often tied to the consensus mechanism, which means the data must remain available as long as it is needed for consensus (e.g., fraud proofs or validity proofs). However, long-term data retrievability is not always guaranteed once the consensus is finalized.

Off-chain DA systems, such as **Sunrise V2**, provide more flexible control over data retrievability because the data is stored in decentralized storage systems (like **IPFS or Arweave**). This allows for **longer-term retention of data** and better control over how long data remains accessible.

### Validators Load Mitigation

On-chain DA attestation places a _heavier load_ on validators since they are responsible for verifying the data availability directly on-chain. As transaction sizes grow, the computational and storage demands on validators increase, potentially limiting decentralization.

In contrast, off-chain DA attestation significantly reduces the load on validators by **outsourcing data storage** and retrieval to external systems. Validators only need to verify the availability of data shards through **erasure coding** and **zero-knowledge proofs**, which lightens their processing and storage requirements.

### False-Positive DA Attestation Resistance

_False-positive DA attestation_ refers to situations where a system incorrectly attests that data is available when, in reality, it is not.

On-chain DA attestation, used by systems **like Celestia and Sunrise V1**, has strong resistance to false positives since all the data is stored and verified directly on-chain, making it difficult to falsely claim that data is available when it is not.

In off-chain DA attestation (e.g., **Sunrise V2**), false-positive resistance is maintained through the use of **zero-knowledge proofs** and cryptographic commitments like **erasure coding**. By verifying the double-hashed values of shard data, validators can ensure that the data is indeed available without needing to store or directly access the entire data set.

However, there may still be edge cases where _off-chain storage solutions_ or _network latency_ could introduce opportunities for false-positive attestations, though these are minimized by careful design and redundancy in the verification process.
