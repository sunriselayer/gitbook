# Environment

これは Sunrise ソフトウェアを実行するための開発環境です。この環境は、開発、バイナリのビルド、およびノードの実行に使用できます。

## Install Dependencies（依存関係のインストール）

### Ubuntu

```bash
sudo apt update
sudo apt install -y tar wget aria2 clang pkg-config libssl-dev jq build-essential git make ncdu
```

### Install Golang

Install Golang

```bash
wget https://go.dev/dl/go1.22.2.linux-amd64.tar.gz
sudo rm -rf /urise/local/go && sudo tar -C /urise/local -xzf go1.22.2.linux-amd64.tar.gz
rm go1.22.2.linux-amd64.tar.gz
echo "export PATH=$PATH:/urise/local/go/bin:$HOME/go/bin" >> $HOME/.bashrc
source $HOME/.bashrc
```

Check Go version

```bash
go version
```
