---
description: >-
  The nftmint module provides the feature to mint NFTs on UnUniFi. Users can mint collective NFTs by sending specific messages.
---

# nftmint

## Available Commands

**Query:**

| Name                                                              | Description                               |
| :---------------------------------------------------------------- | :---------------------------------------- |
| [class-attributes](nftmint.md#query-nftmint-class-attributes)     | Query the class attributes by class-id    |
| [class-ids-by-name](nftmint.md#query-nftmint-class-ids-by-name)   | Query classIDs which have the class name  |
| [class-ids-by-owner](nftmint.md#query-nftmint-class-ids-by-owner) | Query classIDs owned by the owner address |
| [nft-minter](nftmint.md#query-nftmint-nft-minter)                 | Query nft minter with class and nft id    |
| [params](nftmint.md#query-nftmint-params)                         | shows params                              |

**Tx:**

| Name                                                                     | Description                                                                                              |
| :----------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------- |
| [burn-nft](nftmint.md#tx-nftmint-burn-nft)                               | burn specified NFT                                                                                       |
| [create-class](nftmint.md#tx-nftmint-create-class)                       | create class for minting NFTs                                                                            |
| [mint-nft](nftmint.md#tx-nftmint-mint-nft)                               | mint NFT under specific class by class-id                                                                |
| [send-class](nftmint.md#tx-nftmint-send-class)                           | send the ownership of class                                                                              |
| [update-base-token-uri](nftmint.md#tx-nftmint-update-base-token-uri)     | update the base token uri of class specified by class id and automatically change the belonging nft uris |
| [update-token-supply-cap](nftmint.md#tx-nftmint-update-token-supply-cap) | update the token supply cap of class specified by class id                                               |

## Common flags in nftmint query <a id="common-query-flags"></a>

Common flags for the nftmint query command are summarized.

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

### ununifid query nftmint class-attributes <a id="query-nftmint-class-attributes"></a>

Query the class attributes by class-id.

```bash
ununifid query nftmint class-attributes [class-id] [flags]
```

**Flags:**

{% hint style="info" %}
Please refer to [Common flags in nftmint query](nftmint.md#common-query-flags) for details of flags.
{% endhint %}

### ununifid query nftmint class-ids-by-name <a id="query-nftmint-class-ids-by-name"></a>

Query classIDs which have the class name.

```bash
ununifid query nftmint class-ids-by-name [class-name] [flags]
```

**Flags:**

{% hint style="info" %}
Please refer to [Common flags in nftmint query](nftmint.md#common-query-flags) for details of flags.
{% endhint %}

### ununifid query nftmint class-ids-by-owner <a id="query-nftmint-class-ids-by-owner"></a>

Query classIDs owned by the owner address.

```bash
ununifid query nftmint class-ids-by-owner [owner-address] [flags]
```

**Flags:**

{% hint style="info" %}
Please refer to [Common flags in nftmint query](nftmint.md#common-query-flags) for details of flags.
{% endhint %}

### ununifid query nftmint nft-minter <a id="query-nftmint-nft-minter"></a>

Query nft minter with class and nft id.

```bash
ununifid query nftmint nft-minter [class-id] [nft-id] [flags]
```

**Flags:**

{% hint style="info" %}
Please refer to [Common flags in nftmint query](nftmint.md#common-query-flags) for details of flags.
{% endhint %}

### ununifid query nftmint params <a id="query-nftmint-params"></a>

shows params.

```bash
ununifid query nftmint params [flags]
```

**Flags:**

{% hint style="info" %}
Please refer to [Common flags in nftmint query](nftmint.md#common-query-flags) for details of flags.
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

### ununifid tx nftmint burn-nft <a id="tx-nftmint-burn-nft"></a>

burn specified NFT.

```bash
ununifid tx nftmint burn-nft [class-id] [nft-id] --from [sender] [flags]
```

**Flags:**

{% hint style="info" %}
Please refer to [Common flags in nftmint tx](nftmint.md#common-tx-flags) for details of flags.
{% endhint %}

### ununifid tx nftmint create-class <a id="tx-nftmint-create-class"></a>

create class for minting NFTs.

```bash
ununifid tx nftmint create-class [class-name] [base-token-uri]] [token-supply-cap] [minting-permission] --from [sender] [flags]
```

**Flags:**

| Name, shorthand | Type   | Required | Default | Description           |
| :-------------- | :----- | :------- | :------ | :-------------------- |
| --class-uri     | string |          |         | Content URI for class |
| --description   | string |          |         | Description for denom |

{% hint style="info" %}
Please refer to [Common flags in nftmint tx](nftmint.md#common-tx-flags) for details of flags.
{% endhint %}

### ununifid tx nftmint mint-nft <a id="tx-nftmint-mint-nft"></a>

mint NFT under specific class by class-id.

```bash
ununifid tx nftmint mint-nft [class-id] [nft-id] [receiver] --from [sender] [flags]
```

**Flags:**

{% hint style="info" %}
Please refer to [Common flags in nftmint tx](nftmint.md#common-tx-flags) for details of flags.
{% endhint %}

### ununifid tx nftmint send-class <a id="tx-nftmint-send-class"></a>

send the ownership of class.

```bash
ununifid tx nftmint send-class [class-id] [recipient] --from [sender] [flags]
```

**Flags:**

{% hint style="info" %}
Please refer to [Common flags in nftmint tx](nftmint.md#common-tx-flags) for details of flags.
{% endhint %}

### ununifid tx nftmint update-base-token-uri <a id="tx-nftmint-update-base-token-uri"></a>

update the base token uri of class specified by class id and automatically change the belonging nft uris.

```bash
ununifid tx nftmint update-base-token-uri [class-id] [base-token-uri] --from [sender] [flags]
```

**Flags:**

{% hint style="info" %}
Please refer to [Common flags in nftmint tx](nftmint.md#common-tx-flags) for details of flags.
{% endhint %}

### ununifid tx nftmint update-token-supply-cap <a id="tx-nftmint-update-token-supply-cap"></a>

update the token supply cap of class specified by class id.

```bash
ununifid tx nftmint update-token-supply-cap [class-id] [token-supply-cap] --from [sender] [flags]
```

**Flags:**

{% hint style="info" %}
Please refer to [Common flags in nftmint tx](nftmint.md#common-tx-flags) for details of flags.
{% endhint %}
