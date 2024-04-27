# Modular

## Monolithic vs Modular

There are four layers in a blockchain:

* Execution layer
* Settlement layer
* Consensus layer
* Data Availability layer

"Modular blockchain" is a paradigm that combines these separated layers, and allows us to build a scalable blockchain.

## Data Availability layer

In short, the Data Availability (DA) layer plays a role of storing transaction data of Layer 2 blockchains until the L2 transactions are finalized in the L1 blockchain.

## Combinations of layers

### Conventional rollup

Example of Optimism:

|                         |          |
| ----------------------- | -------- |
| Execution layer         | Optimism |
| Settlement layer        | Ethereum |
| Consensus layer         | Ethereum |
| Data Availability layer | Ethereum |

### Smart contract rollup with altDA

Example of Eclipse:

|                         |          |
| ----------------------- | -------- |
| Execution layer         | Eclipse  |
| Settlement layer        | Ethereum |
| Consensus layer         | Ethereum |
| Data Availability layer | Celestia |

### Sovereign rollup

Example of Gluon:

|                         |         |
| ----------------------- | ------- |
| Execution layer         | Gluon   |
| Settlement layer        | Gluon   |
| Consensus layer         | Sunrise |
| Data Availability layer | Sunrise |
