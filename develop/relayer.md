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

### `~/.hermes/config.toml` for Cosmos Hub

```bash
hermes keys add --key-name keyhub --chain cosmoshub-4 --mnemonic-file ~/mnemonic.txt
rm ~/mnemonic.txt
mkdir ~/.hermes
vi ~/.hermes/config.toml
```

```toml
[global]
log_level = "info"

[mode.clients]
enabled = true
refresh = true
misbehaviour = true

[mode.connections]
enabled = false

[mode.channels]
enabled = false

[mode.packets]
enabled = true
clear_interval = 100
clear_on_start = true
tx_confirmation = false
auto_register_counterparty_payee = false

[rest]
enabled = false
host = "127.0.0.1"
port = 3000

[telemetry]
enabled = false
host = "127.0.0.1"
port = 3001

[[chains]]
id = "cosmoshub-4"
type = "CosmosSdk"
rpc_addr = "https://rpc.cosmoshub.strange.love/"
websocket_addr = "wss://rpc.cosmoshub.strange.love/websocket"
grpc_addr = "https://grpc.cosmos.nodestake.top/"
rpc_timeout = "10s"
batch_delay = "500ms"
trusted_node = false
account_prefix = "cosmos"
key_name = "keyhub"
key_store_type = "Test"
store_prefix = "ibc"
default_gas = 100000
max_gas = 400000
gas_multiplier = 1.1
max_msg_num = 30
max_tx_size = 180000
max_grpc_decoding_size = 33554432
clock_drift = "5s"
max_block_time = "30s"
ccv_consumer_chain = false
memo_prefix = ""
sequential_batch_tx = false

[chains.trust_threshold]
numerator = "1"
denominator = "3"

[chains.gas_price]
price = 0.1
denom = "uatom"

[chains.packet_filter]
policy = "allow"
list = [[
    "transfer",
    "channel-569",
]]

[chains.packet_filter.min_fees]

[chains.address_type]
derivation = "cosmos"

[[chains]]
id = "ununifi-beta-v1"
type = "CosmosSdk"
rpc_addr = "http://a.lcd.ununifi.cauchye.net:26657"
websocket_addr = "ws://a.lcd.ununifi.cauchye.net:26657/websocket"
grpc_addr = "http://a.lcd.ununifi.cauchye.net:9090"
rpc_timeout = "10s"
batch_delay = "500ms"
trusted_node = false
account_prefix = "ununifi"
key_name = "keyununifi"
key_store_type = "Test"
store_prefix = "ibc"
default_gas = 100000
max_gas = 400000
gas_multiplier = 1.1
max_msg_num = 30
max_tx_size = 180000
max_grpc_decoding_size = 33554432
clock_drift = "5s"
max_block_time = "30s"
ccv_consumer_chain = false
memo_prefix = ""
sequential_batch_tx = false

[chains.trust_threshold]
numerator = "1"
denominator = "3"

[chains.gas_price]
price = 0.1
denom = "uguu"

[chains.packet_filter]
policy = "allow"
list = [[
    "transfer",
]]

[chains.packet_filter.min_fees]

[chains.address_type]
derivation = "cosmos"
```

### `~/.hermes/config.toml` for Axelar

```bash
hermes keys add --key-name keyaxelar --chain axelar-dojo-1 --mnemonic-file ~/mnemonic.txt
rm ~/mnemonic.txt
mkdir ~/.hermes
vi ~/.hermes/config.toml
```

