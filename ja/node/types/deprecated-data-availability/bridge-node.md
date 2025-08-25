# Sunriseブリッジノード

ブリッジノードは、データ可用性レイヤーとコンセンサスレイヤーを接続します。

## ハードウェア要件

ブリッジノードを実行するために、以下の最低ハードウェア要件が推奨されます。

- メモリ：4 GB RAM（最小）
- CPU：6コア
- ディスク：10 TB SSDストレージ
- 帯域幅：ダウンロード1 Gbps / アップロード1 Gbps

## 依存関係

このチュートリアルはUbuntu 22.04（LTS）で実行されます。
[環境チュートリアル](../../resources/environment.md)に従ってください。

## ブリッジノードの実行

### インストール

```bash
git clone https://github.com/sunriselayer/sunrise-da.git
cd sunrise-da
git checkout $TAG
make build
sudo make install
```

### 初期化

```bash
sunrise bridge init --core.ip <URI> --p2p.network <NETWORK>
```

`--core.ip` gRPCポートはデフォルトで9090です。IPアドレスの後にポートを追加するか、`--core.grpc.port`フラグを使用して別のポートを指定できます。
開く必要のあるポートについては、[リソースページ](../../resources/README.md)を参照してください。

例：

```bash
sunrise bridge init --core.ip sunrise-private-2.cauchye.net --p2p.network private
```

### ノードの実行

バリデーターノードのgRPCエンドポイント（通常はポート：9090）に接続してブリッジノードを開始します。

```bash
sunrise bridge start --core.ip <URI> --p2p.network <NETWORK>
```

例：

```bash
sunrise bridge start --core.ip sunrise-private-2.cauchye.net --p2p.network private
```
