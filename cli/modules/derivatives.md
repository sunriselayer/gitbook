---
description: >-
  The derivatives module allows you to manage assets through derivatives.
---

# derivatives

**Query:**

| Name                                                    | Description                                                                 |
| :------------------------------------------------------ | :-------------------------------------------------------------------------- |
| [positions](derivatives.md#query-positions)             | shows the positions owned by the designated address                         |
| [available-assets](derivatives.md#query-assets)         | shows the available amount of all assets in the pool                        |
| [available-asset](derivatives.md#query-asset)           | shows the available amount of the asset                                     |
| [lpt-nominal-apy](derivatives.md#query-lpt-nominal-apy) | shows the nominal Annual Percent Yield between beforeHeight and afterHeight |
| [lpt-real-apy](derivatives.md#query-lpt-real-apy)       | shows the real Annual Percent Yield between beforeHeight and afterHeight    |
| [params](derivatives.md#query-params)                   | shows the parameters of the module                                          |

**Tx:**

| Name                                                       | Description                            |
| :--------------------------------------------------------- | :------------------------------------- |
| [open-position](derivatives.md#tx-open-position)           | derivatives open position subcommands  |
| [close-position](derivatives.md#tx-close-position)         | derivatives close position subcommands |
| [report-liquidation](derivatives.md#tx-report-liquidation) | report liquidation needed position     |
| [report-levy-period](derivatives.md#tx-report-levy-period) | report levy needed position            |
| [deposit-to-pool](derivatives.md#tx-deposit-to-pool)       | deposit to pool                        |
| [withdraw-from-pool](derivatives.md#tx-withdraw-from-pool) | withdraw from pool                     |

## Common flags in derivatives query <a id="common-query-flags"></a>

Common flags for the derivatives query command are summarized.

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

### ununifid query derivatives positions <a id="query-positions"></a>

shows the positions owned by the designated address.

```bash
ununifid query derivatives positions [address] [flags]
```

**Flags:**

{% hint style="info" %}
Please refer to [Common flags in derivatives query](derivatives.md#common-query-flags) for details of flags.
{% endhint %}

### ununifid query derivatives available-assets <a id="query-available-assets"></a>

shows the available amount of all assets in the pool.

```bash
ununifid query derivatives available-assets [flags]
```

**Flags:**

{% hint style="info" %}
Please refer to [Common flags in derivatives query](derivatives.md#common-query-flags) for details of flags.
{% endhint %}

### ununifid query derivatives available-asset <a id="query-available-asset"></a>

shows the available amount of the asset.

```bash
ununifid query derivatives available-asset [denom] [flags]
```

**Flags:**

{% hint style="info" %}
Please refer to [Common flags in derivatives query](derivatives.md#common-query-flags) for details of flags.
{% endhint %}

### ununifid query derivatives lpt-nominal-apy <a id="query-lpt-nominal-apy"></a>

shows the nominal Annual Percent Yield between beforeHeight and afterHeight.

```bash
ununifid query derivatives lpt-nominal-apy [beforeHeight] [afterHeight] [flags]
```

**Flags:**

{% hint style="info" %}
Please refer to [Common flags in derivatives query](derivatives.md#common-query-flags) for details of flags.
{% endhint %}

### ununifid query derivatives lpt-real-apy <a id="query-lpt-real-apy"></a>

shows the real Annual Percent Yield between beforeHeight and afterHeight.

```bash
ununifid query derivatives lpt-real-apy [beforeHeight] [afterHeight] [flags]
```

**Flags:**

{% hint style="info" %}
Please refer to [Common flags in derivatives query](derivatives.md#common-query-flags) for details of flags.
{% endhint %}

### ununifid query derivatives params <a id="query-params"></a>

shows the parameters of the module.

```bash
ununifid query derivatives params [flags]
```

**Flags:**

{% hint style="info" %}
Please refer to [Common flags in derivatives query](derivatives.md#common-query-flags) for details of flags.
{% endhint %}

## Common flags in derivatives tx <a id="common-tx-flags"></a>

Common flags for the derivatives tx command are summarized.

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

### ununifid tx derivatives open-position <a id="tx-open-position"></a>

derivatives open position.

```bash
ununifid tx derivatives open-position [command]
```

**Command:**

| Name, shorthand | Type | Required | Default | Description |
| :---------------------- | :--- | :------- | :------ | :----------------- |
| perpetual-futures | | | | open perpetual futures position |

```bash
ununifid tx derivatives open-position perpetual-futures [margin] [base-denom] [quote-denom] [long/short] [position-size] [leverage] [flags]
```

**Flags:**

{% hint style="info" %}
Please refer to [Common flags in derivatives tx](derivatives.md#common-tx-flags) for details of flags.
{% endhint %}

### ununifid tx derivatives close-position <a id="tx-close-position"></a>

derivatives close position.

```bash
ununifid tx derivatives close-position [position-id] [flags]
```

**Flags:**

{% hint style="info" %}
Please refer to [Common flags in derivatives tx](derivatives.md#common-tx-flags) for details of flags.
{% endhint %}

### ununifid tx derivatives report-liquidation <a id="tx-report-liquidation"></a>

report liquidation needed position.

```bash
ununifid tx derivatives report-liquidation [position-id] [reward-recipient] [flags]
```

**Flags:**

{% hint style="info" %}
Please refer to [Common flags in derivatives tx](derivatives.md#common-tx-flags) for details of flags.
{% endhint %}

### ununifid tx derivatives report-levy-period <a id="tx-report-levy-period"></a>

report levy needed position.

```bash
ununifid tx derivatives report-levy-period [position-id] [reward-recipient] [flags]
```

**Flags:**

{% hint style="info" %}
Please refer to [Common flags in derivatives tx](derivatives.md#common-tx-flags) for details of flags.
{% endhint %}

### ununifid tx derivatives deposit-to-pool <a id="tx-deposit-to-pool"></a>

deposit to pool.

```bash
ununifid tx derivatives deposit-to-pool [amount] [flags]
```

**Flags:**

{% hint style="info" %}
Please refer to [Common flags in derivatives tx](derivatives.md#common-tx-flags) for details of flags.
{% endhint %}

### ununifid tx derivatives withdraw-from-pool <a id="tx-withdraw-from-pool"></a>

withdraw from pool.

```bash
ununifid tx derivatives withdraw-from-pool [amount] [redeem-denom] [flags]
```

**Flags:**

{% hint style="info" %}
Please refer to [Common flags in derivatives tx](derivatives.md#common-tx-flags) for details of flags.
{% endhint %}
