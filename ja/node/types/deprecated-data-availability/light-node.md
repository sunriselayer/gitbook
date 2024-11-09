# Sunrise Light Node（ライトノード）

ライトノードはブロックチェーンのデータ可用性を確保します。これは Sunrise ネットワークと通信する最も一般的な方法です。

## ハードウェア要件

以下は、ライトノードを実行するために推奨される最小限のハードウェア要件です。

- メモリ: 500 GB RAM（最小）
- CPU: 2 core
- ディスク: 50 GB SSD ストレージ
- Bandwidth: 56 Kbps for Download/56 Kbps for Upload

## 依存関係

このチュートリアルは Ubuntu 22.04（LTS）で実行されます。[環境構築チュートリアル](https://github.com/SunriseLayer/gitbook/blob/main/node/resources/enviromant.md)に従ってください。

## ライトノードの実行

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
sunrise light init --p2p.network <NETWORK>
```

例:

```bash
sunrise light init --p2p.network private
```

### ノードの実行

ライトノードを起動し、バリデータノードの gRPC エンドポイント（通常は port：9090）に接続します。

```bash
sunrise light start --core.ip <URI> --p2p.network <NETWORK>
```

例:

```bash
sunrise light start --core.ip sunrise-private-2.cauchye.net --p2p.network private
```
