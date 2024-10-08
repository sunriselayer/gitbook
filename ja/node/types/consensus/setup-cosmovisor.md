# Cosmovisor のセットアップ

**メインネットでは、ノードの実行に Cosmovisor を使用することをおすすめします。**

Cosmovisor のセットアップは比較的簡単です。ただし、特定の環境変数とフォルダ構造が設定されていることが前提となります。
Cosmovisor を使用すると、チェーンアップグレード用のバイナリを事前にダウンロードできるため、ダウンタイムがゼロ（またはほぼゼロ）のチェーンアップグレードが可能になります。また、ローカルのタイムゾーンの関係でチェーンアップグレードのタイミングが悪い場合にも便利です。
深夜にストレスの多い運用タスクを行うよりも、自動化できる方が常に良いでしょう。それが Cosmovisor の目指すところです。

## インストール

まず、cosmovisor を入手します（推奨アプローチ）：

```Bash
# 特定のバージョンを指定する場合：
go install github.com/cosmos/cosmos-sdk/cosmovisor/cmd/cosmovisor@v1.0.0
```

> !! Cosmovisor を使用する際は、バイナリの自動ダウンロードがオフになっていることを確認してください。

### シェルに環境変数を追加する

いくつかの環境変数は、各ノードと各ネットワークに適切な値を設定する必要があります。

```Bash
echo "export CHAIN_REPO=https://github.com/UnUniFi/chain" >> ~/.bash_profile
echo "export CHAIN_REPO_BRANCHE=main" >> ~/.bash_profile
echo "export TARGET=ununifid" >> ~/.bash_profile
echo "export TARGET_HOME=.ununifi" >> ~/.bash_profile
# この値は各ノードで異なります。
echo "export MONIKER=<your-moniker>" >> ~/.bash_profile
echo "export CHAIN_ID=ununifi-beta-v1" >> ~/.bash_profile
# この値はメインネットの例です。
echo "export GENESIS_FILE_URL=https://raw.githubusercontent.com/UnUniFi/network/main/launch/ununifi-beta-v1/genesis.json" >> ~/.bash_profile
echo "export SETUP_NODE_CONFIG_ENV=TRUE" >> ~/.bash_profile
echo "export SETUP_NODE_ENV=TRUE" >> ~/.bash_profile
echo "export SETUP_NODE_MASTER=TRUE" >> ~/.bash_profile
echo "export DAEMON_NAME=\$TARGET" >> ~/.bash_profile
# この値は各ノードで異なります。
echo "export DAEMON_HOME=$HOME/.ununifi" >> ~/.bash_profile
echo "export DAEMON_ALLOW_DOWNLOAD_BINARIES=false" >> ~/.bash_profile
echo "export DAEMON_LOG_BUFFER_SIZE=512" >> ~/.bash_profile
echo "export DAEMON_RESTART_AFTER_UPGRADE=true" >> ~/.bash_profile
echo "export UNSAFE_SKIP_BACKUP=true" >> ~/.bash_profile
```

次に、これらの変数にアクセスできるようにプロファイルをソースします：

```Bash
source ~/.bash_profile
```

### フォルダ構造のセットアップ

```Bash
mkdir -p $DAEMON_HOME/cosmovisor
mkdir -p $DAEMON_HOME/cosmovisor/genesis
mkdir -p $DAEMON_HOME/cosmovisor/genesis/bin
mkdir -p $DAEMON_HOME/cosmovisor/upgrades
```

### ジェネシスバイナリのセットアップ

Cosmovisor は、ジェネシス時にどのバイナリを使用するかを知る必要があります。これを `$DAEMON_HOME/cosmovisor/genesis/bin` に配置します。

```Bash
cp ~/go/bin/$DAEMON_NAME $DAEMON_HOME/cosmovisor/genesis/bin
```

### サービスのセットアップ

Cosmovisor に送信されたコマンドは、基礎となるバイナリに送信されます。例えば、`cosmovisor version` は `ununifid version` と入力するのと同じです。
それでも、プロセスマネージャーを使用して `ununifid` を管理するのと同様に、エラーや再起動など何かが起こった場合に、Cosmovisor が自動的に再起動されるようにしたいと思います。
まず、サービスファイルを作成します：

```Bash
sudo nano /lib/systemd/system/cosmovisor.service
```

以下の内容をあなたのセットアップに合わせて変更してください

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

> !! 環境変数の機能については[こちら](https://docs.cosmos.network/master/run-node/cosmovisor.html)で説明されています。セットアップに応じて変更してください。

### Cosmovisor の起動

> !! スナップショットから同期する場合は、まだ Cosmovisor を起動しないでください。
> 最後に、サービスを有効にして起動します。

```Bash
sudo systemctl daemon-reload
sudo systemctl restart systemd-journald
sudo systemctl enable cosmovisor
sudo systemctl start cosmovisor
```

以下のコマンドを使用して、実行中であることを確認します：

```Bash
sudo systemctl status cosmovisor
```

起動後にサービスを監視する必要がある場合は、以下のコマンドでログを表示できます：

```Bash
sudo journalctl -u cosmovisor -f -o cat
```
