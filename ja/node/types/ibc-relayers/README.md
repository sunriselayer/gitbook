# **IBC Relayers**

IBC リレイヤーを設定することで、Sunrise と他のブロックチェーン間で新しい IBC の接続やチャネルを作成することができます。

## Go リレイヤーを使用したリレイヤーの設定（推奨）

[詳細](https://github.com/cosmos/relayer)はここで確認できます。

まず、[Go](https://go.dev/doc/install)をインストールしてください。

## Rust リレイヤーの Hermes を使用したリレイヤーの設定（非推奨）

まず、[Rust](https://www.rust-lang.org/tools/install)をインストールしてください。

次に、以下のコマンドを実行してください。

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install librust-openssl-dev build-essential git -y

cargo install ibc-relayer-cli --bin hermes --locked
hermes version

echo word1 ... word12or24 > ~/mnemonic.txt
```

### config の設定

Under construction.

### daemon の設定

```bash
sudo tee /etc/systemd/system/hermes.service > /dev/null <<EOF
[Unit]
  Description=Hermes relayer daemon
  After=network-online.target
[Service]
  User=$USER
  ExecStart=$HOME/.cargo/bin/hermes start
  Restart=on-failure
  RestartSec=3
  LimitNOFILE=4096
[Install]
  WantedBy=multi-user.target
EOF
sudo systemctl enable hermes
sudo systemctl daemon-reload
sudo systemctl restart hermes
```

### daemon のモニタリング

```bash
journalctl -u hermes.service -f
```

## Clients and Connections
