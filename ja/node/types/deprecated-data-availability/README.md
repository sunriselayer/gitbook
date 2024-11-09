# Data Availability Nodes

## 概要

- [ブリッジノード](https://docs.sunriselayer.io/run-a-sunrise-node/types/deprecated-data-availability/bridge-node): このノードは、データ可用性ネットワークとコンセンサスネットワークの間でブロックの橋渡しを行います
- [フルストレージノード](https://docs.sunriselayer.io/run-a-sunrise-node/types/deprecated-data-availability/full-node): このノードはすべてのデータを保存しますが、コンセンサスネットワークには接続しません
- [ライトノード](https://docs.sunriselayer.io/run-a-sunrise-node/types/deprecated-data-availability/light-node): ライトクライアントは、データ可用性ネットワーク上でデータ可用性サンプリングを実施します

コンセンサスノードを実行する場合は、[コンセンサスノードのチュートリアル](https://docs.sunriselayer.io/run-a-sunrise-node/types/consensus)に従ってください。

{% hint style='working' %}
バリデータノードを実行する場合、ブリッジノードが必要です。[このセクション](../deprecated-data-availability/bridge-node.md)を参照してください。
{% endhint %}

### 要件

| Type         | CPU    | Mem    | Disk      | Bandwidth |
| ------------ | ------ | ------ | --------- | --------- |
| Bridge       | 6 Core | 4 GB   | 10 TB SSD | 1 Gbps    |
| Full Storage | 4 Core | 4 GB   | 10 TB SSD | 1 Gbps    |
| Light        | 2 Core | 500 MB | 50 GB SSD | 56 Kbps   |
