# Sunrise Validator Node

Validator nodes allow you to participate in consensus in the Sunrise network.

## Hardware requirements

The following hardware minimum requirements are recommended for running the validator node:

- Memory: 8 GB RAM (minimum)
- CPU: 6 cores
- Disk: 500 GB SSD Storage
- Bandwidth: 1 Gbps for Download/1 Gbps for Upload

## Run the Node

First, follow the instructions on [setting up a full consensus node](./full-consensus-node.md).

```bash
MONIKER="your_moniker"
VALIDATOR_WALLET="validator"

sunrised tx staking create-validator [path/to/validator.json] \
    --chain-id=$CHAIN_ID \
    --from=$VALIDATOR_WALLET \
    --keyring-backend=test \
    --fees=21000usr \
    --gas=220000
```

```json
{
        "pubkey": {"@type":"/cosmos.crypto.ed25519.PubKey","key":"oWg2ISpLF405Jcm2vXV+2v4fnjodh6aafuIdeoW+rUw="},
        "amount": "1000000usr",
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

Next, edit `~/.sunrise/config/config.toml`

## Backup

There are certain files that you need to backup to be able to restore your validator if, for some reason, it is damaged or lost in some way. Please make a secure backup of the following files located in `~/.sunrise/config/`:

- `priv_validator_key.json`
- `node_key.json`

It is recommended that you encrypt the backup of these files.

## Additional incentives for validators

The core team will delegate SR to validators who serve the following services:

- IBC relayer
  - `100000000microSR` delegation per channel
- Node snapshot
  - `10000000000microSR` delegation
- REST API endpoints
  - `10000000000microSR` delegation
