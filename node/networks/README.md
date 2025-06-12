# Sunrise Network

## Mainnet

The main network of Sunrise. Use tokens with real value.

### Mainnet Details

Coming soon

### Mainnet Software

Coming soon

## Testnet

{% hint style="warning" %}
**IMPORTANT**: Testnet is closed on May 21, 2025 at 0:00 UTC.
Currently only the DA 3 Testnet is running.
{% endhint %}

This network is used to test operations on the mainnet. Normally, the same environment as the mainnet is provided, but tokens have no value.

### Testnet Details

[sunrise-test-0.2 Network Details](https://github.com/sunriselayer/network/tree/main/sunrise-test-0.2)

| Detail | Value                                            |
| ------ | ------------------------------------------------ |
| RPC    | <https://a-node.sunrise-test-1.cauchye.net>      |
| REST   | <https://a-node.sunrise-test-1.cauchye.net:1318> |

In some cases b-d is also in operation; check with [RiseScan](https://testnet.risescan.sunriselayer.io/).

### Testnet Software

Please check our proposals and community. See [sunrise-test-0.2](https://github.com/sunriselayer/network/tree/main/sunrise-test-0.2) for setup.
Currently, Testnet uses v0.2.x binaries for blockchain compatibility.

[Released Binary](https://github.com/sunriselayer/sunrise/releases)

## DA Testnet

{% hint style="warning" %}
**IMPORTANT**: DA Testnet is sometimes initialized to fix bugs or for upgrades that cannot be handled on-chain.
Please update your software according to the [documentation](https://github.com/sunriselayer/network/tree/main/sunrise-test-da-4). If you need more RISE, please use the faucet again or contact our team.
{% endhint %}

This network is used to test Data Availability functions on the mainnet.
Since our testnet does not support DA, please use it to test L2 chains, etc.

Currently the latest is DA 3 Testnet.

### DA Testnet Details

[sunrise-test-da-4 Network Details](https://github.com/sunriselayer/network/tree/main/sunrise-test-da-4)

| Detail | Value                                        |
| ------ | -------------------------------------------- |
| RPC    | <https://sunrise-test-da-4.cauchye.net>      |
| REST   | <https://sunrise-test-da-4.cauchye.net:1318> |

### Frontend

| Name                | URL                                           |
| ------------------- | --------------------------------------------- |
| APP (Tx Portal)     | <https://da-test-4.app.sunriselayer.io>       |
| Risescan (Explorer) | <https://da-test-4.risescan.sunriselayer.io/> |

### DA Testnet Software

Please check our proposals and community. See [sunrise-test-da-4](https://github.com/sunriselayer/network/tree/main/sunrise-test-da-4) for setup.

[Released Binary](https://github.com/sunriselayer/sunrise/releases)

{% hint style="warning" %}
`sunrise-test-da-1`, `sunrise-test-da-2` and `sunrise-test-da-3` is deprecated. Please move to `sunrise-test-da-4`.
{% endhint %}

### DA Testnet Faucet

RISE faucet is available for testing DA testnet.
The binary version as of genesis is v0.6.x. For details, see [sunrise-test-da-4](https://github.com/sunriselayer/network/tree/main/sunrise-test-da-4).

```bash
curl https://da4-faucet-requests-le6vcwy6pa-an.a.run.app/?address=[your-address]
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
git checkout v0.5.0
make install
```

#### Register Proof Deputy (for Validators)

Run the following command to register a proof deputy from your validator.

```bash
sunrised tx da register-proof-deputy [deputy-address] \
--from [your-validator] --chain-id sunrise-test-da-1 --fees 10000urise --gas 1000000 --yes
```
