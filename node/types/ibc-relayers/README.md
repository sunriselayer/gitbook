# IBC Relayer

By setting up the IBC relayer, you can create new connections and channels of IBC between Sunrise and other blockchains.

## Setting up relayer with Go relayer (Deprecated)

You can see details [here](https://github.com/cosmos/relayer).

First, install [Go](https://go.dev/doc/install)

## Setting up relayer with Rust relayer Hermes (Recommended)

You can see details [here](http://hermes.informal.systems).

First, install [Rust](https://www.rust-lang.org/tools/install)

Then, run the commands below:

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install librust-openssl-dev build-essential git -y

cargo install ibc-relayer-cli --bin hermes --locked
hermes version

echo word1 ... word12or24 > ~/mnemonic.txt
```

### Setup accounts

First, you need a wallet with enough funds on both chains.
This tutorial assumes that you already have wallets created on the chains you want to relay on, and that these wallets have funds allocated to each of them.

```bash
hermes keys add --key-name <user-name> --chain <ibc-0> --mnemonic-file mnemonic.txt
hermes keys add --key-name <user-name> --chain <ibc-1> --mnemonic-file mnemonic.txt
```

### Configuration file

The command hermes config auto provides a way to automatically generate a configuration file for chains in the [chain-registry](https://github.com/cosmos/chain-registry):

You must set each parameter yourself for the testnet. See the [documentation](https://hermes.informal.systems/documentation/configuration/index.html) for more details.

```bash
hermes config auto --output $HOME/.hermes/config.toml --chain <ibc-0>:<key-ibc-0> <ibc-1>:<key-ibc-1> --chain 
```

#### Add a new relay path

The following settings are not required for mainnets that already have an established IBC channel. Follow only if you are starting a new connection.

- Create a connection

First, create a client on `ibc-1` tracking the state of `ibc-0`. It will be assigned 07-tendermint-0 as its identifier:

```bash
hermes create client --host-chain <ibc-1> --reference-chain <ibc-0>
```

- Create a connection

After creating clients on both chains, you have to establish a connection between them. Both chains will assign connection-0 as the identifier of their first connection:

```bash
hermes create connection --a-chain <ibc-0> --b-chain <ibc-1>
```

If the command runs successfully, it should output the `connection ID`.

- Channel identifiers

Finally, after the connection has been established, you can now open a new channel on top of it. Both chains will assign channel-0 as the identifier of their first channel:

```bash
hermes create channel --a-chain <ibc-0> --a-connection <connection-id> --a-port transfer --b-port transfer
```

If the command runs successfully, it should output the channel IDs of both chains.

Add these to `.hermes/config.toml`

```yml
[chains.packet_filter]
policy = "allow"
list = [[
    "transfer",
    "channel-0",
]]
```

Once the configuration is complete, you can start the relayer with the following command.

```bash
hermes start
```


### Setting up daemon

Recommend setting SystemD to run automatically after reboot.

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

### Monitoring daemon

```bash
journalctl -u hermes.service -f
```
