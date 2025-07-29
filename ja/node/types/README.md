# Sunriseでノードを実行するための概要

Sunrise [ネットワーク](../networks/README.md)への参加方法は多岐にわたります。
Sunriseのノード運用者は、ネットワーク上でいくつかの選択肢を実行することができます。

## コンセンサス

- [バリデーターノード](./consensus/build-validator-node.md): このタイプのノードは、ブロックを生成し、投票することによってコンセンサスに参加します。
- [フルコンセンサスノード](./consensus/build-full-node.md): ブロックチェーンの履歴を同期するためのsunrise-appフルノード。

## データ可用性

- [OP Stack](https://docs.sunriselayer.io/run-a-sunrise-node/types/data-availability/optimism): OP Stackを使用してSunrise L2を作成するためのガイド。
- [Sunrise Alt DA](https://docs.sunriselayer.io/run-a-sunrise-node/types/data-availability/alt-da): L2とSunriseチェーンを接続するソフトウェアのドキュメント。OP Stackがサポートされています。

## 要件

| タイプ | CPU | アーキテクチャ | メモリ | ディスク | 帯域幅 |
| --- | --- | --- | --- | --- | --- |
| バリデーター | 6コア | x86_64 | 8 GB | 500 GB SSD | 1 Gbps |
| フルコンセンサス | 4コア | x86_64 | 8 GB | 250 GB SSD | 1 Gbps |

各チュートリアルガイドを参照することで、それぞれの異なるノードの設定方法について詳しく学ぶことができます。