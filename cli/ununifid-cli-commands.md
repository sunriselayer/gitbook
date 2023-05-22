# Useful CLI Commands

Get standard debug info from the `ununifi` daemon:

```bash
ununifid status
```

Check if your node is catching up:

```bash
# Query via the RPC (default port: 26657)
curl http://localhost:26657/status | jq .result.sync_info.catching_up
```

Get your node ID:

```bash
ununifid tendermint show-node-id
```

{% hint style="info" %}
Your peer address will be the result of this plus host and port, i.e. `<id>@<host>:26656` if you are using the default port.
{% endhint %}

Check if you are jailed or tombstoned:

```bash
ununifid query slashing signing-info $(ununifid tendermint show-validator)
```

Get your `valoper` address:

```bash
ununifid keys show <your-key-name> -a --bech val
```

See keys on the current box:

```bash
ununifid keys list
```

Import a key from a mnemonic:

```bash
ununifid keys add <new-key-name> --recover
```

Export a private key (warning: don't do this unless you know what you're doing!)

```bash
ununifid keys export <your-key-name> --unsafe --unarmored-hex
```

Withdraw rewards (including validator commission), where `ununifivaloper1...` is the validator address:

```bash
ununifid tx distribution withdraw-rewards <ununifivaloper1...> --from <your-key>  --commission
```

Stake:

```bash
ununifid tx staking delegate <ununifivaloper1...> <AMOUNT>uununifi --from <your-key>
```

Find out what the JSON for a command would be using `--generate-only`:

```bash
ununifid tx bank send $(ununifid keys show <your-key-name> -a) <recipient addr> <AMOUNT>uununifi --generate-only
```

Query the validator set (and jailed status) via CLI:

```bash
ununifid query staking validators --limit 1000 -o json | jq -r '.validators[] | [.operator_address, (.tokens|tonumber / pow(10; 6)), .description.moniker, .jail, .status] | @csv' | column -t -s"," | sort -k2 -n -r | nl
```

Get contract state:

```bash
ununifid q wasm contract-state all <contract-address>
```
