# Cosmovisorの設定

**メインネットでは、ノードの実行にCosmovisorを使用することをお勧めします。**

Cosmovisorの設定は比較的簡単です。ただし、特定の環境変数とフォルダ構造が設定されている必要があります。\
Cosmovisorを使用すると、チェーンのアップグレードのためにバイナリを事前にダウンロードできます。つまり、ダウンタイムをゼロ（またはほぼゼロ）に抑えてチェーンのアップグレードを実行できます。また、ローカルのタイムゾーンによってチェーンのアップグレードが不都合な時間に発生する場合にも便利です。\
夜遅くにストレスの多い運用タスクを実行するよりも、それらを自動化できる方が常に優れています。それがCosmovisorが試みることです。

## インストール

まず、cosmovisorを入手します（推奨されるアプローチ）：

```Bash
# 特定のバージョンをターゲットにするには：
go install github.com/cosmos/cosmos-sdk/cosmovisor/cmd/cosmovisor@v1.0.0
```

### シェルに環境変数を追加する

一部の環境変数は、各ノードと各ネットワークに対して適切な値に設定する必要があります。

```Bash
echo "export DAEMON_NAME=sunrised" >> ~/.profile
echo "export DAEMON_HOME=$HOME/.sunrised" >> ~/.profile
echo "export DAEMON_ALLOW_DOWNLOAD_BINARIES=true" >> ~/.profile
echo "export DAEMON_LOG_BUFFER_SIZE=512" >> ~/.profile
echo "export DAEMON_RESTART_AFTER_UPGRADE=true" >> ~/.profile
echo "export UNSAFE_SKIP_BACKUP=true" >> ~/.profile
```

次に、プロファイルをソースして、これらの変数にアクセスできるようにします。

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

[Github](https://github.com/sunriselayer/network)でジェネシスのバイナリバージョンを確認してください。

```Bash
wget https://github.com/sunriselayer/sunrise/releases/download/<version>/sunrised
cp sunrised $DAEMON_HOME/cosmovisor/genesis/bin
```

### サービスの設定

Cosmovisorに送信されたコマンドは、基盤となるバイナリに送信されます。たとえば、`cosmovisor version`は`sunrised version`と入力するのと同じです。それでも、`sunrised`をプロセス管理ツールで管理するのと同じように、エラーや再起動などが発生した場合にCosmovisorが自動的に再起動されるようにしたいと考えています。まず、サービスファイルを作成します。

```Bash
sudo vi /lib/systemd/system/cosmovisor.service
```

以下の内容を自分の設定に合わせて変更してください。

```Bash
[Unit]
Description=Cosmovisor daemon
After=network-online.target
[Service]
Environment="DAEMON_NAME=sunrised"
Environment="DAEMON_HOME=$DAEMON_HOME"
Environment="DAEMON_RESTART_AFTER_UPGRADE=true"
Environment="DAEMON_ALLOW_DOWNLOAD_BINARIES=true" // 推奨
Environment="DAEMON_LOG_BUFFER_SIZE=512"
Environment="UNSAFE_SKIP_BACKUP=true"
User=$USER
ExecStart=${HOME}/go/bin/cosmovisor start
Restart=always
RestartSec=3
LimitNOFILE=infinity
LimitNPROC=infinity
[Install]
WantedBy=multi-user.target
```

{% hint style="info" %}
環境変数の説明は[こちら](https://docs.cosmos.network/main/run-node/cosmovisor.html)にあります。設定に応じて変更してください。
{% endhint %}

### Cosmovisorの起動

{% hint style="warning" %}
スナップショットから同期する場合は、まだCosmovisorを起動しないでください。スナップショットをダウンロードして`$HOME/.sunrise/data`に展開します。最後に、サービスを有効にして起動します。
{% endhint %}

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
