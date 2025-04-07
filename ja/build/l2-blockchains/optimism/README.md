# OP-Stack + Sunrise

SunriseのデータDA可用性レイヤーは、[OP Stack](https://github.com/ethereum-optimism/optimism)を使用して作成されたレイヤー2ブロックチェーンをサポートしています。

これは、OP Stackを使用して作成したL2チェーンを[Sunrise Data](https://github.com/sunriselayer/sunrise-data)を通じてSunriseチェーンに接続するためのガイドです。データ可用性レイヤーはSunrise v0.3.0以降でサポートされています。

## Sunrise Data

**Optimismを開始する前に、sunrise-dataをセットアップしてください。**
[Sunrise Dataドキュメント](./sunrise-data.md)

外部RPCに依存せず、完全なコンセンサスノードをローカルで実行することが推奨されます。
[Sunriseコンセンサスノードドキュメント](../../../node/types/consensus/README.md)

## OP Stack

[Alt-DAモード](https://docs.optimism.io/operators/chain-operators/features/alt-da-mode)でOP Stack L2チェーンを起動します。

最新のドキュメントに従ってください。要件を満たすために、ローカルのEVMチェーンが必要になる場合があります。

[OP Stack L2チェーンドキュメント](./op-stack.md)