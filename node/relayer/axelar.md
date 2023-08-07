
# `~/.hermes/config.toml` for Axelar

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
enabled = true

[mode.channels]
enabled = true

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
    "channel-1",
]]

[chains.packet_filter.min_fees]

[chains.address_type]
derivation = "cosmos"
```

`~/.hermes/config.toml` can be updated with the command below.

```bash
hermes config auto --output $HOME/.hermes/config.toml --chains axelar
```
