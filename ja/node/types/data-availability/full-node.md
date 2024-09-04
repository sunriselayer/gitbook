# Sunrise Full storage Node

フルストレージノードは `sunrise-app`（したがってフルコンセンサスノードではありません）に接続しませんが、すべてのデータを保存します。

## Hardware requirements（ハードウェア要件）

フルストレージノードを実行するために推奨される最小限のハードウェア要件は以下の通りです。

- Memory: 4 GB RAM (最小)
- CPU: 4 cores
- Disk: 10 TB SSD Storage
- Bandwidth: 1 Gbps for Download/1 Gbps for Upload

## Dependencies（依存関係）

このチュートリアルは Ubuntu 22.04（LTS）で実行されます。[環境構築チュートリアル](https://github.com/SunriseLayer/gitbook/blob/main/node/resources/enviromant.md)に従ってください。

## Run the Full storage node（フルストレージノードの実行）

### Install（インストール）

```bash
git clone https://github.com/SunriseLayer/sunrise-da.git
cd sunrise-da
git checkout $TAG
make build
sudo make install
```

### Initialize（初期化）

```bash
sunrise full init --p2p.network <NETWORK>
```

example:

```bash
sunrise full init --p2p.network private
```

### Run the Node（ノードの実行）

フルストレージノードを、バリデータノードの gRPC エンドポイント（通常は Port:9090）への接続と共に起動します。

```bash
sunrise full start --core.ip <URI> --p2p.network <NETWORK>
```

example:

```bash
sunrise full start --core.ip sunrise-private-2.cauchye.net --p2p.network private
```