```toml
[global]
log_level = "info"

[mode.clients]
enabled = true
refresh = true
misbehaviour = true

[mode.connections]
enabled = false

[mode.channels]
enabled = false

[mode.packets]
enabled = true
clear_interval = 100
clear_on_start = true
tx_confirmation = false
auto_register_counterparty_payee = false

[rest]
enabled = false
host = "127.0.0.1"
port = 3000

[telemetry]
enabled = false
host = "127.0.0.1"
port = 3001

[[chains]]
id = "axelar-dojo-1"
type = "CosmosSdk"
rpc_addr = "https://rpc.axelar.bh.rocks/"
websocket_addr = "wss://rpc.axelar.bh.rocks/websocket"
grpc_addr = "https://axelar-mainnet-grpc.autostake.com/"
rpc_timeout = "10s"
batch_delay = "500ms"
trusted_node = false
account_prefix = "axelar"
key_name = "keyaxelar"
key_store_type = "Test"
store_prefix = "ibc"
default_gas = 100000
max_gas = 400000
gas_multiplier = 1.1
max_msg_num = 30
max_tx_size = 180000
max_grpc_decoding_size = 33554432
clock_drift = "5s"
max_block_time = "30s"
ccv_consumer_chain = false
memo_prefix = ""
sequential_batch_tx = false

[chains.trust_threshold]
numerator = "1"
denominator = "3"

[chains.gas_price]
price = 0.1
denom = "uaxl"

[chains.packet_filter]
policy = "allow"
list = [[
    "transfer",
    "channel-78",
]]

[chains.packet_filter.min_fees]

[chains.address_type]
derivation = "cosmos"

[[chains]]
id = "ununifi-beta-v1"
type = "CosmosSdk"
rpc_addr = "http://a.lcd.ununifi.cauchye.net:26657"
websocket_addr = "ws://a.lcd.ununifi.cauchye.net:26657/websocket"
grpc_addr = "http://a.lcd.ununifi.cauchye.net:9090"
rpc_timeout = "10s"
batch_delay = "500ms"
trusted_node = false
account_prefix = "ununifi"
key_name = "keyununifi"
key_store_type = "Test"
store_prefix = "ibc"
default_gas = 100000
max_gas = 400000
gas_multiplier = 1.1
max_msg_num = 30
max_tx_size = 180000
max_grpc_decoding_size = 33554432
clock_drift = "5s"
max_block_time = "30s"
ccv_consumer_chain = false
memo_prefix = ""
sequential_batch_tx = false

[chains.trust_threshold]
numerator = "1"
denominator = "3"

[chains.gas_price]
price = 0.1
denom = "uguu"

[chains.packet_filter]
policy = "allow"
list = [[
    "transfer",
]]

[chains.packet_filter.min_fees]

[chains.address_type]
derivation = "cosmos"
```

### `~/.hermes/config.toml` for Neutron

```bash
hermes keys add --key-name keyneutron --chain neutron-1 --mnemonic-file ~/mnemonic.txt
rm ~/mnemonic.txt
mkdir ~/.hermes
vi ~/.hermes/config.toml
```

```toml
[global]
log_level = "info"

[mode.clients]
enabled = true
refresh = true
misbehaviour = true

[mode.connections]
enabled = false

[mode.channels]
enabled = false

[mode.packets]
enabled = true
clear_interval = 100
clear_on_start = true
tx_confirmation = false
auto_register_counterparty_payee = false

[rest]
enabled = false
host = "127.0.0.1"
port = 3000

[telemetry]
enabled = false
host = "127.0.0.1"
port = 3001

[[chains]]
id = "neutron-1"
type = "CosmosSdk"
rpc_addr = "http://posthuman-neutron-rpc.ingress.europlots.com/"
websocket_addr = "ws://posthuman-neutron-rpc.ingress.europlots.com/websocket"
grpc_addr = "https://grpc-web.novel.remedy.tm.p2p.org/"
rpc_timeout = "10s"
batch_delay = "500ms"
trusted_node = false
account_prefix = "neutron"
key_name = "keyneutron"
key_store_type = "Test"
store_prefix = "ibc"
default_gas = 100000
max_gas = 400000
gas_multiplier = 1.1
max_msg_num = 30
max_tx_size = 180000
max_grpc_decoding_size = 33554432
clock_drift = "5s"
max_block_time = "30s"
ccv_consumer_chain = false
memo_prefix = ""
sequential_batch_tx = false

[chains.trust_threshold]
numerator = "1"
denominator = "3"

[chains.gas_price]
price = 0.1
denom = "untrn"

[chains.packet_filter]
policy = "allow"
list = [
    [
    "transfer",
    "channel-2",
],
    [
    "transfer",
    "channel-1",
],
]

[chains.packet_filter.min_fees]

[chains.address_type]
derivation = "cosmos"

[[chains]]
id = "ununifi-beta-v1"
type = "CosmosSdk"
rpc_addr = "http://a.lcd.ununifi.cauchye.net:26657"
websocket_addr = "ws://a.lcd.ununifi.cauchye.net:26657/websocket"
grpc_addr = "http://a.lcd.ununifi.cauchye.net:9090"
rpc_timeout = "10s"
batch_delay = "500ms"
trusted_node = false
account_prefix = "ununifi"
key_name = "keyununifi"
key_store_type = "Test"
store_prefix = "ibc"
default_gas = 100000
max_gas = 400000
gas_multiplier = 1.1
max_msg_num = 30
max_tx_size = 180000
max_grpc_decoding_size = 33554432
clock_drift = "5s"
max_block_time = "30s"
ccv_consumer_chain = false
memo_prefix = ""
sequential_batch_tx = false

[chains.trust_threshold]
numerator = "1"
denominator = "3"

[chains.gas_price]
price = 0.1
denom = "uguu"

[chains.packet_filter]
policy = "allow"
list = [[
    "transfer",
]]

[chains.packet_filter.min_fees]

[chains.address_type]
derivation = "cosmos"
```

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
