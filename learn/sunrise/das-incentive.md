# DAS Incentive

Sunrise is based on Celestia's Data Availability architecture, but we think that the incentive mechanism for the Data Availability layer is not enough in Celestia's architecture, and it depends on the voluntary contribution of many parts. So we introduce the DAS Incentive mechanism.

By introducing this mechanism, we can expect DAS light nodes to have enough bandwidth and it leads to the improvement of data throughput and shortening the time to finality.

## Design

The full storage nodes in DA network will pay the rewards to the light nodes that participated in the reconstruction of the block. The rewards will be in proportion to the staking amount of the address of the light node to prevent Sybil attack.

The full storage nodes also get rewarded by inflation rewards after the corresponding light nodes submit the proof of the receipt of the rewards to the light nodes, to the consensus network.

The reward for the full storage nodes will also be in proportion to the staking amount of the address of the full storage node to prevent Sybil attack and incentivize the full storage nodes to participate in the Data Availability Sampling actively without depending on voluntary contribution.
