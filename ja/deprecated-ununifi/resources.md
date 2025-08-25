# リソース

## メインネット

フロントエンドアプリケーション：<https://ununifi.io>

- エクスプローラー
  <https://ununifi.io/explorer>
  UnUniFiのブロックチェーンエクスプローラー
- ポータル
  <https://ununifi.io/portal>
  UnUniFiのウォレット＆DeFiアプリケーション

### パブリックLCD

UnUniFi Rest API
OpenAPI仕様のダウンロード：[swagger.yaml](https://github.com/UnUniFi/chain/blob/main/docs/client/swagger.yaml)

Cosmos SDK Rest＆gRPCゲートウェイ：[v1.cosmos.network](https://v1.cosmos.network/rpc)

| エンドポイント | ネットワーク | チェーンID |
| ----------------------------- | --------------- | --------------- |
| **a.lcd.ununifi.cauchye.net** | UnUniFiメインネット | ununifi-beta-v1 |
| **b.lcd.ununifi.cauchye.net** | UnUniFiメインネット | ununifi-beta-v1 |

### 利用可能なポート

| ポート | 機能 |
| -------------------- | --------------------------------- |
| 9090 | gRPCサーバー |
| 1317（https：1318） | RESTサーバー |
| 26657（https：26658） | CometBFT RPCエンドポイント（websocket） |

## テストネット

現在、3つのパブリックテストネットチェーンがあります。

- テストネット
  メインネット開発用
  <https://test.ununifi.io/>
- ラボ
  次期リリースで計画されている機能を含む
  <https://lab-testnet.ununifi.io/>
- アルファ
  不安定で最新の機能を含む
  <https://alpha-test.ununifi.io/>

すべてのテストネットにはエクスプローラーとポータルがあります。

| エンドポイント | ネットワーク | チェーンID |
| ---------------------------------- | --------------- | ------------------ |
| **a.ununifi-test-v1.cauchye.net** | UnUniFiテストネット | ununifi-test-v1 |
| **b.ununifi-test-v1.cauchye.net** | UnUniFiテストネット | ununifi-test-v1 |
| **c.ununifi-test-v1.cauchye.net** | UnUniFiテストネット | ununifi-test-v1 |
| **d.ununifi-test-v1.cauchye.net** | UnUniFiテストネット | ununifi-test-v1 |
| **ununifi-beta-test.cauchye.net** | UnUniFiラボ | ununifi-beta |
| **ununifi-alpha-test.cauchye.net** | UnUniFiアルファ | ununifi-alpha-test |

### 利用可能なポート（テストネット）

| ポート | 機能 |
| -------------------- | --------------------------------- |
| 9090 | gRPCサーバー |
| 1317（https：1318） | RESTサーバー |
| 26657（https：26658） | CometBFT RPCエンドポイント（websocket） |
| 8000（https：8001） | BTC用フォーセット |
| 8002（https：8003） | GUU＆USDC用フォーセット |
