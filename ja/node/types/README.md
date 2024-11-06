# Sunrise でノードを実行するための概要

[Sunrise ネットワーク](https://docs.sunriselayer.io/run-a-sunrise-node/networks)への参加方法は多岐にわたります。Sunrise のノード運用者は、ネットワーク上でいくつかの選択肢を実行することができます。

## Consensus

- [Validator node](https://github.com/SunriseLayer/gitbook/blob/main/node/types/consensus/build-validator-node.md)（バリデーターノード）：このタイプのノードはブロック生成と投票によってコンセンサスに参加します。
- [Full consensus node](https://github.com/SunriseLayer/gitbook/blob/main/node/types/consensus/build-full-node.md)（フルコンセンサスノード）: ブロックチェーンの履歴を同期する Sunrise-app のフルノード。

## Data Availability

- [OP Stack](https://docs.sunriselayer.io/run-a-sunrise-node/types/data-availability/optimism): OP Stack を使用した Sunrise L2 作成ガイド。
- [Sunrise Alt DA](https://docs.sunriselayer.io/run-a-sunrise-node/types/data-availability/alt-da): L2 と Sunrise チェーンを接続するソフトウェアのドキュメント。OP Stack がサポートされます。

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
