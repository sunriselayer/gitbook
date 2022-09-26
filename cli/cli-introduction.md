---
description: >-
  A general introduction UnUnifi cli along with a brief description of commands and
  flags
---

# Introduction

## Introduction

`ununifid` is a command line client for the UnUniFi network. UnUniFi users can use `ununifid` to send transactions to the UnUniFi network and query the blockchain data.

{% hint style="info" %}
See [here](../validators/ununifid-installation-and-setup.md) for instructions on installing `ununifid`.
{% endhint %}

### Working Directory <a href="#working-directory" id="working-directory"></a>

The default working directory for the `ununifid` is `$HOME/.ununifid`, which is mainly used to store configuration files and blockchain data.  
The UnUnifi `key` data is saved in the working directory of `ununifid`. You can also specify the `ununifid` working directory by using the `--home` flag when executing `ununifid`.

### Connecting to a Full-Node

By default, `ununifid` uses `tcp://localhost:26657` as the RPC address to connect to the UnUnifi network.  
This default configuration assumes that the machine executing `ununifid` is running as a full-node.

### Global Flags <a href="#global-flags" id="global-flags"></a>

All commands have the following global flags:

| Name, shorthand | type   | Required | Default Value    | Description                                                                   |
| --------------- | ------ | -------- | ---------------- | ----------------------------------------------------------------------------- |
| --chain-id      | string |          |                  | The network Chain ID                                                          |
| --help          | string |          |                  | Print help message                                                            |
| --home          | string |          | $HOME/.ununifi   | Directory for config and data                                                 |
| --log\_format   | string |          | plain            | The Logging format (json \| plain)                                            |
| --log\level     | string |          | info             | The logging level (trace \| debug \| info \| warn \| error \| fatal \| panic) |
| --trace         | string |          |                  | Print out full stack trace on errors                                          |

### Module Commands <a href="#module-commands" id="module-commands"></a>

| **Subcommand**                          | **Description**                                               |
| --------------------------------------- | ------------------------------------------------------------- |
| [nftmint](modules/nftmint.md)           | nftmint subcommands for the feature to mint NFTs on UnUniFi.  |
| [nftmarket](modules/nftmarket.md)       | stablecoins can be minted with NFT as collateral.             |

