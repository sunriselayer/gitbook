---
description: >-
  The `nftbackedloan` module allows you to borrow tokens with NFTs as collateral. Also, can also lend tokens to NFT owners and earn interest.
---

# `nftbackedloan`

## Available Commands

**Query:**

  | Name                                            | Description                                       |
  | :---------------------------------------------- | :------------------------------------------------ |
  | [bidder_bids](nftbackedloan.md#query-bidder_bids)   | shows bids by bidder                              |
  | [cdp_list](nftbackedloan.md#query-cdp_list)         | shows cdps                                        |
  | [liquidation](nftbackedloan.md#query-liquidation)   | shows liquidation date                            |
  | [listed_class](nftbackedloan.md#query-listed_class) | shows listed nft ids and uris in defined class-id |
  | [listed_nfts](nftbackedloan.md#query-listed_nfts)   | shows listed nfts on the market                   |
  | [loan](nftbackedloan.md#query-loan)                 | shows nft loan                                    |
  | [loans](nftbackedloan.md#query-loans)               | shows loans                                       |
  | [nft_bids](nftbackedloan.md#query-nft_bids)         | shows nft bids                                    |
  | [nft_listing](nftbackedloan.md#query-nft_listing)   | shows nft listing                                 |
  | [params](nftbackedloan.md#query-params)             | shows params                                      |
  | [rewards](nftbackedloan.md#query-rewards)           | shows rewards of an address                       |

**Tx:**

  | Name                                                 | Description                        |
  | :--------------------------------------------------- | :--------------------------------- |
  | [borrow](nftbackedloan.md#tx-borrow)                     | borrow denom                       |
  | [cancel_listing](nftbackedloan.md#tx-cancel_listing)     | Cancel nft listing                 |
  | [cancelbid](nftbackedloan.md#tx-cancelbid)               | Cancel bid on nft                  |
  | [endlisting](nftbackedloan.md#tx-endlisting)             | end listing                        |
  | [listing](nftbackedloan.md#tx-listing)                   | Creates a new listing              |
  | [mint](nftbackedloan.md#tx-mint)                         | Mint an nft                        |
  | [pay_fullbid](nftbackedloan.md#tx-pay_fullbid)           | Pay full bid on nft                |
  | [placebid](nftbackedloan.md#tx-placebid)                 | Creates a new place bid            |
  | [repay](nftbackedloan.md#tx-repay)                       | repay loan on nft                  |
  | [selling_decision](nftbackedloan.md#tx-selling_decision) | broadcast selling decision message |

## Common flags in nftbackedloan query <a id="common-query-flags"></a>

Common flags for the `nftbackedloan` query command are summarized.

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

### ununifid query nftbackedloan bidder_bids <a id="query-cdp_list"></a>

shows bids by bidder.

```bash
ununifid query nftbackedloan bidder_bids [bidder] [flags]
```

**Flags:**

{% hint style="info" %}
Please refer to [Common flags in nftbackedloan query](nftbackedloan.md#common-query-flags) for details of flags.
{% endhint %}

### ununifid query nftbackedloan cdp_list <a id="query-cdp_list"></a>

shows cdps.

```bash
ununifid query nftbackedloan cdp_list [flags]
```

**Flags:**

{% hint style="info" %}
Please refer to [Common flags in nftbackedloan query](nftbackedloan.md#common-query-flags) for details of flags.
{% endhint %}

### ununifid query nftbackedloan liquidation <a id="query-liquidation"></a>

shows liquidation date.

```bash
ununifid query nftbackedloan liquidation [class-id] [nft-id] [flags]
```

**Flags:**

{% hint style="info" %}
Please refer to [Common flags in nftbackedloan query](nftbackedloan.md#common-query-flags) for details of flags.
{% endhint %}

### ununifid query nftbackedloan listed_class <a id="query-listed_class"></a>

shows listed nft ids and uris in defined class-id.

```bash
ununifid query nftbackedloan listed_class [class-id] [nft-limit] [flags]
```

**Flags:**

{% hint style="info" %}
Please refer to [Common flags in nftbackedloan query](nftbackedloan.md#common-query-flags) for details of flags.
{% endhint %}

### ununifid query nftbackedloan listed_nfts <a id="query-listed_nfts"></a>

shows listed nfts on the market.

```bash
ununifid query nftbackedloan listed_nfts [flags]
```

**Flags:**

| Name, shorthand | Type   | Required | Default | Description       |
| :-------------- | :----- | :------- | :------ | :---------------- |
| --owner         | string |          |         | nft owner address |

{% hint style="info" %}
Please refer to [Common flags in nftbackedloan query](nftbackedloan.md#common-query-flags) for details of flags.
{% endhint %}

### ununifid query nftbackedloan loan <a id="query-loan"></a>

shows nft loan.

```bash
ununifid query nftbackedloan loan [class-id] [nft-id] [flags]
```

**Flags:**

{% hint style="info" %}
Please refer to [Common flags in nftbackedloan query](nftbackedloan.md#common-query-flags) for details of flags.
{% endhint %}

### ununifid query nftbackedloan loans <a id="query-loans"></a>

shows loans.

```bash
ununifid query nftbackedloan loans [flags]
```

**Flags:**

{% hint style="info" %}
Please refer to [Common flags in nftbackedloan query](nftbackedloan.md#common-query-flags) for details of flags.
{% endhint %}

### ununifid query nftbackedloan nft_bids <a id="query-nft_bids"></a>

shows nft bids.

```bash
ununifid query nftbackedloan nft_bids [class_id] [nft_id] [flags]
```

**Flags:**

{% hint style="info" %}
Please refer to [Common flags in nftbackedloan query](nftbackedloan.md#common-query-flags) for details of flags.
{% endhint %}

### ununifid query nftbackedloan nft_listing <a id="query-nft_listing"></a>

shows nft listing.

```bash
ununifid query nftbackedloan nft_listing [class_id] [nft_id] [flags]
```

**Flags:**

{% hint style="info" %}
Please refer to [Common flags in nftbackedloan query](nftbackedloan.md#common-query-flags) for details of flags.
{% endhint %}

### ununifid query nftbackedloan params <a id="query-params"></a>

shows params.

```bash
ununifid query nftbackedloan params [flags]
```

**Flags:**

{% hint style="info" %}
Please refer to [Common flags in nftbackedloan query](nftbackedloan.md#common-query-flags) for details of flags.
{% endhint %}

### ununifid query nftbackedloan rewards <a id="query-rewards"></a>

shows rewards of an address.

```bash
ununifid query nftbackedloan rewards [address] [flags]
```

**Flags:**

{% hint style="info" %}
Please refer to [Common flags in nftbackedloan query](nftbackedloan.md#common-query-flags) for details of flags.
{% endhint %}

## Common flags in nftbackedloan tx <a id="common-tx-flags"></a>

Common flags for the nftbackedloan tx command are summarized.

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

### ununifid tx nftbackedloan borrow <a id="tx-borrow"></a>

borrow denom.

```bash
ununifid tx nftbackedloan borrow [class-id] [nft-id] [amount] [flags]
```

**Flags:**

{% hint style="info" %}
Please refer to [Common flags in nftbackedloan tx](nftbackedloan.md#common-tx-flags) for details of flags.
{% endhint %}

### ununifid tx nftbackedloan cancel_listing <a id="tx-cancel_listing"></a>

Cancel nft listing.

```bash
ununifid tx nftbackedloan cancel_listing [class-id] [nft-id] [flags]
```

**Flags:**

{% hint style="info" %}
Please refer to [Common flags in nftbackedloan tx](nftbackedloan.md#common-tx-flags) for details of flags.
{% endhint %}

### ununifid tx nftbackedloan cancelbid <a id="tx-cancelbid"></a>

Cancel bid on nft.

```bash
ununifid tx nftbackedloan cancelbid [class-id] [nft-id] [flags]
```

**Flags:**

{% hint style="info" %}
Please refer to [Common flags in nftbackedloan tx](nftbackedloan.md#common-tx-flags) for details of flags.
{% endhint %}

### ununifid tx nftbackedloan endlisting <a id="tx-endlisting"></a>

end listing.

```bash
ununifid tx nftbackedloan endlisting [class-id] [nft-id] [flags]
```

**Flags:**

{% hint style="info" %}
Please refer to [Common flags in nftbackedloan tx](nftbackedloan.md#common-tx-flags) for details of flags.
{% endhint %}

### ununifid tx nftbackedloan listing <a id="tx-listing"></a>

Creates a new listing.

```bash
ununifid tx nftbackedloan listing [class-id] [nft-id] [flags]
```

**Flags:**

| Name, shorthand   | Type   | Required | Default | Description     |
| :---------------- | :----- | :------- | :------ | :-------------- |
| --bid-active-rank | uint   | 1        |         | bid active rank |
| --bid-token       | string | uguu     |         | bid token       |
| --min-bid         | uint   | 1        |         | min bid amount  |

{% hint style="info" %}
Please refer to [Common flags in nftbackedloan tx](nftbackedloan.md#common-tx-flags) for details of flags.
{% endhint %}

### ununifid tx nftbackedloan mint <a id="tx-mint"></a>

Mint an nft.

```bash
ununifid tx nftbackedloan mint [class-id] [nft-id] [uri] [uri-hash] [flags]
```

**Flags:**

{% hint style="info" %}
Please refer to [Common flags in nftbackedloan tx](nftbackedloan.md#common-tx-flags) for details of flags.
{% endhint %}

### ununifid tx nftbackedloan pay_fullbid <a id="tx-pay_fullbid"></a>

Pay full bid on nft.

```bash
ununifid tx nftbackedloan pay_fullbid [class-id] [nft-id] [flags]
```

**Flags:**

{% hint style="info" %}
Please refer to [Common flags in nftbackedloan tx](nftbackedloan.md#common-tx-flags) for details of flags.
{% endhint %}

### ununifid tx nftbackedloan placebid <a id="tx-placebid"></a>

Creates a new place bid.

```bash
ununifid tx nftbackedloan placebid [class-id] [nft-id] [amount] [flags]
```

**Flags:**

| Name, shorthand         | Type | Required | Default | Description        |
| :---------------------- | :--- | :------- | :------ | :----------------- |
| -p, --automatic-payment |      |          |         | automation payment |

{% hint style="info" %}
Please refer to [Common flags in nftbackedloan tx](nftbackedloan.md#common-tx-flags) for details of flags.
{% endhint %}

### ununifid tx nftbackedloan repay <a id="tx-repay"></a>

repay loan on nft.

```bash
ununifid tx nftbackedloan repay [class-id] [nft-id] [amount] [flags]
```

**Flags:**

{% hint style="info" %}
Please refer to [Common flags in nftbackedloan tx](nftbackedloan.md#common-tx-flags) for details of flags.
{% endhint %}

### ununifid tx nftbackedloan selling_decision <a id="tx-selling_decision"></a>

broadcast selling decision message.

```bash
ununifid tx nftbackedloan selling_decision [class-id] [nft-id] [flags]
```

**Flags:**

{% hint style="info" %}
Please refer to [Common flags in nftbackedloan tx](nftbackedloan.md#common-tx-flags) for details of flags.
{% endhint %}
