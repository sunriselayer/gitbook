---
description: >-
  The `yieldaggregator` module allows you to manage assets and earn yield.
---

# `yieldaggregator`

**Query:**

| Name                                                     | Description                        |
| :------------------------------------------------------- | :--------------------------------- |
| [list-vault](yieldaggregator.md#query-list-vault)       | list all vault                     |
| [show-vault](yieldaggregator.md#query-show-vault)       | shows a vault                      |
| [list-strategy](yieldaggregator.md#query-list-strategy) | list all strategies                |
| [show-strategy](yieldaggregator.md#query-show-strategy) | shows a strategy                   |
| [params](yieldaggregator.md#query-params)               | shows the parameters of the module |

**Tx:**

| Name                                                                        | Description                         |
| :-------------------------------------------------------------------------- | :---------------------------------- |
| [create-vault](yieldaggregator.md#tx-create-vault)                         | create a new vault                  |
| [delete-vault](yieldaggregator.md#tx-delete-vault)                         | delete the vault                    |
| [transfer-vault-ownership](yieldaggregator.md#tx-transfer-vault-ownership) | transfer the ownership of a vault   |
| [deposit-to-vault](yieldaggregator.md#tx-deposit-to-vault)                 | deposit to the vault                |
| [withdraw-from-vault](yieldaggregator.md#tx-withdraw-from-vault)           | withdraw from the vault             |
| [proposal-add-strategy](yieldaggregator.md#tx-proposal-add-strategy)       | Submit a proposal to add a strategy |

## Common flags in yieldaggregator query <a id="common-query-flags"></a>

Common flags for the `yieldaggregator` query command are summarized.

**Flags:**

| Name, shorthand | Type   | Required | Default               | Description                                                                           |
| :-------------- | :----- | :------- | :-------------------- | :------------------------------------------------------------------------------------ |
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

## Query

### ununifid query yieldaggregator list-vault <a id="query-list-vault"></a>

list all vaults.

```bash
ununifid query yieldaggregator list-vault [flags]
```

**Flags:**

{% hint style="info" %}
Please refer to [Common flags in yieldaggregator query](yieldaggregator.md#common-query-flags) for details of flags.
{% endhint %}

### ununifid query yieldaggregator show-vault <a id="query-show-vault"></a>

shows a vault.

```bash
ununifid query yieldaggregator show-vault [vault-id] [flags]
```

**Flags:**

{% hint style="info" %}
Please refer to [Common flags in yieldaggregator query](yieldaggregator.md#common-query-flags) for details of flags.
{% endhint %}

### ununifid query yieldaggregator list-strategy <a id="query-list-strategy"></a>

list all strategies.

```bash
ununifid query yieldaggregator list-strategy [vault-denom] [flags]
```

**Flags:**

{% hint style="info" %}
Please refer to [Common flags in yieldaggregator query](yieldaggregator.md#common-query-flags) for details of flags.
{% endhint %}

### ununifid query yieldaggregator show-strategy <a id="query-show-strategy"></a>

shows a strategy.

```bash
ununifid query yieldaggregator show-strategy [vault-denom] [strategy-id] [flags]
```

**Flags:**

{% hint style="info" %}
Please refer to [Common flags in yieldaggregator query](yieldaggregator.md#common-query-flags) for details of flags.
{% endhint %}

### ununifid query yieldaggregator params <a id="query-params"></a>

shows the parameters of the module

```bash
ununifid query yieldaggregator params [flags]
```

**Flags:**

{% hint style="info" %}
Please refer to [Common flags in yieldaggregator query](yieldaggregator.md#common-query-flags) for details of flags.
{% endhint %}

## Common flags in yieldaggregator tx <a id="common-tx-flags"></a>

Common flags for the yieldaggregator tx command are summarized.

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

### ununifid tx yieldaggregator create-vault <a id="tx-create-vault"></a>

create a new vault.

```bash
ununifid tx yieldaggregator create-vault [denom] [commission-rate] [withdraw-reserve-rate] [fee] [deposit] [strategyWeights] [flags]
```

**Flags:**

{% hint style="info" %}
Please refer to [Common flags in yieldaggregator tx](yieldaggregator.md#common-tx-flags) for details of flags.
{% endhint %}

### ununifid tx yieldaggregator delete-vault <a id="tx-delete-vault"></a>

delete the vault.

```bash
ununifid tx yieldaggregator delete-vault [id] [flags]
```

**Flags:**

{% hint style="info" %}
Please refer to [Common flags in yieldaggregator tx](yieldaggregator.md#common-tx-flags) for details of flags.
{% endhint %}

### ununifid tx yieldaggregator transfer-vault-ownership <a id="tx-transfer-vault-ownership"></a>

transfer the ownership of a vault.

```bash
ununifid tx yieldaggregator transfer-vault-ownership [id] [recipient] [flags]
```

**Flags:**

{% hint style="info" %}
Please refer to [Common flags in yieldaggregator tx](yieldaggregator.md#common-tx-flags) for details of flags.
{% endhint %}

### ununifid tx yieldaggregator deposit-to-vault <a id="tx-deposit-to-vault"></a>

deposit to the vault.

```bash
ununifid tx yieldaggregator deposit-to-vault [id] [principal-amount] [flags]
```

**Flags:**

{% hint style="info" %}
Please refer to [Common flags in yieldaggregator tx](yieldaggregator.md#common-tx-flags) for details of flags.
{% endhint %}

### ununifid tx yieldaggregator withdraw-from-vault <a id="tx-withdraw-from-vault"></a>

withdraw from the vault.

```bash
ununifid tx yieldaggregator withdraw-from-vault [id] [vault-token-amount] [flags]
```

**Flags:**

{% hint style="info" %}
Please refer to [Common flags in yieldaggregator tx](yieldaggregator.md#common-tx-flags) for details of flags.
{% endhint %}

### ununifid tx yieldaggregator proposal-add-strategy <a id="tx-proposal-add-strategy"></a>

Submit a proposal to add a strategy.

```bash
ununifid tx yieldaggregator proposal-add-strategy [flags]
```

**Flags:**

{% hint style="info" %}
Please refer to [Common flags in yieldaggregator tx](yieldaggregator.md#common-tx-flags) for details of flags.
{% endhint %}
