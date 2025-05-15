# Sunrise Network

## Mainnet

The main network of Sunrise. Use tokens with real value.

### Mainnet Details

Coming soon

### Mainnet Software

Coming soon

## Testnet

{% hint style="warning" %}
**IMPORTANT**: Testnet is closed.
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

This network is used to test Data Availability functions on the mainnet.
Since our testnet does not support DA, please use it to test L2 chains, etc.

### DA Testnet Details

[sunrise-test-da-2 Network Details](https://github.com/sunriselayer/network/tree/main/sunrise-test-da-2)

| Detail | Value                                        |
| ------ | -------------------------------------------- |
| RPC    | <https://sunrise-test-da-2.cauchye.net>      |
| REST   | <https://sunrise-test-da-2.cauchye.net:1318> |

### DA Testnet Software

Please check our proposals and community. See [sunrise-test-da-2](https://github.com/sunriselayer/network/tree/main/sunrise-test-da-2) for setup.
Data Availability is supported in v0.3.0 and later.

[Released Binary](https://github.com/sunriselayer/sunrise/releases)

{% hint style="warning" %}
`sunrise-test-da-1` is deprecated. Please migrate to `sunrise-test-da-2`.
{% endhint %}

### DA Testnet Faucet

RISE faucet is available for testing DA testnet.

```bash
curl https://da2-faucet-requests-le6vcwy6pa-an.a.run.app/?address=[your-address]
```

### How to use sunrise-data on DA Testnet

[sunrise-data](https://github.com/sunriselayer/sunrise-data) provides validator assistance and functionality for L2 chain publishers.

See [Sunrise Data](../../build/l2-blockchains/rollkit/sunrise-data.md) and [Proof of Data Availability](../../build/validators/data-availability-proof.md) for details.

Use the same version of `sunrise-data` as the `sunrised` binary.

```bash
git clone https://github.com/sunriselayer/sunrise-data.git
cd sunrise-data
git checkout v0.4.2
make install
```

For validators, run the following command to register a proof deputy from your validator.

```bash
sunrised tx da register-proof-deputy [deputy-address] \
--from [your-validator] --chain-id sunrise-test-da-1 --fees 10000urise --gas 1000000 --yes
```
