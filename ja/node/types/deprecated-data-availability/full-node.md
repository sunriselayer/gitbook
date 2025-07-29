# Sunriseフルストレージノード

フルストレージノードはsunrise-appに接続しませんが（したがってフルコンセンサスノードではありません）、すべてのデータを保存します。

## ハードウェア要件

フルストレージノードを実行するための最小ハードウェア要件は以下の通りです：

- メモリ：4 GB RAM（最小）
- CPU：4コア
- ディスク：10 TB SSDストレージ
- 帯域幅：ダウンロード1 Gbps / アップロード1 Gbps

## 依存関係

このチュートリアルはUbuntu 22.04（LTS）で行われます。
[環境チュートリアル](../../resources/enviromant.md)に従ってください。

## フルストレージノードの実行

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
sunrise full init --p2p.network <NETWORK>
```

例：

```bash
sunrise full init --p2p.network private
```

### ノードの実行

バリデータノードのgRPCエンドポイント（通常はポート9090）に接続してフルストレージノードを起動します：

```bash
sunrise full start --core.ip <URI> --p2p.network <NETWORK>
```

例：

```bash
sunrise full start --core.ip sunrise-private-2.cauchye.net --p2p.network private
```