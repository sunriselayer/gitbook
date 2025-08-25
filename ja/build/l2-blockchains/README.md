# L2ブロックチェーン

## Sunriseドキュメント

* [Rollkit](rollkit/)
  * [Sunriseデータ](rollkit/sunrise-data.md) - Sunrise DAリレーの設定と実行
  * [Rollkit L2チェーン](rollkit/rollkit.md) - RollkitベースのL2の構築とデプロイ
* [Optimism OP Stack](optimism/)
  * [Sunriseデータ](optimism/sunrise-data.md) - OP Stack用のSunrise DAの設定
  * [OP Stack L2チェーン](optimism/op-stack.md) - Sunriseを使用したOP Stack L2のデプロイ

## L2の作成方法

外部RPCに依存せず、フルコンセンサスノードをローカルで実行することをお勧めします。これにより、L2デプロイメントの信頼性と制御が向上します。

[Sunriseコンセンサスノードドキュメント](../../run-a-sunrise-node/types/consensus/)

### Rollkit

`sunrise-data`と`rollkit`を実行する必要があります。この統合により、以下が提供されます。

* Sunriseを介したネイティブなデータ可用性
* ソブリンロールアップ機能
* カスタマイズ可能な実行環境
* シンプルな設定とデプロイ

### OP Stack

`sunrise-data`、`optimism`、`op-geth`を実行する必要があります。主なポイントは次のとおりです。

* ローカルEVM L1チェーンは、OP Stackの要件を満たすためにのみ使用されます
* 実際のデータ（メタデータ）はSunriseに保存されます
* ローカルL1チェーンにはGanache、Hardhat、Anvilなどを使用します
* Sunriseが実際のデータ可用性を処理します

## 要件

| タイプ | CPU | アーキテクチャ | メモリ | ディスク | 帯域幅 | 目的 |
| --- | --- | --- | --- | --- | --- | --- |
| Rollkit + Sunriseデータ | 4コア | x86\_64 | 16 GB | 1 TB SSD | 1 Gbps | 開発とテスト |
| OP Stack + Sunriseデータ | 6コア | x86\_64 | 32 GB | 1 TB SSD | 1 Gbps | 本番デプロイメント |

追加の考慮事項：

* 本番環境では、SSDはエンタープライズグレードである必要があります
* 帯域幅の要件はトランザクション量に応じて増加します
* メモリ要件は状態サイズに応じてスケールします

## 公式ドキュメント

* [Rollkit](https://rollkit.dev/learn/intro)
  * [BeaconKit（オプション）](https://rollkit.dev/tutorials/execution/beaconkit): BeaconKitとRollkitを組み合わせることで、EVM互換のL2ブロックチェーンを開発できます。
  * Sunrise DAの利点を維持しながら、完全なEVM互換性を提供します
* [OP Stack](https://docs.optimism.io/stack/getting-started)
  * OP Stackデプロイメントのための包括的なドキュメント
  * さまざまなコンポーネントの統合ガイド

## 統合アーキテクチャ

```
┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐
│                 │     │                 │     │                 │
│  L2ブロックチェーン  │────▶│  Sunrise DA     │────▶│  バリデーター      │
│                 │     │  レイヤー          │     │  ネットワーク        │
└─────────────────┘     └─────────────────┘     └─────────────────┘
        │                       │                       ▲
        │                       │                       │
        ▼                       ▼                       │
┌─────────────────┐     ┌─────────────────┐             │
│                 │     │                 │             │
│  ユーザー           │     │  DA証明       │─────────────┘
│  アプリケーション   │     │  検証   │
└─────────────────┘     └─────────────────┘
```

## 一般的な統合手順

1. **Sunrise DAノードの設定**
   * Sunriseノードをデプロイするか、テストネットに接続します
   * ネットワークパラメータを設定します
   * 必要に応じてバリデーターを設定します
   * ノードの同期を確認します
2. **L2フレームワークの設定**
   * 必要な依存関係をインストールします
   * 設定ファイルを設定します
   * Sunrise DAレイヤーに接続します
   * ネットワークパラメータを設定します
3. **DA統合の実装**
   * BLOB送信を設定します
   * 証明検証を設定します
   * 手数料処理を実装します
   * 監視を設定します
4. **テストとデプロイ**
   * テストネットでテストします
   * DA証明を検証します
   * 本番環境にデプロイします
   * パフォーマンスを監視します

## 設定例

### Rollkit設定

```yaml
[da]
rpc_address = "http://localhost:26657"
fee_denom   = "uusdrise"
gas_price   = "0.025"

[rollup]
chain_id = "my-rollup-1"
```

### OP Stack設定

```bash
# 環境変数
DA_SERVER=http://localhost:8547
BLOB_RPC=http://localhost:26657
```

## ベストプラクティス

1. **セキュリティ**
   * 常にDA証明を検証します
   * 安全なRPCエンドポイントを使用します
   * 適切なエラー処理を実装します
   * 定期的なセキュリティ監査
2. **パフォーマンス**
   * BLOBサイズを最適化します
   * 適切なキャッシングを実装します
   * ガス代を監視します
   * 定期的なパフォーマンステスト
3. **信頼性**
   * 再試行メカニズムを実装します
   * DA証明のステータスを監視します
   * 適切なロギングを設定します
   * 定期的なバックアップ

## トラブルシューティング

| 問題 | 解決策 | 防止策 |
| --- | --- | --- |
| DA証明が検証されない | RPC接続と証明の形式を確認してください | 定期的な接続テスト |
| ガス代が高い | BLOBのサイズと頻度を最適化してください | ガス設定の監視と調整 |
| 接続の問題 | ネットワーク設定とファイアウォールの設定を確認してください | 定期的なネットワーク監視 |

## 追加リソース

* [Rollkitドキュメント](rollkit/)
* [OP Stack統合](optimism/)
* [データ可用性の証明](../validators/data-availability-proof.md)
* [料金抽象化](https://github.com/SunriseLayer/gitbook/blob/main/learn/sunrise/fee-abstraction.md)
