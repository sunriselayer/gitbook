# Relayer

By setting up IBC relayer, you can create new connections and channels of IBC between UnUniFi and other blockchains.

- [Go Relayer](https://github.com/cosmos/relayer)
- [Hermes](https://hermes.informal.systems/)

UnUniFi is registered in [Chain Registry](https://github.com/cosmos/chain-registry) as `ununifi`.

## Setting up Relayer with Hermes

At first, install [Rust](https://www.rust-lang.org/tools/install)

Then, run the commands below:

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install librust-openssl-dev build-essential git -y

cargo install ibc-relayer-cli --bin hermes --locked
hermes version

echo word1 ... word12or24 > ~/mnemonic.txt
```

### Setting up config

- [CosmosHub](./relayer/cosmoshub.md)
- [Axelar](./relayer/axelar.md)
- [Neutron](./relayer/neutron.md)

### Setting up daemon

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

### Monitoring daemon

```bash
journalctl -u hermes.service -f
```
