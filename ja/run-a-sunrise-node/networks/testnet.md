# Sunriseテストネット

## Dawnテストネット

{% hint style="warning" %}
**重要**: これはテストネットです。このネットワーク上のトークンはテスト目的のみであり、現実世界での価値はありません。ネットワークの状態は、バグ修正やアップグレードのためにいつでもリセットされる可能性があり、その永続性は保証されません。
{% endhint %}

このネットワークは、メインネットのいくつかの機能をテストするために使用されます。

### Dawnテストネットの詳細

[dawn-1ネットワークの詳細](https://github.com/sunriselayer/network/tree/main/dawn-1)

| 詳細 | 値 |
| ------ | ----------------------------------------- |
| RPC | <https://sunrise-dawn-1.cauchye.com> |
| REST | <https://sunrise-dawn-1.cauchye.com:1318> |

### Dawnテストネットのフロントエンド

| 名前 | URL |
| -------------------- | ----------------------------------------- |
| Dawn APP（Txポータル） | <https://dawn-1.app.sunriselayer.io> |
| Risescan（エクスプローラー） | <https://dawn-1.risescan.sunriselayer.io> |

### Dawnテストネットのソフトウェア

私たちの提案とコミュニティを確認してください。設定については[dawn-1 Github](https://github.com/sunriselayer/network/tree/main/dawn-1)を参照してください。

[リリース済みバイナリ](https://github.com/sunriselayer/sunrise/releases)

### Dawnテストネットのフォーセット

RISEとUSDriseのフォーセットはDawnテストネットで利用可能です。
このフォーセットはDawn APP内で提供されています。

使用するには、イーサリアムメインネットに少なくとも0.01 ETHを持つウォレットで署名する必要があります。費用はかかりません。

### DawnテストネットでUSDNからUSDriseをミントする

USDriseをミントするためのコントラクトのアドレスは`sunrise1suhgf5svhu4usrurvxzlgn54ksxmn8gljarjtxqnapv8kjnp4nrs4ef8ka`です。
USDNを使用して同量のUSDriseをミントできます。

```bash
sunrised tx wasm execute sunrise1suhgf5svhu4usrurvxzlgn54ksxmn8gljarjtxqnapv8kjnp4nrs4ef8ka \
'{"mint":{"amount":"1000000","recipient":"[your-address]"}}' \
--amount 1000000ibc/A7AD825A4B48DDA0138D118655E60100D22A4D690C45B95221520B58C9A64B63 \
--from=[your-account] --gas-prices=0.025uusdrise --gas-adjustment=1.2 --gas=auto -y
```

### DawnテストネットのIBC設定

| Dstチェーン | Dstポート | Dstチャネル | Srcチェーン | Srcポート | Srcチャネル |
| ---------- | ---------- | ------------- | --------- | ---------- | ----------- |
| `grand-1` | `transfer` | `channel-554` | `dawn-1` | `transfer` | `channel-0` |
| `provider` | `transfer` | `channel-493` | `dawn-1` | `transfer` | `channel-1` |

`grand-1`は現在のNobleテストネット[Grand-1 Testnet](https://www.noble.xyz/dev-hub)です。
[Noble Testnet chain-registry](https://github.com/cosmos/chain-registry/tree/master/testnets/nobletestnet)

`provider`は現在のCosmosHubテストネット[Cosmos ICS Provider Testnet](https://hub.cosmos.network/main/hub-tutorials/join-testnet)です。
[provider chain-registry](https://github.com/cosmos/chain-registry/tree/master/testnets/cosmosicsprovidertestnet)

## DawnテストネットのIBC Denom

| 名前 | チェーン | オリジナルDenom | IBC denom |
| ---- | ---------- | -------------- | ---------------------------------------------------------------------- |
| USDN | `grand-1` | `uusdn` | `ibc/A7AD825A4B48DDA0138D118655E60100D22A4D690C45B95221520B58C9A64B63` |
| USDC | `grand-1` | `uusdc` | `ibc/8E27BA2D5493AF5636760E354E46004562C46AB7EC0CC4C1CA14E9E20E2545B5` |
| ATOM | `provider` | `uatom` | `ibc/C4CFF46FD6DE35CA4CF4CE031E643C8FDC9BA4B99AE598E9B0ED98FE3A2319F9` |

## 非推奨のテストネット

### DAテストネット

{% hint style="warning" %}
`sunrise-test-da-1`、`sunrise-test-da-2`、`sunrise-test-da-3`、`sunrise-test-da-4`、`sunrise-test-da-5`は非推奨です。代わりに`dawn-1`を使用してください。
{% endhint %}

このネットワークは、メインネットのデータ可用性機能をテストするために使用されます。

### インセンティブ付きテストネット0.2

{% hint style="warning" %}
**重要**: このテストネットは2025年5月21日0:00 UTCに終了しました。
現在、DA 3テストネットのみが稼働しています。
{% endhint %}

このネットワークは、メインネットでの操作をテストするために使用されます。通常、メインネットと同じ環境が提供されますが、トークンに価値はありません。

### インセンティブ付きテストネット0.2の詳細

[sunrise-test-0.2ネットワークの詳細](https://github.com/sunriselayer/network/tree/main/sunrise-test-0.2)

| 詳細 | 値 |
| ------ | ------------------------------------------------ |
| RPC | <https://a-node.sunrise-test-1.cauchye.net> |
| REST | <https://a-node.sunrise-test-1.cauchye.net:1318> |

場合によってはb-dも稼働しています。[RiseScan](https://testnet.risescan.sunriselayer.io/)で確認してください。

### インセンティブ付きテストネット0.2のソフトウェア

私たちの提案とコミュニティを確認してください。設定については[sunrise-test-0.2](https://github.com/sunriselayer/network/tree/main/sunrise-test-0.2)を参照してください。
現在、テストネットはブロックチェーンの互換性のためにv0.2.xバイナリを使用しています。

[リリース済みバイナリ](https://github.com/sunriselayer/sunrise/releases)
