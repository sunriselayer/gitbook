# ununifid

ununifidバイナリをインストールするための手順

## オペレーティングシステムの選択

ノードに使用するオペレーティングシステムは、完全に個人の好みです。ほとんどの最新のLinuxディストリビューションと最近のバージョンのmacOSでununifidデーモンをコンパイルできます。

> このチュートリアルでは、Ubuntu LTSリリースを使用していることを前提としています。
> 別のオペレーティングシステムを選択した場合は、オペレーティングシステムに合わせてコマンドを変更する必要があります。

## 要件

バリデータノードサーバー

- メモリ：8 GB以上
- ストレージ：SSD 160 GB以上
- 次のポート：`26656`は、ノード間のピアツーピア通信のために開いている必要があります。

Ubuntu LTSリリースを使用しているかのように例を記述します。

## 前提条件のインストール

```Bash
# ローカルパッケージリストを更新し、利用可能なアップグレードをインストールする
sudo apt update && sudo apt upgrade -y
# ツールチェーンをインストールし、正確な時刻同期を確保する
sudo apt install build-essential git jq -y
```

## Goのインストール

[こちら](https://go.dev/doc/install)の指示に従ってGoをインストールします。
Ubuntu LTSの場合は、おそらく次を使用できます。

```Bash
# Go v1.19をインストールしてください
# $HOMEディレクトリから
$ wget https://go.dev/dl/go1.19.linux-amd64.tar.gz
$ sudo rm -rf /usr/local/go
$ sudo tar -C /usr/local -xzf go1.19.linux-amd64.tar.gz
$ go version
go version go1.19 linux/amd64
```

標準的でない方法で設定したくない場合は、ユーザーの`home`（つまり~/）フォルダの`.bash_profile`にこれらを設定します。

```Bash
echo "export GOROOT=/usr/local/go" >> ~/.bash_profile
echo "export GOPATH=$HOME/go" >> ~/.bash_profile
echo "export GO111MODULE=on" >> ~/.bash_profile
echo "export PATH=$PATH:/usr/local/go/bin:$HOME/go/bin" >> ~/.bash_profile
```

`~/.bash_profile`を更新した後、それを読み込む必要があります。

```Bash
source ~/.bash_profile
```

## ソースからのUnUniFiのビルド

UnUniFiブロックチェーンリポジトリをクローンし、指定されたブランチをチェックアウトし、`make install`でビルドしてバイナリをビルドします。

```Bash
# $HOMEディレクトリから
git clone https://github.com/UnUniFi/chain chain_repo
cd chain_repo
git checkout v3.1.0
make install
```

インストールが成功したことを確認するには、次を実行します。

```Bash
ununifid version
```
