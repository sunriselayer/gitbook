# Sunriseライトノード

ライトノードはデータの可用性を保証します。これはSunriseネットワークと対話する最も一般的な方法です。

## ハードウェア要件

ライトノードを実行するための最小ハードウェア要件は以下の通りです：

- メモリ：500 GB RAM（最小）
- CPU：2コア
- ディスク：50 GB SSDストレージ
- 帯域幅：ダウンロード56 Kbps / アップロード56 Kbps

## 依存関係

このチュートリアルはUbuntu 22.04（LTS）で行われます。
[環境チュートリアル](../../resources/enviromant.md)に従ってください。

## ライトノードの実行

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
sunrise light init --p2p.network <NETWORK>
```

例：

```bash
sunrise light init --p2p.network private
```

### ノードの実行

バリデータノードのgRPCエンドポイント（通常はポート9090）に接続してライトノードを起動します：

```bash
sunrise light start --core.ip <URI> --p2p.network <NETWORK>
```

例：

```bash
sunrise light start --core.ip sunrise-private-2.cauchye.net --p2p.network private
```