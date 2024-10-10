# Sunrise でノードを実行するための概要

[Sunrise ネットワーク](https://docs.sunriselayer.io/run-a-sunrise-node/networks)への参加方法は多岐にわたります。Sunrise のノード運用者は、ネットワーク上でいくつかの選択肢を実行することができます。

## Consensus

- [Validator node](https://github.com/SunriseLayer/gitbook/blob/main/node/types/consensus/build-validator-node.md)（バリデーターノード）：このタイプのノードはブロック生成と投票によってコンセンサスに参加します。
- [Full consensus node](https://github.com/SunriseLayer/gitbook/blob/main/node/types/consensus/build-full-node.md)（フルコンセンサスノード）: ブロックチェーンの履歴を同期する Sunrise-app のフルノード。

## Data Availability

- [Bridge Node](https://docs.sunriselayer.io/run-a-sunrise-node/types/data-availability/bridge-node)（ブリッジノード）: データ可用性ネットワークとコンセンサスネットワーク間でブロックをブリッジするノード。
- [Full Storage Node](https://docs.sunriselayer.io/run-a-sunrise-node/types/data-availability/full-node)（フルストレージノード）: すべてのデータを保存するが、コンセンサスネットワークには接続しないノード。
- [Light Node](https://docs.sunriselayer.io/run-a-sunrise-node/types/data-availability/light-node)（ライトノード）: データ可用性ネットワーク上でデータ可用性サンプリングを行うライトクライアント。

## 要件

| Type           | CPU    | Mem    | Disk       | Bandwidth |
| -------------- | ------ | ------ | ---------- | --------- |
| Light          | 2 Core | 500 MB | 50 GB SSD  | 56 Kbps   |
| Full Storage   | 4 Core | 4 GB   | 10 TB SSD  | 1 Gbps    |
| Bridge         | 6 Core | 4 GB   | 10 TB SSD  | 1 Gbps    |
| -------------- | ------ | ----   | ---------- | --------- |
| Validator      | 6 Core | 8 GB   | 500 GB SSD | 1 Gbps    |
| Full Consensus | 4 Core | 8 GB   | 250 GB SSD | 1 Gbps    |

各チュートリアル ガイドを参照することで、さまざまなノードのセットアップ方法について詳しく学ぶことができます。
