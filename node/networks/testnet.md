# Sunrise Testnets

## Dawn Testnet

{% hint style="warning" %}
**Important**: This is a testnet. Tokens on this network are for testing purposes only and have no real-world value. The network state may be reset at any time for bug fixes or upgrades, and its persistence is not guaranteed.
{% endhint %}

This network is used to test some functions on the mainnet.

### Dawn Testnet Details

[dawn-1 Network Details](https://github.com/sunriselayer/network/tree/main/dawn-1)

| Detail | Value                                     |
| ------ | ----------------------------------------- |
| RPC    | <https://sunrise-dawn-1.cauchye.com>      |
| REST   | <https://sunrise-dawn-1.cauchye.com:1318> |

### Dawn Testnet Frontend

| Name                 | URL                                       |
| -------------------- | ----------------------------------------- |
| Dawn APP (Tx Portal) | <https://dawn-1.app.sunriselayer.io>      |
| Risescan (Explorer)  | <https://dawn-1.risescan.sunriselayer.io> |

### Dawn Testnet Software

Please check our proposals and community. See [dawn-1 Github](https://github.com/sunriselayer/network/tree/main/dawn-1) for setup.

[Released Binary](https://github.com/sunriselayer/sunrise/releases)

### Dawn Testnet Faucet

RISE & USDrise faucet is available for Dawn testnet.
This faucet is provided within the Dawn APP.

To use it, it must be signed in a wallet that has at least 0.01 ETH on the Ethereum mainnet. No cost.

### Mint USDrise from USDN on Dawn Testnet

The address of the contract to mint USDrise is `sunrise1suhgf5svhu4usrurvxzlgn54ksxmn8gljarjtxqnapv8kjnp4nrs4ef8ka`.
You can mint the same amount of USDrise using USDN.

```bash
sunrised tx wasm execute sunrise1suhgf5svhu4usrurvxzlgn54ksxmn8gljarjtxqnapv8kjnp4nrs4ef8ka \
'{"mint":{"amount":"1000000","recipient":"[your-address]"}}' \
--amount 1000000ibc/A7AD825A4B48DDA0138D118655E60100D22A4D690C45B95221520B58C9A64B63 \
--from=[your-account] --gas-prices=0.025uusdrise --gas-adjustment=1.2 --gas=auto -y
```

### IBC Config on Dawn Testnet

| Dst Chain  | Dst Port   | Dst Channel   | Src Chain | Src Port   | Src Channel |
| ---------- | ---------- | ------------- | --------- | ---------- | ----------- |
| `grand-1`  | `transfer` | `channel-554` | `dawn-1`  | `transfer` | `channel-0` |
| `provider` | `transfer` | `channel-493` | `dawn-1`  | `transfer` | `channel-1` |

`grand-1` is current Noble testnet [Grand-1 Testnet](https://www.noble.xyz/dev-hub)
[Noble Testnet chain-registry](https://github.com/cosmos/chain-registry/tree/master/testnets/nobletestnet)

`provider` is current CosmosHub testnet [Cosmos ICS Provider Testnet](https://hub.cosmos.network/main/hub-tutorials/join-testnet)
[provider chain-registry](https://github.com/cosmos/chain-registry/tree/master/testnets/cosmosicsprovidertestnet)

## Deprecated Testnets

### DA Testnet

{% hint style="warning" %}
`sunrise-test-da-1`, `sunrise-test-da-2`, `sunrise-test-da-3`, `sunrise-test-da-4`, `sunrise-test-da-5` is deprecated. Please use `dawn-1` instead.
{% endhint %}

This network is used to test Data Availability functions on the mainnet.

### Incentivized Testnet 0.2

{% hint style="warning" %}
**IMPORTANT**: This testnet is closed on May 21, 2025 at 0:00 UTC.
Currently only the DA 3 Testnet is running.
{% endhint %}

This network is used to test operations on the mainnet. Normally, the same environment as the mainnet is provided, but tokens have no value.

### Incentivized Testnet 0.2 Details

[sunrise-test-0.2 Network Details](https://github.com/sunriselayer/network/tree/main/sunrise-test-0.2)

| Detail | Value                                            |
| ------ | ------------------------------------------------ |
| RPC    | <https://a-node.sunrise-test-1.cauchye.net>      |
| REST   | <https://a-node.sunrise-test-1.cauchye.net:1318> |

In some cases b-d is also in operation; check with [RiseScan](https://testnet.risescan.sunriselayer.io/).

### Incentivized Testnet 0.2 Software

Please check our proposals and community. See [sunrise-test-0.2](https://github.com/sunriselayer/network/tree/main/sunrise-test-0.2) for setup.
Currently, Testnet uses v0.2.x binaries for blockchain compatibility.

[Released Binary](https://github.com/sunriselayer/sunrise/releases)
