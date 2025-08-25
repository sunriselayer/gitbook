# Cosmovisorのセットアップ

**メインネットでは、Cosmovisorを使用してノードを実行することをお勧めします。**

Cosmovisorのセットアップは比較的簡単です。ただし、特定の環境変数とフォルダ構造を設定する必要があります。
Cosmovisorを使用すると、チェーンのアップグレードのために事前にバイナリをダウンロードできます。つまり、ダウンタイムをゼロ（またはほぼゼロ）にすることができます。また、ローカルのタイムゾーンによってチェーンのアップグレードが都合の悪い時間に行われる場合にも便利です。
深夜にストレスの多い運用タスクを行うよりも、自動化できる方が常に優れています。Cosmovisorがやろうとしているのはまさにそれです。

## インストール

まず、cosmovisorを入手します（推奨されるアプローチ）。

```Bash
# 特定のバージョンをターゲットにする場合：
go install github.com/cosmos/cosmos-sdk/cosmovisor/cmd/cosmovisor@v1.0.0
```

> !! Cosmovisorを使用する場合は、バイナリの自動ダウンロードがオンになっていないことを確認してください。

### シェルに環境変数を追加する

一部の環境変数は、各ノードおよび各ネットワークに対して適切な値に設定する必要があります。

```Bash
echo "export CHAIN_REPO=https://github.com/UnUniFi/chain" >> ~/.bash_profile
echo "export CHAIN_REPO_BRANCHE=main" >> ~/.bash_profile
echo "export TARGET=ununifid" >> ~/.bash_profile
echo "export TARGET_HOME=.ununifi" >> ~/.bash_profile
# この値はノードごとに異なります。
echo "export MONIKER=<your-moniker>" >> ~/.bash_profile
echo "export CHAIN_ID=ununifi-beta-v1" >> ~/.bash_profile
# この値はメインネットの例です。
echo "export GENESIS_FILE_URL=https://raw.githubusercontent.com/UnUniFi/network/main/launch/ununifi-beta-v1/genesis.json" >> ~/.bash_profile
echo "export SETUP_NODE_CONFIG_ENV=TRUE" >> ~/.bash_profile
echo "export SETUP_NODE_ENV=TRUE" >> ~/.bash_profile
echo "export SETUP_NODE_MASTER=TRUE" >> ~/.bash_profile
echo "export DAEMON_NAME=\$TARGET" >> ~/.bash_profile
# この値はノードごとに異なります。
echo "export DAEMON_HOME=$HOME/.ununifi" >> ~/.bash_profile
echo "export DAEMON_ALLOW_DOWNLOAD_BINARIES=false" >> ~/.bash_profile
echo "export DAEMON_LOG_BUFFER_SIZE=512" >> ~/.bash_profile
echo "export DAEMON_RESTART_AFTER_UPGRADE=true" >> ~/.bash_profile
echo "export UNSAFE_SKIP_BACKUP=true" >> ~/.bash_profile
```

次に、プロファイルを読み込んでこれらの変数にアクセスできるようにします。

```Bash
source ~/.bash_profile
```

### フォルダ構造の設定

```Bash
mkdir -p $DAEMON_HOME/cosmovisor
mkdir -p $DAEMON_HOME/cosmovisor/genesis
mkdir -p $DAEMON_HOME/cosmovisor/genesis/bin
mkdir -p $DAEMON_HOME/cosmovisor/upgrades
```

### ジェネシスバイナリの設定

Cosmovisorは、ジェネシスで使用するバイナリを知る必要があります。これを`$DAEMON_HOME/cosmovisor/genesis/bin`に置きます。

```Bash
cp ~/go/bin/$DAEMON_NAME $DAEMON_HOME/cosmovisor/genesis/bin
```

### サービスの設定

Cosmovisorに送信されるコマンドは、基盤となるバイナリに送信されます。たとえば、`cosmovisor version`は`ununifid version`と入力するのと同じです。
それにもかかわらず、プロセス管理ツールを使用して`ununifid`を管理するのと同じように、エラーや再起動などの問題が発生した場合にCosmovisorが自動的に再起動されるようにしたいと考えています。
まず、サービスファイルを作成します。

```Bash
sudo nano /lib/systemd/system/cosmovisor.service
```

以下の内容を自分の設定に合わせて変更します。

```Bash
[Unit]
Description=Cosmovisor daemon
After=network-online.target
[Service]
Environment="DAEMON_NAME=ununifid"
Environment="DAEMON_HOME=/home/<your-user>/.ununifi"
Environment="DAEMON_RESTART_AFTER_UPGRADE=true"
Environment="DAEMON_ALLOW_DOWNLOAD_BINARIES=false"
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

> !! 環境変数の機能については、[こちら](https://docs.cosmos.network/master/run-node/cosmovisor.html)をご覧ください。設定に応じて変更してください。

### Cosmovisorの起動

> !! スナップショットから同期する場合は、まだCosmovisorを起動しないでください。
> 最後に、サービスを有効にして起動します。

```Bash
sudo systemctl daemon-reload
sudo systemctl restart systemd-journald
sudo systemctl enable cosmovisor
sudo systemctl start cosmovisor
```

実行中であることを確認するには、次を使用します。

```Bash
sudo systemctl status cosmovisor
```

起動後にサービスを監視する必要がある場合は、次を使用してログを表示できます。

```Bash
sudo journalctl -u cosmovisor -f -o cat
```
