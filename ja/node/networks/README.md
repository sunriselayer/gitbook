# Sunriseネットワーク

## メインネット

Sunriseのメインネットワーク。実価値のあるトークンを使用します。

### メインネットの詳細

近日公開

### メインネットソフトウェア

近日公開

## テストネット

{% hint style="warning" %}
**重要**: テストネットは2025年5月21日0:00 UTCに終了しました。
現在、DA 3テストネットのみが稼働しています。
{% endhint %}

このネットワークは、メインネットでの操作をテストするために使用されます。通常、メインネットと同じ環境が提供されますが、トークンに価値はありません。

### テストネットの詳細

[sunrise-test-0.2ネットワーク詳細](https://github.com/sunriselayer/network/tree/main/sunrise-test-0.2)

| 詳細 | 値 |
| --- | --- |
| RPC | <https://a-node.sunrise-test-1.cauchye.net> |
| REST | <https://a-node.sunrise-test-1.cauchye.net:1318> |

b-dも稼働している場合があります。[RiseScan](https://testnet.risescan.sunriselayer.io/)で確認してください。

### テストネットソフトウェア

提案やコミュニティをご確認ください。セットアップについては[sunrise-test-0.2](https://github.com/sunriselayer/network/tree/main/sunrise-test-0.2)をご覧ください。
現在、テストネットはブロックチェーンの互換性のためにv0.2.xバイナリを使用しています。

[リリース済みバイナリ](https://github.com/sunriselayer/sunrise/releases)

## DAテストネット

{% hint style="warning" %}
**重要**: DAテストネットは、バグ修正やオンチェーンで処理できないアップグレードのために初期化されることがあります。
[ドキュメント](https://github.com/sunriselayer/network/tree/main/sunrise-test-da-5)に従ってソフトウェアを更新してください。さらにUSDriseが必要な場合は、再度フォーセットを使用するか、チームにお問い合わせください。
{% endhint %}

このネットワークは、メインネットでのデータ可用性機能をテストするために使用されます。

### DAテストネットの詳細

[sunrise-test-da-5ネットワーク詳細](https://github.com/sunriselayer/network/tree/main/sunrise-test-da-5)

| 詳細 | 値 |
| --- | --- |
| RPC | <https://sunrise-test-da-5.cauchye.net> |
| REST | <https://sunrise-test-da-5.cauchye.net:1318> |

### フロントエンド

| 名前 | URL |
| --- | --- |
| APP (Txポータル) | <https://da-5-test.app.sunriselayer.io> |
| Risescan (エクスプローラー) | <https://da-5-test.risescan.sunriselayer.io/> |

### DAテストネットソフトウェア

提案やコミュニティをご確認ください。セットアップについては[sunrise-test-da-5](https://github.com/sunriselayer/network/tree/main/sunrise-test-da-5)をご覧ください。

[リリース済みバイナリ](https://github.com/sunriselayer/sunrise/releases)

{% hint style="warning" %}
`sunrise-test-da-1`、`sunrise-test-da-2`、`sunrise-test-da-3`、`sunrise-test-da-4`は非推奨です。`sunrise-test-da-5`に移行してください。
{% endhint %}

### DAテストネットフォーセット

DAテストネットではUSDriseフォーセットが利用可能です。
DA 5テストネット以降では、手数料トークンとしてUSDriseが使用されます。

```bash
curl https://da5-faucet-requests-le6vcwy6pa-an.a.run.app/?address=[your-address]
```

### RISEでバリデーターを作成

`x/shareclass`により、バリデーターはRISEのみでバリデーターを作成できます。
この機能はバリデーターと開発者向けのため、ヘッダーには表示されません。

<https://da-test.app.sunriselayer.io/share-class>

このページでは、RISEをステーキングする機能も提供されています。

### DAテストネットでsunrise-dataを使用する方法

[sunrise-data](https://github.com/sunriselayer/sunrise-data)は、バリデーターの支援とL2チェーン発行者向けの機能を提供します。
バリデーターによるDAの有効性証明の提出や、L2チェーンデータのDAへの公開に必要です。

詳細は[Sunriseデータ](../../build/l2-blockchains/rollkit/sunrise-data.md)と[データ可用性の証明](../../build/validators/data-availability-proof.md)をご覧ください。

`sunrised`バイナリをサポートする`sunrise-data`を使用してください。

```bash
git clone https://github.com/sunriselayer/sunrise-data.git
cd sunrise-data
git checkout v0.6.0
make install
```

#### プルーフ代理の登録（バリデーター向け）

次のコマンドを実行して、バリデーターからプルーフ代理を登録します。

```bash
sunrised tx da register-proof-deputy [deputy-address] \
--from [your-validator] --chain-id sunrise-test-da-5 --fees 10000uusdrise --gas auto --yes
```

### USDNからUSDriseをミント

USDriseをミントするコントラクトのアドレスは`sunrise14hj2tavq8fpesdwxxcu44rty3hh90vhujrvcmstl4zr3txmfvw9s2v9j75`です。
USDNを使用して同額のUSDriseをミントできます。

```bash
sunrised tx wasm execute sunrise14hj2tavq8fpesdwxxcu44rty3hh90vhujrvcmstl4zr3txmfvw9s2v9j75 \
'{"mint":{"amount":"1000000","recipient":"[your-address]"}}' --amount 1000000uusdn \
--from [your-account] --fees 10000uusdrise --gas auto --yes
```

### IBC設定

| 宛先チェーン | 宛先ポート | 宛先チャネル | 送信元チェーン | 送信元ポート | 送信元チャネル |
| --- | --- | --- | --- | --- | --- |
| `provider` | `transfer` | `channel-489` | `sunrise-test-da-5` | `transfer` | `channel-0` |
| `grand-1` | `transfer` | `channel-532` | `sunrise-test-da-5` | `transfer` | `channel-1` |

`provider`は現在のCosmosHubテストネット[Cosmos ICS Provider Testnet](https://hub.cosmos.network/main/hub-tutorials/join-testnet)です。
[provider chain-registry](https://github.com/cosmos/chain-registry/tree/master/testnets/cosmosicsprovidertestnet)

`grand-1`は現在のNobleテストネット[Grand-1 Testnet](https://www.noble.xyz/dev-hub)です。
[Noble Testnet chain-registry](https://github.com/cosmos/chain-registry/tree/master/testnets/nobletestnet)