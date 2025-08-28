# Sunrise Mainnet

The main network of Sunrise. Use tokens with real value.

## Mainnet Details

[sunrise-1 Network Configuration](https://github.com/sunriselayer/network/tree/main/sunrise-1)

[genesis file](https://github.com/sunriselayer/network/blob/main/sunrise-1/genesis.json)

[Snapshot (Provided by Polkachu)](https://www.polkachu.com/tendermint_snapshots/sunrise)

| Detail | Value                                                                                                      |
| ------ | ---------------------------------------------------------------------------------------------------------- |
| RPC    | <https://a.consensus.sunrise-1.sunriselayer.io>, <https://b.consensus.sunrise-1.sunriselayer.io>           |
| REST   | <https://a.consensus.sunrise-1.sunriselayer.io:1318>, <https://b.consensus.sunrise-1.sunriselayer.io:1318> |

Explorer and APIs are also provided by third parties. For details, see [Chain Registry](https://github.com/cosmos/chain-registry/blob/master/sunrise/chain.json).

## Frontend

| Name                | URL                                 |
| ------------------- | ----------------------------------- |
| APP (Tx Portal)     | <https://app.sunriselayer.io>       |
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

| Name | Chain         | Original Denom                                                         | IBC denom                                                              | Decimals |
| ---- | ------------- | ---------------------------------------------------------------------- | ---------------------------------------------------------------------- | -------- |
| USDN | `noble-1`     | `uusdn`                                                                | `ibc/A7AD825A4B48DDA0138D118655E60100D22A4D690C45B95221520B58C9A64B63` | 6        |
| USDC | `noble-1`     | `uusdc`                                                                | `ibc/8E27BA2D5493AF5636760E354E46004562C46AB7EC0CC4C1CA14E9E20E2545B5` | 6        |
| USDY | `noble-1`     | `ausdy`                                                                | `ibc/AAF322A78A0E34B76CDA05BA9AE96DC1521F9E103EC576AB9931116B2AB8C26B` | 18       |
| ATOM | `cosmoshub-4` | `uatom`                                                                | `ibc/C4CFF46FD6DE35CA4CF4CE031E643C8FDC9BA4B99AE598E9B0ED98FE3A2319F9` | 6        |
| USDT | `cosmoshub-4` | `ibc/E7E51FFF94A8B55BE84CEB0345E5CAF0A5DAEB374C6806CE908098B8996C7782` | `ibc/D4FF12988C31AD8E3D2555621F95C7EB2B6FBAAD2F9487FB11A2A8BBB004B4B3` | 6        |
| WBTC | `cosmoshub-4` | `ibc/D742E8566B0B8CC8F569D950051C09CF57988A88F0E45574BFB3079D41DE6462` | `ibc/0E293A7622DC9A6439DB60E6D234B5AF446962E27CA3AB44D0590603DFF6968E` | 8        |
| WETH | `cosmoshub-4` | `ibc/C0B53D3D23827AE38058BED0BDCD554229278AF530A8D265FCF6DFF7C4B2ADFF` | `ibc/694A6B26A43A2FBECCFFEAC022DEACB39578E54207FDD32005CD976B57B98004` | 18       |

## Mint USDrise from USDN on Mainnet

The address of the contract to mint USDrise is `sunrise14hj2tavq8fpesdwxxcu44rty3hh90vhujrvcmstl4zr3txmfvw9s2v9j75`.
You can mint the same amount of USDrise using USDN.

```bash
sunrised tx wasm execute sunrise14hj2tavq8fpesdwxxcu44rty3hh90vhujrvcmstl4zr3txmfvw9s2v9j75 \
'{"mint":{"amount":"1000000","recipient":"[your-address]"}}' \
--amount 1000000ibc/A7AD825A4B48DDA0138D118655E60100D22A4D690C45B95221520B58C9A64B63 \
--from=[your-account] --chain-id=sunrise-1\
--gas-prices=0.025uusdrise --gas-adjustment=1.5 --gas=auto -y
```

## Redeem USDrise to USDN on Mainnet

The address of the contract to redeem USDrise to USDN is `sunrise14hj2tavq8fpesdwxxcu44rty3hh90vhujrvcmstl4zr3txmfvw9s2v9j75`.
You can redeem the same amount of USDN using USDrise.

```bash
sunrised tx wasm execute sunrise14hj2tavq8fpesdwxxcu44rty3hh90vhujrvcmstl4zr3txmfvw9s2v9j75 \
'{"burn":{"amount":"1000000"}}' \
--amount 1000000uusdrise \
--from=[your-account] --chain-id=sunrise-1 \
--gas-prices=0.025uusdrise --gas-adjustment=1.5 --gas=auto -y
```
