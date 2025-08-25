# Sunrise Rollkitの実行方法

例として、Rollkitを使用してL2チェーンを作成し、Sunriseのデータ可用性レイヤーで実行する方法を以下に示します。

## 依存関係

Ubuntu 22.04の依存関係と一般的なインストール手順。

## Sunriseデータの設定

Rollkitのサポートは、sunrise-dataに含まれるサーバーを介して提供されます。
DAサーバーの役割については、[Rollkitドキュメント](https://rollkit.dev/tutorials/da/overview)を参照してください。

設定方法は[Sunriseデータドキュメント](./sunrise-data.md)を参照してください。
デフォルトでは、Rollkitサポート用のGRPCサーバーはポート7980でリッスンします。

## Rollkitの実行

1. rollkitリポジトリをクローンします

   ```bash
   cd ~
   git clone https://github.com/rollkit/rollkit.git
   cd rollkit
   git checkout v0.14.1 # 最新のメジャーバージョン
   make install
   ```

2. rollkitチェーンを開始します
  `--rollkit.da_address`オプションを使用してDAサーバーに接続します。
  他のポート指定オプションは、sunrisedをローカルで実行する際の競合を避けるために使用されます。
  他のチェーン設定については、[Rollkitドキュメント](https://rollkit.dev/)を参照してください。

   ```bash
   rollkit start --rollkit.aggregator \
   --rollkit.sequencer_rollup_id sunrise \
   --rollkit.da_address grpc://localhost:7980 \
   --p2p.laddr tcp://0.0.0.0:25656 --rpc.laddr tcp://127.0.0.1:25657
   ```

3. 動作

## リンク

- [Rollkit](https://rollkit.dev/learn/intro)
