# How to Become a Validator

This document explains the steps to become a validator on the Sunrise chain.

## Prerequisites

Before operating a validator, you must set up a [Full Consensus Node](../../run-a-sunrise-node/types/consensus/full-consensus-node.md) and be fully synchronized with the network.

## Data Availability Verification

{% hint style="warning" %}
Validators on the Sunrise network are required to verify data for the Data Availability (DA) layer. This is a crucial responsibility. Please see the [Proof of the Data Availability Layer](data-availability-proof.md) guide for instructions on how to set this up.
{% endhint %}

## Setup Cosmovisor

For mainnet, it is strongly recommended to use Cosmovisor to run your node. Cosmovisor allows you to perform chain upgrades smoothly with minimal downtime.

Follow the [Cosmovisor setup tutorial](../../run-a-sunrise-node/types/consensus/setup-cosmovisor.md) for details.

It is recommended to set the following environment variable to enable automatic upgrades:

```bash
export DAEMON_ALLOW_DOWNLOAD_BINARIES=true
```

## Binary and Genesis File

When setting up a validator, it is crucial to use the correct version of the binary and `genesis.json`.

* **Binary:** The latest binary can be downloaded from the [GitHub releases](https://github.com/sunriselayer/sunrise/releases/tag/v1.0.0).
* **Genesis File:** The `genesis.json` file is located in the [network repository](https://github.com/sunriselayer/network/tree/main/sunrise-1).

## Creating a Validator

There are two ways to create a validator: joining at genesis and joining after the chain has started.

### Join as a Genesis Validator (Gentx)

To join as a validator before the network starts (as a genesis validator), you need to generate and submit a `gentx` (genesis transaction).

For detailed instructions, please refer to the [README in the sunriselayer/network repository](https://github.com/sunriselayer/network/blob/main/sunrise-1/gentx/README.md).

### Join as a Validator After the Chain Has Started

If the chain is already running, you can create a validator with the following method.

#### `tx staking create-validator`

This is the standard Cosmos SDK method, which uses a `validator.json` file to create a validator. This method requires `vRISE` for self-delegation. This method requires `vRISE` for self-delegation.

1.  **Get the Validator's Public Key**

    Run the `sunrised tendermint show-validator` command to get the validator's public key (pubkey).

    ```bash
    sunrised tendermint show-validator
    ```
2.  **Create the `validator.json` file**

    Create a `validator.json` file with the following content. Set the `pubkey` with the value obtained above.

    ```json
    {
        "pubkey": {"@type":"/cosmos.crypto.ed25519.PubKey","key":"oWg2ISpLF405Jcm2vXV+2v4fnjodh6aafuIdeoW+rUw="},
        "amount": "1000000uvrise",
        "moniker": "myvalidator",
        "identity": "optional identity signature (ex. UPort or Keybase)",
        "website": "validator's (optional) website",
        "security": "validator's (optional) security contact email",
        "details": "validator's (optional) details",
        "commission-rate": "0.1",
        "commission-max-rate": "0.2",
        "commission-max-change-rate": "0.01",
        "min-self-delegation": "1"
    }
    ```

    * The `amount` is specified in `uvrise`.
    * The `min-self-delegation` is also the amount of `vRISE`.
3.  **Send the `create-validator` transaction**

    ```bash
    sunrised tx staking create-validator path/to/validator.json --from <keyname> --chain-id <chain-id> --gas="auto" --gas-prices=<gas-prices> -y
    ```

    **Usage:**

    ```bash
    sunrised tx staking create-validator [path/to/validator.json] [flags]
    ```

## Backup

Backing up key files is crucial for validator operations. Please back up the following files to a secure location:

* `~/.sunrise/config/priv_validator_key.json`
* `~/.sunrise/config/node_key.json`

It is strongly recommended to encrypt these backup files.
