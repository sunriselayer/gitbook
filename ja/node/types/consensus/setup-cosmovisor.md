# Setup Cosmovisor

**For mainnet, it's recommended to use Cosmovisor to run your node.**

Setting up Cosmovisor is relatively straightforward. However, it does expect certain environment variables and folder structure to be set.\
Cosmovisor allows you to download binaries ahead of time for chain upgrades, meaning that you can do zero (or close to zero) downtime chain upgrades. It's also useful if your local timezone means that a chain upgrade will fall at a bad time.\
Rather than having to do stressful ops tasks late at night, it's always better if you can automate them away, and that's what Cosmovisor tries to do.

メインネットでは、Cosmovisor を使用してノードを実行することをお勧めします。
Cosmovisor のセットアップは比較的簡単です。ただし、特定の環境変数とフォルダ構造を設定する必要があります。Cosmovisor を使用すると、チェーンのアップグレードに備えて事前にバイナリをダウンロードできるため、ダウンタイムがゼロ（またはほぼゼロ）のチェーンアップグレードが可能になります。また、お住まいのタイムゾーンの関係でチェーンのアップグレードが不都合な時間に行われる場合にも便利です。深夜にストレスの多い運用タスクを行うよりも、可能な限り自動化する方が常に良いでしょう。それが Cosmovisor の目指すところです。

## Install（インストール）

まず、cosmovisor を入手します（推奨方法）。

```Bash
# to target a specific version:
go install github.com/cosmos/cosmos-sdk/cosmovisor/cmd/cosmovisor@v1.0.0
```

### Add environment variables to your shell（シェルに環境変数を追加する）

各ノードと各ネットワークに適した値を設定するために、いくつかの環境変数を設定する必要があります。

```Bash
echo "export CHAIN_REPO=https://github.com/sunrise-layer/sunrise-app" >> ~/.bash_profile
echo "export CHAIN_REPO_BRANCHE=main" >> ~/.bash_profile
echo "export TARGET=sunrised" >> ~/.bash_profile
echo "export TARGET_HOME=.sunrise" >> ~/.bash_profile
# This value will be different for each node.
echo "export MONIKER=<your-moniker>" >> ~/.bash_profile
echo "export CHAIN_ID=sunrise-v1" >> ~/.bash_profile
# This value is example of mainnet.
echo "export GENESIS_FILE_URL=https://raw.githubusercontent.com/sunrise-layer/network/main/launch/sunrise-1/genesis.json" >> ~/.bash_profile
echo "export SETUP_NODE_CONFIG_ENV=TRUE" >> ~/.bash_profile
echo "export SETUP_NODE_ENV=TRUE" >> ~/.bash_profile
echo "export SETUP_NODE_MASTER=TRUE" >> ~/.bash_profile
echo "export DAEMON_NAME=\$TARGET" >> ~/.bash_profile
# This value will be different for each node.
echo "export DAEMON_HOME=$HOME/.ununifi" >> ~/.bash_profile
echo "export DAEMON_ALLOW_DOWNLOAD_BINARIES=false" >> ~/.bash_profile
echo "export DAEMON_LOG_BUFFER_SIZE=512" >> ~/.bash_profile
echo "export DAEMON_RESTART_AFTER_UPGRADE=true" >> ~/.bash_profile
echo "export UNSAFE_SKIP_BACKUP=true" >> ~/.bash_profile
```

プロファイルをソースして、これらの変数にアクセスできるようにします：

```Bash
source ~/.bash_profile
```

### Set up folder structure（フォルダ構造を設定する）

```Bash
mkdir -p $DAEMON_HOME/cosmovisor
mkdir -p $DAEMON_HOME/cosmovisor/genesis
mkdir -p $DAEMON_HOME/cosmovisor/genesis/bin
mkdir -p $DAEMON_HOME/cosmovisor/upgrades
```

### Set up genesis binary（ジェネシスバイナリを設定する）

Cosmovisor はジェネシス時にどのバイナリを使用するかを知る必要があります。これを `$DAEMON_HOME/cosmovisor/genesis/bin` に配置します。

```Bash
cp ~/go/bin/$DAEMON_NAME $DAEMON_HOME/cosmovisor/genesis/bin
```

### Set up service（サービスを設定する）

Cosmovisor に送信されたコマンドは、基盤となるバイナリに送信されます。たとえば、`cosmovisor version` と入力するのは、`sunrised version` と入力するのと同じです。しかし、`sunrised` をプロセスマネージャーで管理するのと同様に、エラーや再起動など何かが発生した場合には、Cosmovisor が自動的に再起動されるようにしたいと考えています。まず、サービスファイルを作成します。

```Bash
sudo nano /lib/systemd/system/cosmovisor.service
```

以下の内容を自分の設定に合わせて変更してください。

```Bash
[Unit]
Description=Cosmovisor daemon
After=network-online.target
[Service]
Environment="DAEMON_NAME=sunrised"
Environment="DAEMON_HOME=/home/<your-user>/.sunrise"
Environment="DAEMON_RESTART_AFTER_UPGRADE=true"
Environment="DAEMON_ALLOW_DOWNLOAD_BINARIES=false" // if want auto-upgrade, set true
Environment="DAEMON_LOG_BUFFER_SIZE=512"
Environment="UNSAFE_SKIP_BACKUP=true"
User=<your-user>
ExecStart=/home/<your-user>/go/bin/cosmovisor start
Restart=always
RestartSec=3
LimitNOFILE=infinity
LimitNPROC=infinity
[Install]
WantedBy=multi-user.target
```

> !! 環境変数が何をするかについての説明は、[こちら](https://docs.cosmos.network/main/run-node/cosmovisor.html)にあります。自分の設定に応じて、それらを変更してください。

### Start Cosmovisor（Cosmovisor を起動する）

> !! スナップショットから同期している場合は、まだ Cosmovisor を起動しないでください。最後に、サービスを有効化して起動します。

```Bash
sudo systemctl daemon-reload
sudo systemctl restart systemd-journald
sudo systemctl enable cosmovisor
sudo systemctl start cosmovisor
```

以下のコマンドを使用して、正常に実行されているか確認してください。

```Bash
sudo systemctl status cosmovisor
```

サービスの起動後にモニタリングが必要な場合は、以下のコマンドでログを表示できます。

```Bash
sudo journalctl -u cosmovisor -f -o cat
```
