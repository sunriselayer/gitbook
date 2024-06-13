# Blob

The module `x/blob` is the Celestia-compatible module of Sunrise.

This module allows L2 operators to post the data to the Sunrise network. The data will be stored in the Sunrise network until the L2 transactions are finalized in the L1 blockchain.

## OFf Chain Blob Data (Data Availability v2)

After successfully launching the Sunrise v1 as a specialized Data Availability Layer for Proof of Liquidity,
we will introduce an upgrade for Blob features in Sunrise v2, to realize the usecases of Data Availability for fully on-chain AI, gaming, social and so on. Gluon will be the first place to realize the full on chain AI with Sunrise DA.

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
When the sizes of `BlobTx`s get larger, the throughput of the network will be limited by the txs transfer in the mempool. This will be an obstacle to apply the Data Availability technology for fully on-chain AI, gaming, social and so on.

To mitigate this bottleneck, we will do these things:

1. Off chain execution of erasure encoding to generate the erasure-coded BLOB data
1. Using off chain distributed file transfer system / storage like IPFS, Arweave, etc.

In this new design, `MsgPayForBlob` will contain the URIs of erasure-coded data shares.
The value is assumed to be the URI of the IPFS `"ipfs://[ipfs-cid]"` or Arweave `"ar://[hash]"`, and it will not be contained by `BlobTx` hence the blob data will not be on-chain of Sunrise.

In the consensus network, erasure encoding is not executed anymore. Only the merkle root of the list of erasure-coded data shares URI will be stored in the `Header`.

Ultimately it means that Data Availability Sampling will be done only for blob data off-chain, not the entire tx data in the block.

In this design, "long term Data Retrievability" is easy to control by using external storage / file system like IPFS and Arweave whereas the Data Retrievability is not guaranteed by other ecosystem which serve Data Availability. The reason why long term Data Retrievability is not guaranteed by other ecosystem which serve Data Availability is that it is not needed to preserve the tx data of Optimistic Rollups after the challenge period for fraud proofs, or ZK Rollups after the submission of validity proofs.

Furthermore, the decentralization of the network will get better. In the former design of executing 2-dimension Reed Solomon encoding by validators, the required resource of validators will be increased by the size of the tx data in the block and it will lead to the concentration of the network to small number of validators.
In the new design, the resource of running Prover Node is very light. The more Prover Node in the Network, the more off chain blob data can be attested for their Data Availability.

To prevent from data withholding attack, the Prover Nodes will submit the [verifiable Proof of Data Posession](https://hdl.handle.net/20.500.14094/90009512) of the share of erasure-coded BLOB data.

In conclusion, there are benefits:

- The throughput of the network will be increased due to the block size
- Easy to control the long term Data Retrievability
  - Applications for fully on-chain AI, gaming, social and so on can be realized
- The decentralization of the network will be improved

### Sequence Diagram

```mermaid
sequenceDiagram
    autonumber
    User ->> Prover Node: BLOB data and fee
    Prover Node --> Prover Node: Erasure encoding
    Prover Node ->> IPFS / Arweave: Erasure-coded data shares
    Prover Node ->> Other Prover Nodes: Erasure-coded data shares URIs
    Prover Node ->> Other Prover Nodes: KZG commitment
    IPFS / Arweave ->> Other Prover Nodes: Data Availability Sampling
    Other Prover Nodes --> Other Prover Nodes: Verify KZG commitment
    Prover Node ->> Validator Set: Erasure-coded data shares URIs
    Prover Node ->> Validator Set: KZG commitment
    Validator Set ->> Prover Node: Tx receipt
    Prover Node ->> Other Prover Nodes: Tx receipt
    Prover Node ->> User: Tx receipt
    Other Prover Nodes ->> Validator Set: Proof of Data Posession
    Validator Set ->> Other Prover Nodes: Reward
    Validator Set ->> Block Body: DA Attestations
    Validator Set ->> Block Header: Merkle root of DA Attestations
```

### References

- [Transparent Provable Data Possession Scheme for Cloud Storage](https://hdl.handle.net/20.500.14094/90009512)