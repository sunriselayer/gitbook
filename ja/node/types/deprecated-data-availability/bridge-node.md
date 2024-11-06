# Sunrise Bridge Node（ブリッジノード）

ブリッジノードは、ブロックチェーンのデータ可用性層とコンセンサス層を接続します。

## ハードウェア要件

ブリッジノードを実行するために推奨される最小限のハードウェア要件は以下の通りです。

- Memory: 4 GB RAM (最小)
- CPU: 6 cores
- Disk: 10 TB SSD Storage
- Bandwidth: 1 Gbps for Download/1 Gbps for Upload

## 依存関係

このチュートリアルは Ubuntu 22.04（LTS）で実行されます。
[環境構築チュートリアル](../../resources/enviromant.md)に従ってください。

## ブリッジノードの実行

### インストール

```bash
git clone https://github.com/SunriseLayer/sunrise-da.git
cd sunrise-da
git checkout $TAG
make build
sudo make install
```

### 初期化

```bash
sunrise bridge init --core.ip <URI> --p2p.network <NETWORK>
```

`--core.ip` gRPC ポートのデフォルトは 9090 です。IP アドレスの後にポートを追加するか、`--core.grpc.port`フラグを使用して別のポートを指定することができます。
必要なポートの開放については、[リソースページ](../../resources/README.md)を参照してください。

例:

`--core.ip` gRPC ポートのデフォルト番号は 9090 です。IP アドレスの後にポートを追加するか、`--core.grpc.port` フラグを使用して別のポートを指定することができます。どのポートを開放する必要があるかについての情報は、[リソースページ](https://docs.sunriselayer.io/run-a-sunrise-node/resources)を参照してください。

```bash
sunrise bridge init --core.ip sunrise-private-2.cauchye.net --p2p.network private
```

### ノードの実行

バリデータノードの gRPC エンドポイント（通常は Port:9090）への接続を使用してブリッジノードを起動します。

```bash
sunrise bridge start --core.ip <URI> --p2p.network <NETWORK>
```

例:

```bash
sunrise bridge start --core.ip sunrise-private-2.cauchye.net --p2p.network private
```
