# Consensus Nodes（コンセンサスノード）

## 概要

- [Validator node](https://github.com/SunriseLayer/gitbook/blob/main/node/types/consensus/build-validator-node.md)（バリデータノード）：このタイプのノードは、ブロックの生成と投票によってコンセンサスに参加します
- [Full consensus node](https://github.com/SunriseLayer/gitbook/blob/main/node/types/consensus/build-full-node.md)（フルコンセンサスノード）：ブロックチェーンの履歴を同期する `sunrise-app` のフルノード

### 要件

| Type           | CPU    | Mem  | Disk       | Bandwidth |
| -------------- | ------ | ---- | ---------- | --------- |
| Validator      | 6 Core | 8 GB | 500 GB SSD | 1 Gbps    |
| Full Consensus | 4 Core | 8 GB | 250 GB SSD | 1 Gbps    |
