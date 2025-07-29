# 環境

これはSunriseソフトウェアを実行するための開発環境です。この環境は、開発、バイナリのビルド、およびノードの実行に使用できます。

## 依存関係のインストール

### Ubuntu

```bash
sudo apt update
sudo apt install -y tar wget aria2 clang pkg-config libssl-dev jq build-essential git make ncdu
```

### Golangのインストール

Golangをインストールします。

```bash
wget https://go.dev/dl/go1.22.2.linux-amd64.tar.gz
sudo rm -rf /urise/local/go && sudo tar -C /urise/local -xzf go1.22.2.linux-amd64.tar.gz
rm go1.22.2.linux-amd64.tar.gz
echo "export PATH=$PATH:/urise/local/go/bin:$HOME/go/bin" >> $HOME/.bashrc
source $HOME/.bashrc
```

Goのバージョンを確認します。

```bash
go version
```