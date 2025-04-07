# Sunrise Rollkitの実行方法

例として、Rollkitを使用してL2チェーンを作成し、SunriseのデータDA可用性レイヤー上で実行する方法を紹介します。

## 依存関係

Ubuntu 22.04向けの依存関係と一般的なインストール手順です。

## Sunrise Dataのセットアップ

Rollkitサポートは、sunrise-dataに含まれるサーバーを通じて提供されています。
DAサーバーの役割については[Rollkitドキュメント](https://rollkit.dev/tutorials/da/overview)を参照してください。

セットアップについては[Sunrise Dataドキュメント](./sunrise-data.md)を参照してください。
デフォルトでは、Rollkitサポート用のGRPCサーバーはポート7980でリッスンします。

## Rollkitの実行

1. Rollkitリポジトリのクローン

   ```bash
   cd ~
   git clone https://github.com/rollkit/rollkit.git
   cd rollkit
   git checkout v0.14.1 # 最新のメジャーバージョン
   make install
   ```

1. Rollkitチェーンの起動
  DAサーバーに接続するには`--rollkit.da_address`オプションを使用します。
  その他のポート指定オプションは、sunrisedをローカルで実行する際の競合を避けるために使用されます。
  その他のチェーン設定については[Rollkitドキュメント](https://rollkit.dev/)を参照してください。

   ```bash
   rollkit start --rollkit.aggregator \
   --rollkit.sequencer_rollup_id sunrise \
   --rollkit.da_address grpc://localhost:7980 \
   --p2p.laddr tcp://0.0.0.0:25656 --rpc.laddr tcp://127.0.0.1:25657
   ```

1. 動作確認

## リンク

- [Rollkit](https://rollkit.dev/learn/intro)