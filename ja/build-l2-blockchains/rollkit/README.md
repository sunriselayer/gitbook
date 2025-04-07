# Rollkit + Sunrise

SunriseのデータDA可用性レイヤーは、[Rollkit](https://github.com/rollkit/rollkit)を使用して作成されたレイヤー2ブロックチェーンをサポートしています。

これは、Rollkitを使用して作成したL2チェーンを[Sunrise Data](https://github.com/sunriselayer/sunrise-data)を通じてSunriseチェーンに接続するためのガイドです。データ可用性レイヤーはSunrise v0.3.1-rc1以降でサポートされています。

## Sunrise Data

**Optimismを開始する前に、sunrise-dataをセットアップしてください。**
[Sunrise Dataドキュメント](./sunrise-data.md)

外部RPCに依存せず、完全なコンセンサスノードをローカルで実行することが推奨されます。
[Sunriseコンセンサスノードドキュメント](../../../node/types/consensus/README.md)

## Rollkit

RollkitのL2チェーンを起動します。

[Rollkit L2チェーンドキュメント](./rollkit.md)