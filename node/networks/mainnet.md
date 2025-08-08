# Sunrise Mainnet

The main network of Sunrise. Use tokens with real value.

{% hint style="warning" %}
**IMPORTANT**: This network is currently in the process of being launched.
{% endhint %}

## Mainnet Details

[sunrise-1 Network Details](https://github.com/sunriselayer/network/tree/main/sunrise-1)

| Detail | Value                                                                                                      |
| ------ | ---------------------------------------------------------------------------------------------------------- |
| RPC    | <https://a.consensus.sunrise-1.sunriselayer.io>, <https://b.consensus.sunrise-1.sunriselayer.io>           |
| REST   | <https://a.consensus.sunrise-1.sunriselayer.io:1318>, <https://b.consensus.sunrise-1.sunriselayer.io:1318> |

## Frontend

| Name                | URL                                 |
| ------------------- | ----------------------------------- |
| APP (Tx Portal)     | Coming soon                         |
| Risescan (Explorer) | <https://risescan.sunriselayer.io/> |

## Mainnet Software

Please check our proposals and community. See [sunrise-1](https://github.com/sunriselayer/network/tree/main/sunrise-1) for setup.
The genesis binary is `v1.0.0`.

[Released Binary](https://github.com/sunriselayer/sunrise/releases)

## IBC Config

| Dst Chain     | Dst Port   | Dst Channel  | Src Chain   | Src Port   | Src Channel |
| ------------- | ---------- | ------------ | ----------- | ---------- | ----------- |
| `noble-1`     | `transfer` | channel-168  | `sunrise-1` | `transfer` | channel-0   |
| `cosmoshub-4` | `transfer` | channel-1421 | `sunrise-1` | `transfer` | channel-1   |

## IBC Denom

| Name | Chain         | Original Denom | IBC denom                                                              |
| ---- | ------------- | -------------- | ---------------------------------------------------------------------- |
| USDN | `noble-1`     | `uusdn`        | `ibc/A7AD825A4B48DDA0138D118655E60100D22A4D690C45B95221520B58C9A64B63` |
| USDC | `noble-1`     | `uusdc`        | `ibc/8E27BA2D5493AF5636760E354E46004562C46AB7EC0CC4C1CA14E9E20E2545B5` |
| ATOM | `cosmoshub-4` | `uatom`        | `ibc/C4CFF46FD6DE35CA4CF4CE031E643C8FDC9BA4B99AE598E9B0ED98FE3A2319F9` |

## Mint USDrise from USDN on Mainnet

The address of the contract to mint USDrise is `sunrise14hj2tavq8fpesdwxxcu44rty3hh90vhujrvcmstl4zr3txmfvw9s2v9j75`.
You can mint the same amount of USDrise using USDN.

```bash
sunrised tx wasm execute sunrise14hj2tavq8fpesdwxxcu44rty3hh90vhujrvcmstl4zr3txmfvw9s2v9j75 \
'{"mint":{"amount":"1000000","recipient":"[your-address]"}}' \
--amount 1000000ibc/A7AD825A4B48DDA0138D118655E60100D22A4D690C45B95221520B58C9A64B63 \
--from=[your-account] --gas-prices=0.025uusdrise --gas-adjustment=1.2 --gas=auto -y
```
