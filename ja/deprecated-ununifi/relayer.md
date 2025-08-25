# IBCリレーヤー

IBCリレーヤーを設定することで、UnUniFiと他のブロックチェーンとの間にIBCの新しい接続とチャネルを作成できます。

UnUniFiは[Chain Registry](https://github.com/cosmos/chain-registry)に`ununifi`として登録されています。

## Goリレーヤーでのリレーヤーの設定（推奨）

詳細は[こちら](https://github.com/cosmos/relayer)をご覧ください。

まず、[Go](https://go.dev/doc/install)をインストールします。

## RustリレーヤーHermesでのリレーヤーの設定（非推奨）

まず、[Rust](https://www.rust-lang.org/tools/install)をインストールします。

次に、以下のコマンドを実行します。

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install librust-openssl-dev build-essential git -y

cargo install ibc-relayer-cli --bin hermes --locked
hermes version

echo word1 ... word12or24 > ~/mnemonic.txt
```

### 設定のセットアップ

- [CosmosHub](https://github.com/UnUniFi/gitbook/blob/main/develop/relayer/cosmoshub.md)
- [Axelar](https://github.com/UnUniFi/gitbook/blob/main/develop/relayer/axelar.md)
- [Neutron](https://github.com/UnUniFi/gitbook/blob/main/develop/relayer/neutron.md)

### デーモンの設定

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

### デーモンの監視

```bash
journalctl -u hermes.service -f
```

## クライアントと接続

| チェーンID | クライアント | 接続 |
| --------------- | ----------------- | -------------- |
| `osmosis-1` | `07-tendermint-8` | `connection-6` |
| `cosmoshub-4` | `07-tendermint-3` | `connection-7` |
| `axelar-dojo-1` | `07-tendermint-5` | `connection-8` |
| `neutron-1` | `07-tendermint-4` | `connection-9` |

チャネルについては、[こちら](ibc-channels.md)をご覧ください。
