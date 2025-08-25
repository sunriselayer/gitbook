---
description: >-
  UnUniFi cliの一般的な紹介と、コマンドとフラグの簡単な説明
---

# ununifid

## はじめに

`ununifid`はUnUniFiネットワークのコマンドラインクライアントです。UnUniFiユーザーは`ununifid`を使用してUnUniFiネットワークにトランザクションを送信し、ブロックチェーンデータを照会できます。

{% hint style="info" %}
`ununifid`のインストール手順については、[こちら](../setup-ununifid.md)を参照してください。
{% endhint %}

### 作業ディレクトリ

`ununifid`のデフォルトの作業ディレクトリは`$HOME/.ununifid`で、主に設定ファイルとブロックチェーンデータの保存に使用されます。
UnUniFiの`key`データは`ununifid`の作業ディレクトリに保存されます。`ununifid`の実行時に`--home`フラグを使用して`ununifid`の作業ディレクトリを指定することもできます。

### フルノードへの接続

デフォルトでは、`ununifid`はUnUniFiネットワークに接続するためのRPCアドレスとして`tcp://localhost:26657`を使用します。
このデフォルト設定は、`ununifid`を実行しているマシンがフルノードとして実行されていることを前提としています。

`ununifid`の実行時に`--node`フラグを追加することで、RPCポートが公開されている任意のフルノードに接続するようにRPCアドレスを指定できます。

{% hint style="info" %}
_<https://a.lcd.ununifi.cauchye.net:443>_ が利用可能です。
{% endhint %}

### グローバルフラグ

すべてのコマンドには、次のグローバルフラグがあります。

| 名前、省略形 | 型 | 必須 | デフォルト値 | 説明 |
| --------------- | ------ | -------- | -------------- | ----------------------------------------------------------------------------- |
| --chain-id | string | | | ネットワークのチェーンID |
| --help | string | | | ヘルプメッセージを印刷する |
| --home | string | | $HOME/.ununifi | 設定とデータのディレクトリ |
| --log_format | string | | plain | ログ形式（json \| plain） |
| --log_level | string | | info | ログレベル（trace \| debug \| info \| warn \| error \| fatal \| panic） |
| --trace | string | | | エラー時に完全なスタックトレースを印刷する |

### モジュールコマンド

| **サブコマンド** | **説明** |
| ----------------------------------- | ------------------------------------------- |
| [derivatives](broken-reference) | 永久先物と永久オプション用 |
| [nftbackedloan](broken-reference) | NFT担保ローン用 |
| [nftfactory](broken-reference) | オリジナルNFTの作成用 |
| [wasm](modules/wasm.md) | CosmWasmスマートコントラクト用 |
| [yieldaggregator](broken-reference) | インターチェーンイールドアグリゲーター用 |
