# Sunrise Testnet

## DA Testnet

{% hint style="warning" %}
**IMPORTANT**: DA Testnet is sometimes initialized to fix bugs or for upgrades that cannot be handled on-chain.
Please update your software according to the [documentation](https://github.com/sunriselayer/network/tree/main/sunrise-test-da-5). If you need more USDrise, please use the faucet again or contact our team.
{% endhint %}

This network is used to test Data Availability functions on the mainnet.

### DA Testnet Details

[sunrise-test-da-5 Network Details](https://github.com/sunriselayer/network/tree/main/sunrise-test-da-5)

| Detail | Value                                        |
| ------ | -------------------------------------------- |
| RPC    | <https://sunrise-test-da-5.cauchye.net>      |
| REST   | <https://sunrise-test-da-5.cauchye.net:1318> |

### Frontend

| Name                | URL                                           |
| ------------------- | --------------------------------------------- |
| APP (Tx Portal)     | <https://da-5-test.app.sunriselayer.io>       |
| Risescan (Explorer) | <https://da-5-test.risescan.sunriselayer.io/> |

### DA Testnet Software

Please check our proposals and community. See [sunrise-test-da-5](https://github.com/sunriselayer/network/tree/main/sunrise-test-da-5) for setup.

[Released Binary](https://github.com/sunriselayer/sunrise/releases)

{% hint style="warning" %}
`sunrise-test-da-1`, `sunrise-test-da-2`, `sunrise-test-da-3`, `sunrise-test-da-4` is deprecated. Please move to `sunrise-test-da-5`.
{% endhint %}

### DA Testnet Faucet

USDrise faucet is available for DA testnet.
DA 5 testnet and beyond will use USDrise as the fee token.

```bash
curl https://da5-faucet-requests-le6vcwy6pa-an.a.run.app/?address=[your-address]
```

### Create Validator with RISE

`x/shareclass` allows validators to create validators only with RISE.
This feature is not shown in the header because it is for validators and developers.

<https://da-test.app.sunriselayer.io/share-class>

The feature of staking RISE is also provided on this page.

### How to use sunrise-data on DA Testnet

[sunrise-data](https://github.com/sunriselayer/sunrise-data) provides validator assistance and functionality for L2 chain publishers.
It is required for the submission of a Validity Proof of DA by the validator and the publish of L2 chain data to DA.

See [Sunrise Data](../../build/l2-blockchains/rollkit/sunrise-data.md) and [Proof of Data Availability](../../build/validators/data-availability-proof.md) for details.

Use `sunrise-data` which supports `sunrised` binary.

```bash
git clone https://github.com/sunriselayer/sunrise-data.git
cd sunrise-data
git checkout v0.6.0
make install
```

#### Register Proof Deputy (for Validators)

Run the following command to register a proof deputy from your validator.

```bash
sunrised tx da register-proof-deputy [deputy-address] \
--from [your-validator] --chain-id sunrise-test-da-5 --gas-prices 0.0025uusdrise --gas auto -y
```

### Mint USDrise from USDN

The address of the contract to mint USDrise is `sunrise14hj2tavq8fpesdwxxcu44rty3hh90vhujrvcmstl4zr3txmfvw9s2v9j75`.
You can mint the same amount of USDrise using USDN.

```bash
sunrised tx wasm execute sunrise14hj2tavq8fpesdwxxcu44rty3hh90vhujrvcmstl4zr3txmfvw9s2v9j75 \
'{"mint":{"amount":"1000000","recipient":"[your-address]"}}' --amount 1000000uusdn \
--from [your-account] --gas-prices 0.0025uusdrise --gas auto -y
```

### IBC Config

| Dst Chain  | Dst Port   | Dst Channel   | Src Chain           | Src Port   | Src Channel |
| ---------- | ---------- | ------------- | ------------------- | ---------- | ----------- |
| `provider` | `transfer` | `channel-489` | `sunrise-test-da-5` | `transfer` | `channel-0` |
| `grand-1`  | `transfer` | `channel-532` | `sunrise-test-da-5` | `transfer` | `channel-1` |

`provider` is current CosmosHub testnet [Cosmos ICS Provider Testnet](https://hub.cosmos.network/main/hub-tutorials/join-testnet)
[provider chain-registry](https://github.com/cosmos/chain-registry/tree/master/testnets/cosmosicsprovidertestnet)

`grand-1` is current Noble testnet [Grand-1 Testnet](https://www.noble.xyz/dev-hub)
[Noble Testnet chain-registry](https://github.com/cosmos/chain-registry/tree/master/testnets/nobletestnet)

## Deprecated Testnets

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
