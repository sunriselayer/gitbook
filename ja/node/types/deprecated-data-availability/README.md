# データ可用性ノード

## 概要

- [ブリッジノード](../data-availability/bridge-node.md): このノードは、データ可用性ネットワークとコンセンサスネットワークの間でブロックを橋渡しします。
- [フルストレージノード](../data-availability/full-node.md): このノードはすべてのデータを保存しますが、コンセンサスには接続しません。
- [ライトノード](../data-availability/light-node.md): ライトクライアントは、データ可用性ネットワーク上でデータ可用性サンプリングを実施します。

コンセンサスノードを実行する場合は、[コンセンサスノードチュートリアル](../consensus/README.md)に従ってください。

{% hint style='working' %}
バリデータノードを実行する場合、ブリッジノードが必要です。[このセクション](../data-availability/bridge-node.md)を参照してください。
{% endhint %}

### 要件

| タイプ | CPU | メモリ | ディスク | 帯域幅 |
| --- | --- | --- | --- | --- |
| ブリッジ | 6コア | 4 GB | 10 TB SSD | 1 Gbps |
| フルストレージ | 4コア | 4 GB | 10 TB SSD | 1 Gbps |
| ライト | 2コア | 500 MB | 50 GB SSD | 56 Kbps |