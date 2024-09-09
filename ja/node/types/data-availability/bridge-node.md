# Sunrise Bridge Node

ブリッジノードは、ブロックチェーンのデータ可用性層とコンセンサス層を接続します。

## Hardware requirements（ハードウェア要件）

ブリッジノードを実行するために推奨される最小限のハードウェア要件は以下の通りです。

- Memory: 4 GB RAM (最小)
- CPU: 6 cores
- Disk: 10 TB SSD Storage
- Bandwidth: 1 Gbps for Download/1 Gbps for Upload

## Dependencies（依存関係）

このチュートリアルは Ubuntu 22.04（LTS）で実行されます。
[環境構築チュートリアル](../../resources/enviromant.md)に従ってください。

## Run the bridge node（ブリッジノードの実行）

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
sunrise bridge init --core.ip <URI> --p2p.network <NETWORK>
```

The `--core.ip` gRPC port defaults to 9090. You can add the port after the IP address or use the `--core.grpc.port` flag to specify another port.
Refer to [the Resource page](../../resources/README.md) for information on which ports are required to be open.

example:

`--core.ip` gRPC ポートのデフォルト番号は 9090 です。IP アドレスの後にポートを追加するか、`--core.grpc.port` フラグを使用して別のポートを指定することができます。どのポートを開放する必要があるかについての情報は、[リソースページ](https://docs.sunriselayer.io/run-a-sunrise-node/resources)を参照してください。

```bash
sunrise bridge init --core.ip sunrise-private-2.cauchye.net --p2p.network private
```

### Run the Node（ノードの実行）

バリデータノードの gRPC エンドポイント（通常は Port:9090）への接続を使用してブリッジノードを起動します。

```bash
sunrise bridge start --core.ip <URI> --p2p.network <NETWORK>
```

example:

```bash
sunrise bridge start --core.ip sunrise-private-2.cauchye.net --p2p.network private
```
