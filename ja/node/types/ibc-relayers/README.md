# IBC リレーヤー

IBC リレーヤーを設定することで、Sunrise と IRIS の Blockchain 間に新しい IBC 接続やチャンネルを作成できます。

## Go リレーヤーでの設定（非推奨）

詳細は[こちら](https://github.com/cosmos/relayer)をご覧ください。

まず、[Go](https://go.dev/doc/install)をインストールしてください。

## Rust 製リレーヤー Hermes での設定（推奨）

詳細は[こちら](http://hermes.informal.systems)をご覧ください。

まず、[Rust](https://www.rust-lang.org/tools/install)をインストールしてください。

次に、以下のコマンドを実行します：

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install librust-openssl-dev build-essential git -y

cargo install ibc-relayer-cli --bin hermes --locked
hermes version

echo word1 ... word12or24 > ~/mnemonic.txt
```

### アカウントの設定

まず、両方のチェーンで十分な資金を持つウォレットが必要です。
このチュートリアルでは、リレーしたいチェーンに既にウォレットが作成されており、それぞれのウォレットに資金が割り当てられていることを前提としています。

```bash
hermes keys add --key-name <ユーザー名> --chain <ibc-0> --mnemonic-file mnemonic.txt
hermes keys add --key-name <ユーザー名> --chain <ibc-1> --mnemonic-file mnemonic.txt
```

### 設定ファイル

`hermes config auto`コマンドを使用すると、[chain-registry](https://github.com/cosmos/chain-registry)にあるチェーン用の設定ファイルを自動生成できます：

テストネットの場合は、各パラメータを自分で設定する必要があります。詳細は[ドキュメント](https://hermes.informal.systems/documentation/configuration/index.html)を参照してください。

```bash
hermes config auto --output $HOME/.hermes/config.toml --chain <ibc-0>:<key-ibc-0> <ibc-1>:<key-ibc-1> --chain
```

#### 新しいリレーパスの追加

以下の設定は、既に IBC チャンネルが確立されているメインネットでは必要ありません。新しい接続を開始する場合のみ、以下の手順に従ってください。

- 接続の作成

まず、`ibc-0`の状態を追跡する`ibc-1`上にクライアントを作成します。これには 07-tendermint-0 という識別子が割り当てられます：

```bash
hermes create client --host-chain <ibc-1> --reference-chain <ibc-0>
```

- 接続の作成

両方のチェーンにクライアントを作成した後、それらの間に接続を確立する必要があります。両方のチェーンは、最初の接続の識別子として connection-0 を割り当てます：

```bash
hermes create connection --a-chain <ibc-0> --b-chain <ibc-1>
```

コマンドが正常に実行されると、`connection ID`が出力されるはずです。

- チャンネル識別子

最後に、接続が確立された後、その上に新しいチャンネルを開くことができます。両方のチェーンは、最初のチャンネルの識別子として channel-0 を割り当てます：

```bash
hermes create channel --a-chain <ibc-0> --a-connection <connection-id> --a-port transfer --b-port transfer
```

コマンドが正常に実行されると、両方のチェーンのチャンネル ID が出力されるはずです。

これらを`.hermes/config.toml`に追加します

```yml
[chains.packet_filter]
policy = "allow"
list = [[
    "transfer",
    "channel-0",
]]
```

設定が完了したら、以下のコマンドでリレーヤーを起動できます。

```bash
hermes start
```

### デーモンの設定

再起動後に自動的に実行されるように、SystemD を設定することをお勧めします。

```bash
sudo tee /etc/systemd/system/hermes.service > /dev/null <<EOF
[Unit]
Description=Hermes Relayer Service
After=network-online.target

[Service]
User=ubuntu
ExecStart=/usr/local/bin/hermes start
Restart=on-failure
RestartSec=3
LimitNOFILE=1400000

[Install]
WantedBy=multi-user.target
EOF

sudo systemctl enable hermes
sudo systemctl daemon-reload
sudo systemctl start hermes
```

### デーモンの監視

```bash
journalctl -u hermes.service -f
```
