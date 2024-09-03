---
description: >-
  The `wasm` module allows you to manage CosmWasm smart contract.
---

# `wasm`

**Query:**

| Name                                                               | Description                                                  |
| :----------------------------------------------------------------- | :----------------------------------------------------------- |
| [build-address](wasm.md#build-address)                         | Build contract address                                       |
| [code](wasm.md#code)                                           | Downloads wasm bytecode for given code id                    |
| [code-info](wasm.md#code-info)                                 | Prints out metadata of a code id                             |
| [contract](wasm.md#contract)                                   | Prints out metadata of a contract given its address          |
| [contract-history](wasm.md#contract-history)                   | Prints out the code history for a contract given its address |
| [contract-state](wasm.md#contract-state)                       | Querying commands for the wasm module                        |
| [libwasmvm-version](wasm.md#libwasmvm-version)                 | Get libwasmvm version                                        |
| [list-code](wasm.md#list-code)                                 | List all wasm bytecode on the chain                          |
| [list-contract-by-code](wasm.md#list-contract-by-code)         | List wasm all bytecode on the chain for given code id        |
| [list-contracts-by-creator](wasm.md#list-contracts-by-creator) | List all contracts by creator                                |
| [params](wasm.md#params)                                       | Query the current wasm parameters                            |
| [pinned](wasm.md#pinned)                                       | List all pinned code ids                                     |

**Tx:**

| Name                                                               | Description                                               |
| :----------------------------------------------------------------- | :-------------------------------------------------------- |
| [clear-contract-admin](wasm.md#clear-contract-admin)           | Clears admin for a contract to prevent further migrations |
| [execute](wasm.md#execute)                                     | Execute a command on a wasm contract                      |
| [grant](wasm.md#grant)                                         | Grant authorization to an address                         |
| [instantiate](wasm.md#instantiate)                             | Instantiate a wasm contract                               |
| [instantiate2](wasm.md#instantiate2)                           | Instantiate a wasm contract with predictable address      |
| [migrate](wasm.md#migrate)                                     | Migrate a wasm contract to a new code version             |
| [set-contract-admin](wasm.md#set-contract-admin)               | Set new admin for a contract                              |
| [store](wasm.md#store)                                         | Upload a wasm binary                                      |
| [update-instantiate-config](wasm.md#update-instantiate-config) | Update instantiate config for a codeID                    |

## Common flags in `wasm` query <a id="common-query-flags"></a>

Common flags for the `wasm` query command are summarized.

**Flags:**

| Name, shorthand | Type   | Required | Default               | Description                                                                           |
| :-------------- | :----- | :------- | :-------------------- | :------------------------------------------------------------------------------------ |
| --grpc-addr     | string |          |                       | the gRPC endpoint to use for this chain                                               |
| --grpc-insecure |        |          |                       | allow gRPC over insecure channels, if not TLS the server must use TLS                 |
| --height        | int    |          |                       | Use a specific height to query state at (this can error if the node is pruning state) |
| -h, --help      |        |          |                       | Help for \<module name>                                                               |
| --node          | string |          | tcp://localhost:26657 | \<host>:\<port> to Tendermint RPC interface for this chain                            |
| -o, --output    | string |          | text                  | Output format (text \| json)                                                          |

**Global Flags:**

| Name, shorthand | Type   | Required | Default        | Description                                                                   |
| :-------------- | :----- | :------- | :------------- | :---------------------------------------------------------------------------- |
| --chain-id      | string |          |                | The network chain ID                                                          |
| --home          | string |          | $HOME/.ununifi | directory for config and data                                                 |
| --log_format    | string |          |                | The logging format (json \| plain) (default "plain")                          |
| --log_level     | string |          | info           | The logging level (trace \| debug \| info \| warn \| error \| fatal \| panic) |
| --trace         |        |          |                | print out full stack trace on errors                                          |

### Encode Flags <a id="encode-flags"></a>

**Flags:**

| Name, shorthand | Type | Required | Default | Description         |
| :-------------- | :--- | :------- | :------ | :------------------ |
| --ascii         |      |          |         | ascii encoded salt  |
| --b64           |      |          |         | base64 encoded salt |
| --hex           |      |          |         | hex encoded salt    |

### Pagination Flags <a id="pagination-flags"></a>

**Flags:**

| Name, shorthand | Type   | Required | Default | Description                                                                                           |
| :-------------- | :----- | :------- | :------ | :---------------------------------------------------------------------------------------------------- |
| --count-total   |        |          |         | a count total number of records in contract history to query for                                      |
| --limit         | uint   |          |         | pagination limit of contract history to query for (default 100)                                       |
| --offset        | uint   |          |         | pagination offset of contract history to query for                                                    |
| --page          | uint   |          |         | pagination page of contract history to query for. This sets offset to a multiple of limit (default 1) |
| --page-key      | string |          |         | pagination page-key of contract history to query for                                                  |
| --reverse       |        |          |         | results are sorted in descending order                                                                |

## Query

### ununifid query wasm build-address <a id="build-address"></a>

Build contract address

```bash
ununifid query wasm build-address [code-hash] [creator-address] [salt-hex-encoded] [json_encoded_init_args (required when set as fixed)] [flags]
```

**Flags:**

{% hint style="info" %}
Please refer to [Common flags](wasm.md#common-query-flags) & [Encode flags](wasm.md#encode-flags) for details of flags.
{% endhint %}

### ununifid query wasm code <a id="code"></a>

Downloads wasm bytecode for given code id

```bash
ununifid query wasm code [code_id] [output filename] [flags]
```

**Flags:**

{% hint style="info" %}
Please refer to [Common flags](wasm.md#common-query-flags) for details of flags.
{% endhint %}

### ununifid query wasm code-info <a id="code-info"></a>

Prints out metadata of a code id

```bash
ununifid query wasm code-info [code_id] [flags]
```

**Flags:**

{% hint style="info" %}
Please refer to [Common flags](wasm.md#common-query-flags) for details of flags.
{% endhint %}

### ununifid query wasm contract <a id="contract"></a>

Prints out metadata of a contract given its address

```bash
ununifid query wasm contract [bech32_address] [flags]
```

**Flags:**

{% hint style="info" %}
Please refer to [Common flags](wasm.md#common-query-flags) for details of flags.
{% endhint %}

### ununifid query wasm contract-history <a id="contract-history"></a>

Prints out the code history for a contract given its address

```bash
ununifid query wasm contract-history [bech32_address] [flags]
```

**Flags:**

{% hint style="info" %}
Please refer to [Common flags](wasm.md#common-query-flags) & [Pagination flags](wasm.md#pagination-flags) for details of flags.
{% endhint %}

### ununifid query wasm contract-state <a id="contract-state"></a>

Querying commands for the wasm module

```bash
ununifid query wasm contract-state [flags]
ununifid query wasm contract-state [command]
```

**Command:**

| Name, shorthand | Type | Required | Default | Description                                                                      |
| :-------------- | :--- | :------- | :------ | :------------------------------------------------------------------------------- |
| all             |      |          |         | Prints out all internal state of a contract given its address                    |
| raw             |      |          |         | Prints out internal state for key of a contract given its address                |
| smart           |      |          |         | Calls contract with given address with query data and prints the returned result |

```bash
ununifid query wasm contract-state all [bech32_address] [flags]
```

**Flags:**

{% hint style="info" %}
Please refer to [Common flags](wasm.md#common-query-flags) & [Pagination flags](wasm.md#pagination-flags) for details of flags.
{% endhint %}

```bash
ununifid query wasm contract-state raw [bech32_address] [key] [flags]
ununifid query wasm contract-state smart [bech32_address] [query] [flags]
```

**Flags:**

{% hint style="info" %}
Please refer to [Common flags](wasm.md#common-query-flags) & [Encode flags](wasm.md#encode-flags) for details of flags.
{% endhint %}

### ununifid query wasm libwasmvm-version <a id="libwasmvm-version"></a>

Get libwasmvm version

```bash
ununifid query wasm libwasmvm-version [flags]
```

**Flags:**

{% hint style="info" %}
Please refer to [Common flags](wasm.md#common-query-flags) for details of flags.
{% endhint %}

### ununifid query wasm list-code <a id="list-code"></a>

List all wasm bytecode on the chain

```bash
ununifid query wasm list-code [flags]
```

**Flags:**

{% hint style="info" %}
Please refer to [Common flags](wasm.md#common-query-flags) & [Pagination flags](wasm.md#pagination-flags) for details of flags.
{% endhint %}

### ununifid query wasm list-contract-by-code <a id="list-contract-by-code"></a>

List wasm all bytecode on the chain for given code id

```bash
ununifid query wasm list-contract-by-code [code_id] [flags]
```

**Flags:**

{% hint style="info" %}
Please refer to [Common flags](wasm.md#common-query-flags) & [Pagination flags](wasm.md#pagination-flags) for details of flags.
{% endhint %}

### ununifid query wasm list-contracts-by-creator <a id="list-contracts-by-creator"></a>

List all contracts by creator

```bash
ununifid query wasm list-contracts-by-creator [creator] [flags]
```

**Flags:**

{% hint style="info" %}
Please refer to [Common flags](wasm.md#common-query-flags) & [Pagination flags](wasm.md#pagination-flags) for details of flags.
{% endhint %}

### ununifid query wasm params <a id="params"></a>

Query the current wasm parameters

```bash
ununifid query wasm params [flags]
```

**Flags:**

{% hint style="info" %}
Please refer to [Common flags](wasm.md#common-query-flags) for details of flags.
{% endhint %}

### ununifid query wasm pinned <a id="pinned"></a>

List all pinned code ids

```bash
ununifid query wasm pinned [flags]
```

**Flags:**

{% hint style="info" %}
Please refer to [Common flags](wasm.md#common-query-flags) & [Pagination flags](wasm.md#pagination-flags) for details of flags.
{% endhint %}

## Common flags in nftmint tx <a id="common-tx-flags"></a>

Common flags for the nftmint tx command are summarized.

**Flags:**

| Name, shorthand      | Type   | Required | Default               | Description                                                                                                                                                                                             |
| :------------------- | :----- | :------- | :-------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| -a, --account-number | uint   |          |                       | The account number of the signing account (offline mode only)                                                                                                                                           |
| --aux                |        |          |                       | Generate aux signer data instead of sending a tx                                                                                                                                                        |
| -b, --broadcast-mode | string |          | sync                  | Transaction broadcasting mode (sync \| async \| block)                                                                                                                                                  |
| --dry-run            |        |          |                       | ignore the --gas flag and perform a simulation of a transaction, but don't broadcast it (when enabled, the local Keybase is not accessible)                                                             |
| --fee-granter        | string |          |                       | Fee granter grants fees for the transaction                                                                                                                                                             |
| --fee-payer          | string |          |                       | Fee payer pays fees for the transaction instead of deducting from the signer                                                                                                                            |
| --fees               | string |          |                       | Fees to pay along with transaction; eg: 10uatom                                                                                                                                                         |
| --from               | string |          |                       | Name or address of private key with which to sign                                                                                                                                                       |
| --gas                | string |          | 200000                | gas limit to set per-transaction; set to "auto" to calculate sufficient gas automatically                                                                                                               |
| --gas-adjustment     | float  |          | 1                     | adjustment factor to be multiplied against the estimate returned by the tx simulation; if the gas limit is set manually this flag is ignored                                                            |
| --gas-prices         | string |          |                       | Gas prices in decimal format to determine the transaction fee (e.g. 0.1uatom)                                                                                                                           |
| --generate-only      |        |          |                       | Build an unsigned transaction and write it to STDOUT (when enabled, the local Keybase only accessed when providing a key name)                                                                          |
| -h, --help           |        |          |                       | help for \<module name>                                                                                                                                                                                 |
| --keyring-backend    | string |          | test                  | Select keyring's backend (os \| file \| kwallet \| pass \| test \| memory)                                                                                                                              |
| --keyring-dir        | string |          |                       | The client Keyring directory; if omitted, the default 'home' directory will be used                                                                                                                     |
| --ledger             |        |          |                       | Use a connected Ledger device                                                                                                                                                                           |
| --node               | string |          | tcp://localhost:26657 | \<host>:\<port> to tendermint rpc interface for this chain                                                                                                                                              |
| --note               | string |          |                       | Note to add a description to the transaction (previously --memo)                                                                                                                                        |
| --offline            |        |          |                       | Offline mode (does not allow any online functionality)                                                                                                                                                  |
| -o, --output         | string |          | json                  | Output format (text \| json)                                                                                                                                                                            |
| -s, --sequence       | uint   |          |                       | The sequence number of the signing account (offline mode only)                                                                                                                                          |
| --sign-mode          | string |          |                       | Choose sign mode (direct \| amino-json \| direct-aux), this is an advanced feature                                                                                                                      |
| --timeout-height     | uint   |          |                       | Set a block timeout height to prevent the tx from being committed past a certain height                                                                                                                 |
| --tip                | string |          |                       | Tip is the amount that is going to be transferred to the fee payer on the target chain. This flag is only valid when used with --aux, and is ignored if the target chain didn't enable the TipDecorator |
| -y, --yes            |        |          |                       | Skip tx broadcasting prompt confirmation                                                                                                                                                                |

**Global Flags:**

| Name, shorthand | Type   | Required | Default        | Description                                                                   |
| :-------------- | :----- | :------- | :------------- | :---------------------------------------------------------------------------- |
| --chain-id      | string |          |                | The network chain ID                                                          |
| --home          | string |          | $HOME/.ununifi | directory for config and data                                                 |
| --log_format    | string |          |                | The logging format (json \| plain) (default "plain")                          |
| --log_level     | string |          | info           | The logging level (trace \| debug \| info \| warn \| error \| fatal \| panic) |
| --trace         |        |          |                | print out full stack trace on errors                                          |

## Tx

### ununifid tx wasm clear-contract-admin <a id="clear-contract-admin"></a>

Clears admin for a contract to prevent further migrations

````bash
ununifid tx wasm clear-contract-admin [contract_addr_bech32] [flags]```
````

**Flags:**

{% hint style="info" %}
Please refer to [Common flags in cosmwasm tx](wasm.md#common-tx-flags) for details of flags.
{% endhint %}

### ununifid tx wasm execute <a id="execute"></a>

Execute a command on a wasm contract

```bash
ununifid tx wasm execute [contract_addr_bech32] [json_encoded_send_args] --amount [coins,optional] [flags]
```

**Flags:**

{% hint style="info" %}
Please refer to [Common flags in cosmwasm tx](wasm.md#common-tx-flags) for details of flags.
{% endhint %}

### ununifid tx wasm grant <a id="grant"></a>

Grant authorization to an address

```bash
ununifid tx wasm grant [grantee] [message_type="execution"|"migration"] [contract_addr_bech32] --allow-raw-msgs [msg1,msg2,...] --allow-msg-keys [key1,key2,...] --allow-all-messages [flags]
```

**Example:**

```bash
$ ununifid tx grant <grantee_addr> execution <contract_addr> --allow-all-messages --max-calls 1 --no-token-transfer --expiration 1667979596

$ ununifid tx grant <grantee_addr> execution <contract_addr> --allow-all-messages --max-funds 100000uwasm --expiration 1667979596

$ ununifid tx grant <grantee_addr> execution <contract_addr> --allow-all-messages --max-calls 5 --max-funds 100000uwasm --expiration 1667979596
```

**Flags:**

{% hint style="info" %}
Please refer to [Common flags in cosmwasm tx](wasm.md#common-tx-flags) for details of flags.
{% endhint %}

### ununifid tx wasm instantiate <a id="instantiate"></a>

Creates a new instance of an uploaded wasm code with the given 'constructor' message.
Each contract instance has a unique address assigned.

```bash
ununifid tx wasm instantiate [code_id_int64] [json_encoded_init_args] --label [text] --admin [address,optional] --amount [coins,optional]  [flags]
```

**Example:**

```bash
$ ununifid tx wasm instantiate 1 '{"foo":"bar"}' --admin="$(ununifid keys show mykey -a)" \
  --from mykey --amount="100ustake" --label "local0.1.0"
```

**Flags:**

{% hint style="info" %}
Please refer to [Common flags in cosmwasm tx](wasm.md#common-tx-flags) for details of flags.
{% endhint %}

### ununifid tx wasm instantiate2 <a id="instantiate2"></a>

Creates a new instance of an uploaded wasm code with the given 'constructor' message.
Each contract instance has a unique address assigned. They are assigned automatically but in order to have predictable addresses
for special use cases, the given 'salt' argument and '--fix-msg' parameters can be used to generate a custom address.

```bash
ununifid tx wasm instantiate2 [code_id_int64] [json_encoded_init_args] [salt] --label [text] --admin [address,optional] --amount [coins,optional] --fix-msg [bool,optional] [flags]
```

**Predictable address example (also see 'ununifid query wasm build-address -h'):**

```bash
$ ununifid tx wasm instantiate2 1 '{"foo":"bar"}' $(echo -n "testing" | xxd -ps) --admin="$(ununifid keys show mykey -a)" \
  --from mykey --amount="100ustake" --label "local0.1.0" \
   --fix-msg
```

**Flags:**

{% hint style="info" %}
Please refer to [Common flags in cosmwasm tx](wasm.md#common-tx-flags) for details of flags.
{% endhint %}

### ununifid tx wasm migrate <a id="migrate"></a>

Migrate a wasm contract to a new code version

```bash
ununifid tx wasm migrate [contract_addr_bech32] [new_code_id_int64] [json_encoded_migration_args] [flags]
```

**Flags:**

{% hint style="info" %}
Please refer to [Common flags in cosmwasm tx](wasm.md#common-tx-flags) for details of flags.
{% endhint %}

### ununifid tx wasm set-contract-admin <a id="set-contract-admin"></a>

Set new admin for a contract

```bash
ununifid tx wasm set-contract-admin [contract_addr_bech32] [new_admin_addr_bech32] [flags]
```

**Flags:**

{% hint style="info" %}
Please refer to [Common flags in cosmwasm tx](wasm.md#common-tx-flags) for details of flags.
{% endhint %}

### ununifid tx wasm store <a id="store"></a>

Upload a wasm binary

```bash
ununifid tx wasm store [wasm file] [flags]
```

**Flags:**

{% hint style="info" %}
Please refer to [Common flags in cosmwasm tx](wasm.md#common-tx-flags) for details of flags.
{% endhint %}

### ununifid tx wasm update-instantiate-config <a id="update-instantiate-config"></a>

Update instantiate config for a codeID

```bash
ununifid tx wasm update-instantiate-config [code_id_int64] [flags]
```

**Flags:**

{% hint style="info" %}
Please refer to [Common flags in cosmwasm tx](wasm.md#common-tx-flags) for details of flags.
{% endhint %}
