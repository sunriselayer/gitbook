# IBC Relayer

By setting up the IBC relayer, you can create new connections and channels of IBC between Sunrise and other blockchains.

## Setting up relayer with Go relayer (Recommended)

You can see details [here](https://github.com/cosmos/relayer).

First, install [Go](https://go.dev/doc/install)

## Setting up relayer with Rust relayer Hermes (Not recommended)

First, install [Rust](https://www.rust-lang.org/tools/install)

Then, run the commands below:

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install librust-openssl-dev build-essential git -y

cargo install ibc-relayer-cli --bin hermes --locked
hermes version

echo word1 ... word12or24 > ~/mnemonic.txt
```

### Setting up config

Under construction.

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

## Clients and Connections
