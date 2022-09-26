---
description: >-
  nfsmarket module allows you to manage assets for accounts loaded into the local
  keys module
---

# nfsmarket

## Available Commands

| Name | Description |
| :--- | :--- |
| [cdp_list](nftmarket.md#query-cdp_list)                  | shows cdps |
| [listed_class](nftmarket.md#query-listed_class)          | shows listed nft ids and uris in defined class-id |
| [listed_nfts](nftmarket.md#query-listed_nfts)            | shows listed nfts on the market |
| [loan](nftmarket.md#query-loan)                          | shows nft loan |
| [loans](nftmarket.md#query-loans)                        | shows loans |
| [nft_bids](nftmarket.md#query-nft_bids)                  | shows nft bids |
| [nft_listing](nftmarket.md#query-nft_listing)            | shows nft listing |
| [params](nftmarket.md#query-params)                      | shows params |
| [rewards](nftmarket.md#query-rewards)                    | shows rewards of an address |
| [borrow](nftmarket.md#tx-borrow)                         | borrow denom |
| [burn_stablecoin](nftmarket.md#tx-burn_stablecoin)       | burn stablecoin |
| [cancel_listing](nftmarket.md#tx-cancel_listing)         | Cancel nft listing |
| [cancelbid](nftmarket.md#tx-cancelbid)                   | Cancel bid on nft |
| [endlisting](nftmarket.md#tx-endlisting)                 | end listing |
| [expand_nft_listing](nftmarket.md#tx-expand_nft_listing) | Expand nft listing |
| [liquidate](nftmarket.md#tx-liquidate)                   | liquidate |
| [listing](nftmarket.md#tx-listing)                       | Creates a new listing |
| [mint](nftmarket.md#tx-mint)                             | Mint an nft |
| [mint_stablecoin](nftmarket.md#tx-mint_stablecoin)       | mint stablecoin |
| [pay_fullbid](nftmarket.md#tx-pay_fullbid)               | Pay full bid on nft |
| [placebid](nftmarket.md#tx-placebid)                     | Creates a new place bid |
| [repay](nftmarket.md#tx-repay)                           | repay loan on nft |
| [selling_decision](nftmarket.md#tx-selling_decision)     | broadcast selling decision message |


| [cdp_list](nftmarket.md#query-cdp_list)                  | shows cdps |
### ununifid query nftmarket cdp_list <a id="query-cdp_list"></a>

shows cdps.

```text
ununifid query nftmarket cdp_list [flags]
```

**Flags:**

| Name, shorthand  | Type   | Required | Default                 | Description |
| :--------------- | :----- | :------- | :---------------------- | :---------- |
| --height         | int    |          |                         | Use a specific height to query state at (this can error if the node is pruning state) |
| -h, --help       |        |          |                         | Help for cdp_list |
| --node           | string |          | tcp://localhost:26657   | \<host>:\<port> to Tendermint RPC interface for this chain |
| -o, --output     | string |          | text                    | Output format (text \| json) |
| --chain-id       | string |          |                         | The network chain ID |
| --home           | string |          | $HOME/.ununifi          | directory for config and data |
| --log\_format    | string |          |                         | The logging format (json \| plain) (default "plain") |
| --log\_level     | string |          | info                    | The logging level (trace \| debug \| info \| warn \| error \| fatal \| panic) |
| --trace          |        |          |                         | print out full stack trace on errors |


### ununifid query nftmarket listed_class <a id="query-listed_class"></a>

shows listed nft ids and uris in defined class-id.

```text
ununifid query nftmarket listed_class [class-id] [nft-limit] [flags]
```

**Flags:**

| Name, shorthand  | Type   | Required | Default                 | Description |
| :--------------- | :----- | :------- | :---------------------- | :---------- |
| --height         | int    |          |                         | Use a specific height to query state at (this can error if the node is pruning state) |
| -h, --help       |        |          |                         | Help for cdp_list |
| --node           | string |          | tcp://localhost:26657   | \<host>:\<port> to Tendermint RPC interface for this chain |
| -o, --output     | string |          | text                    | Output format (text \| json) |
| --chain-id       | string |          |                         | The network chain ID |
| --home           | string |          | $HOME/.ununifi          | directory for config and data |
| --log\_format    | string |          |                         | The logging format (json \| plain) (default "plain") |
| --log\_level     | string |          | info                    | The logging level (trace \| debug \| info \| warn \| error \| fatal \| panic) |
| --trace          |        |          |                         | print out full stack trace on errors |


### ununifid query nftmarket listed_nfts <a id="query-listed_nfts"></a>

shows listed nfts on the market.

```text
ununifid query nftmarket listed_nfts [flags]
```

**Flags:**

| Name, shorthand  | Type   | Required | Default                 | Description |
| :--------------- | :----- | :------- | :---------------------- | :---------- |
| --height         | int    |          |                         | Use a specific height to query state at (this can error if the node is pruning state) |
| -h, --help       |        |          |                         | Help for cdp_list |
| --node           | string |          | tcp://localhost:26657   | \<host>:\<port> to Tendermint RPC interface for this chain |
| -o, --output     | string |          | text                    | Output format (text \| json) |
| --owner          | string |          |                         | nft owner address |
| --chain-id       | string |          |                         | The network chain ID |
| --home           | string |          | $HOME/.ununifi          | directory for config and data |
| --log\_format    | string |          |                         | The logging format (json \| plain) (default "plain") |
| --log\_level     | string |          | info                    | The logging level (trace \| debug \| info \| warn \| error \| fatal \| panic) |
| --trace          |        |          |                         | print out full stack trace on errors |


### ununifid query nftmarket loan <a id="query-loan"></a>

shows nft loan.

```text
ununifid query nftmarket loan [class-id] [nft-id] [flags]
```

**Flags:**

| Name, shorthand  | Type   | Required | Default                 | Description |
| :--------------- | :----- | :------- | :---------------------- | :---------- |
| --height         | int    |          |                         | Use a specific height to query state at (this can error if the node is pruning state) |
| -h, --help       |        |          |                         | Help for cdp_list |
| --node           | string |          | tcp://localhost:26657   | \<host>:\<port> to Tendermint RPC interface for this chain |
| -o, --output     | string |          | text                    | Output format (text \| json) |
| --chain-id       | string |          |                         | The network chain ID |
| --home           | string |          | $HOME/.ununifi          | directory for config and data |
| --log\_format    | string |          |                         | The logging format (json \| plain) (default "plain") |
| --log\_level     | string |          | info                    | The logging level (trace \| debug \| info \| warn \| error \| fatal \| panic) |
| --trace          |        |          |                         | print out full stack trace on errors |


### ununifid query nftmarket loans <a id="query-loans"></a>

shows loans.

```text
ununifid query nftmarket loans [flags]
```

**Flags:**

| Name, shorthand  | Type   | Required | Default                 | Description |
| :--------------- | :----- | :------- | :---------------------- | :---------- |
| --height         | int    |          |                         | Use a specific height to query state at (this can error if the node is pruning state) |
| -h, --help       |        |          |                         | Help for cdp_list |
| --node           | string |          | tcp://localhost:26657   | \<host>:\<port> to Tendermint RPC interface for this chain |
| -o, --output     | string |          | text                    | Output format (text \| json) |
| --chain-id       | string |          |                         | The network chain ID |
| --home           | string |          | $HOME/.ununifi          | directory for config and data |
| --log\_format    | string |          |                         | The logging format (json \| plain) (default "plain") |
| --log\_level     | string |          | info                    | The logging level (trace \| debug \| info \| warn \| error \| fatal \| panic) |
| --trace          |        |          |                         | print out full stack trace on errors |


### ununifid query nftmarket nft_bids <a id="query-nft_bids"></a>

shows nft bids.

```text
ununifid query nftmarket nft_bids [class_id] [nft_id] [flags]
```

**Flags:**

| Name, shorthand  | Type   | Required | Default                 | Description |
| :--------------- | :----- | :------- | :---------------------- | :---------- |
| --height         | int    |          |                         | Use a specific height to query state at (this can error if the node is pruning state) |
| -h, --help       |        |          |                         | Help for cdp_list |
| --node           | string |          | tcp://localhost:26657   | \<host>:\<port> to Tendermint RPC interface for this chain |
| -o, --output     | string |          | text                    | Output format (text \| json) |
| --chain-id       | string |          |                         | The network chain ID |
| --home           | string |          | $HOME/.ununifi          | directory for config and data |
| --log\_format    | string |          |                         | The logging format (json \| plain) (default "plain") |
| --log\_level     | string |          | info                    | The logging level (trace \| debug \| info \| warn \| error \| fatal \| panic) |
| --trace          |        |          |                         | print out full stack trace on errors |


### ununifid query nftmarket nft_listing <a id="query-nft_listing"></a>

shows nft listing.

```text
ununifid query nftmarket nft_listing [class_id] [nft_id] [flags]
```

**Flags:**

| Name, shorthand  | Type   | Required | Default                 | Description |
| :--------------- | :----- | :------- | :---------------------- | :---------- |
| --height         | int    |          |                         | Use a specific height to query state at (this can error if the node is pruning state) |
| -h, --help       |        |          |                         | Help for cdp_list |
| --node           | string |          | tcp://localhost:26657   | \<host>:\<port> to Tendermint RPC interface for this chain |
| -o, --output     | string |          | text                    | Output format (text \| json) |
| --chain-id       | string |          |                         | The network chain ID |
| --home           | string |          | $HOME/.ununifi          | directory for config and data |
| --log\_format    | string |          |                         | The logging format (json \| plain) (default "plain") |
| --log\_level     | string |          | info                    | The logging level (trace \| debug \| info \| warn \| error \| fatal \| panic) |
| --trace          |        |          |                         | print out full stack trace on errors |


### ununifid query nftmarket params <a id="query-params"></a>

shows params.

```text
ununifid query nftmarket params [flags]
```

**Flags:**

| Name, shorthand  | Type   | Required | Default                 | Description |
| :--------------- | :----- | :------- | :---------------------- | :---------- |
| --height         | int    |          |                         | Use a specific height to query state at (this can error if the node is pruning state) |
| -h, --help       |        |          |                         | Help for cdp_list |
| --node           | string |          | tcp://localhost:26657   | \<host>:\<port> to Tendermint RPC interface for this chain |
| -o, --output     | string |          | text                    | Output format (text \| json) |
| --chain-id       | string |          |                         | The network chain ID |
| --home           | string |          | $HOME/.ununifi          | directory for config and data |
| --log\_format    | string |          |                         | The logging format (json \| plain) (default "plain") |
| --log\_level     | string |          | info                    | The logging level (trace \| debug \| info \| warn \| error \| fatal \| panic) |
| --trace          |        |          |                         | print out full stack trace on errors |


| [rewards](nftmarket.md#query-rewards)                    | shows rewards of an address |
### ununifid query nftmarket rewards <a id="query-rewards"></a>

shows rewards of an address.

```text
ununifid query nftmarket rewards [address] [flags]
```

**Flags:**

| Name, shorthand  | Type   | Required | Default                 | Description |
| :--------------- | :----- | :------- | :---------------------- | :---------- |
| --height         | int    |          |                         | Use a specific height to query state at (this can error if the node is pruning state) |
| -h, --help       |        |          |                         | Help for cdp_list |
| --node           | string |          | tcp://localhost:26657   | \<host>:\<port> to Tendermint RPC interface for this chain |
| -o, --output     | string |          | text                    | Output format (text \| json) |
| --chain-id       | string |          |                         | The network chain ID |
| --home           | string |          | $HOME/.ununifi          | directory for config and data |
| --log\_format    | string |          |                         | The logging format (json \| plain) (default "plain") |
| --log\_level     | string |          | info                    | The logging level (trace \| debug \| info \| warn \| error \| fatal \| panic) |
| --trace          |        |          |                         | print out full stack trace on errors |


### ununifid tx nftmarket borrow <a id="tx-borrow"></a>

borrow denom.

```text
ununifid tx nftmarket borrow [class-id] [nft-id] [amount] [flags]
```

**Flags:**

| Name, shorthand      | Type   | Required | Default                 | Description |
| :------------------- | :----- | :------- | :---------------------- | :---------- |
| -a, --account-number | uint   |          |                         | The account number of the signing account (offline mode only) |
| --aux                |        |          |                         | Generate aux signer data instead of sending a tx |
| -b, --broadcast-mode | string |          | sync                    | Transaction broadcasting mode (sync \| async \| block) |
| --dry-run            |        |          |                         | ignore the --gas flag and perform a simulation of a transaction, but don't broadcast it (when enabled, the local Keybase is not accessible) |
| --fee-granter        | string |          |                         | Fee granter grants fees for the transaction |
| --fee-payer          | string |          |                         | Fee payer pays fees for the transaction instead of deducting from the signer |
| --fees               | string |          |                         | Fees to pay along with transaction; eg: 10uatom |
| --from               | string |          |                         | Name or address of private key with which to sign |
| --gas                | string |          | 200000                  | gas limit to set per-transaction; set to "auto" to calculate sufficient gas automatically |
| --gas-adjustment     | float  |          | 1                       | adjustment factor to be multiplied against the estimate returned by the tx simulation; if the gas limit is set manually this flag is ignored |
| --gas-prices         | string |          |                         | Gas prices in decimal format to determine the transaction fee (e.g. 0.1uatom) |
| --generate-only      |        |          |                         | Build an unsigned transaction and write it to STDOUT (when enabled, the local Keybase only accessed when providing a key name) |
| -h, --help           |        |          |                         | help for borrow |
| --keyring-backend    | string |          | test                    | Select keyring's backend (os \| file \| kwallet \| pass \| test \| memory) |
| --keyring-dir        | string |          |                         | The client Keyring directory; if omitted, the default 'home' directory will be used |
| --ledger             |        |          |                         | Use a connected Ledger device |
| --node               | string |          | tcp://localhost:26657   | \<host>:\<port> to tendermint rpc interface for this chain |
| --note               | string |          |                         | Note to add a description to the transaction (previously --memo) |
| --offline            |        |          |                         | Offline mode (does not allow any online functionality) |
| -o, --output         | string |          | json                    | Output format (text \| json) |
| -s, --sequence       | uint   |          |                         | The sequence number of the signing account (offline mode only) |
| --sign-mode          | string |          |                         | Choose sign mode (direct \| amino-json \| direct-aux), this is an advanced feature |
| --timeout-height     | uint   |          |                         | Set a block timeout height to prevent the tx from being committed past a certain height |
| --tip                | string |          |                         | Tip is the amount that is going to be transferred to the fee payer on the target chain. This flag is only valid when used with --aux, and is ignored if the target chain didn't enable the TipDecorator |
| -y, --yes            |        |          |                         | Skip tx broadcasting prompt confirmation |
| --chain-id           | string |          |                         | The network chain ID |
| --home               | string |          | $HOME/.ununifi          | directory for config and data |
| --log\_format        | string |          |                         | The logging format (json \| plain) (default "plain") |
| --log\_level         | string |          | info                    | The logging level (trace \| debug \| info \| warn \| error \| fatal \| panic) |
| --trace              |        |          |                         | print out full stack trace on errors |


### ununifid tx nftmarket burn_stablecoin <a id="tx-burn_stablecoin"></a>

burn stablecoin.

```text
ununifid tx nftmarket burn_stablecoin [class-id] [nft-id] [amount] [flags]
```

**Flags:**

| Name, shorthand      | Type   | Required | Default                 | Description |
| :------------------- | :----- | :------- | :---------------------- | :---------- |
| -a, --account-number | uint   |          |                         | The account number of the signing account (offline mode only) |
| --aux                |        |          |                         | Generate aux signer data instead of sending a tx |
| -b, --broadcast-mode | string |          | sync                    | Transaction broadcasting mode (sync \| async \| block) |
| --dry-run            |        |          |                         | ignore the --gas flag and perform a simulation of a transaction, but don't broadcast it (when enabled, the local Keybase is not accessible) |
| --fee-granter        | string |          |                         | Fee granter grants fees for the transaction |
| --fee-payer          | string |          |                         | Fee payer pays fees for the transaction instead of deducting from the signer |
| --fees               | string |          |                         | Fees to pay along with transaction; eg: 10uatom |
| --from               | string |          |                         | Name or address of private key with which to sign |
| --gas                | string |          | 200000                  | gas limit to set per-transaction; set to "auto" to calculate sufficient gas automatically |
| --gas-adjustment     | float  |          | 1                       | adjustment factor to be multiplied against the estimate returned by the tx simulation; if the gas limit is set manually this flag is ignored |
| --gas-prices         | string |          |                         | Gas prices in decimal format to determine the transaction fee (e.g. 0.1uatom) |
| --generate-only      |        |          |                         | Build an unsigned transaction and write it to STDOUT (when enabled, the local Keybase only accessed when providing a key name) |
| -h, --help           |        |          |                         | help for burn_stablecoin |
| --keyring-backend    | string |          | test                    | Select keyring's backend (os \| file \| kwallet \| pass \| test \| memory) |
| --keyring-dir        | string |          |                         | The client Keyring directory; if omitted, the default 'home' directory will be used |
| --ledger             |        |          |                         | Use a connected Ledger device |
| --node               | string |          | tcp://localhost:26657   | \<host>:\<port> to tendermint rpc interface for this chain |
| --note               | string |          |                         | Note to add a description to the transaction (previously --memo) |
| --offline            |        |          |                         | Offline mode (does not allow any online functionality) |
| -o, --output         | string |          | json                    | Output format (text \| json) |
| -s, --sequence       | uint   |          |                         | The sequence number of the signing account (offline mode only) |
| --sign-mode          | string |          |                         | Choose sign mode (direct \| amino-json \| direct-aux), this is an advanced feature |
| --timeout-height     | uint   |          |                         | Set a block timeout height to prevent the tx from being committed past a certain height |
| --tip                | string |          |                         | Tip is the amount that is going to be transferred to the fee payer on the target chain. This flag is only valid when used with --aux, and is ignored if the target chain didn't enable the TipDecorator |
| -y, --yes            |        |          |                         | Skip tx broadcasting prompt confirmation |
| --chain-id           | string |          |                         | The network chain ID |
| --home               | string |          | $HOME/.ununifi          | directory for config and data |
| --log\_format        | string |          |                         | The logging format (json \| plain) (default "plain") |
| --log\_level         | string |          | info                    | The logging level (trace \| debug \| info \| warn \| error \| fatal \| panic) |
| --trace              |        |          |                         | print out full stack trace on errors |

### ununifid tx nftmarket cancel_listing <a id="tx-cancel_listing"></a>

Cancel nft listing.

```text
ununifid tx nftmarket cancel_listing [class-id] [nft-id] [flags]
```

**Flags:**

| Name, shorthand      | Type   | Required | Default                 | Description |
| :------------------- | :----- | :------- | :---------------------- | :---------- |
| -a, --account-number | uint   |          |                         | The account number of the signing account (offline mode only) |
| --aux                |        |          |                         | Generate aux signer data instead of sending a tx |
| -b, --broadcast-mode | string |          | sync                    | Transaction broadcasting mode (sync \| async \| block) |
| --dry-run            |        |          |                         | ignore the --gas flag and perform a simulation of a transaction, but don't broadcast it (when enabled, the local Keybase is not accessible) |
| --fee-granter        | string |          |                         | Fee granter grants fees for the transaction |
| --fee-payer          | string |          |                         | Fee payer pays fees for the transaction instead of deducting from the signer |
| --fees               | string |          |                         | Fees to pay along with transaction; eg: 10uatom |
| --from               | string |          |                         | Name or address of private key with which to sign |
| --gas                | string |          | 200000                  | gas limit to set per-transaction; set to "auto" to calculate sufficient gas automatically |
| --gas-adjustment     | float  |          | 1                       | adjustment factor to be multiplied against the estimate returned by the tx simulation; if the gas limit is set manually this flag is ignored |
| --gas-prices         | string |          |                         | Gas prices in decimal format to determine the transaction fee (e.g. 0.1uatom) |
| --generate-only      |        |          |                         | Build an unsigned transaction and write it to STDOUT (when enabled, the local Keybase only accessed when providing a key name) |
| -h, --help           |        |          |                         | help for cancel_listing |
| --keyring-backend    | string |          | test                    | Select keyring's backend (os \| file \| kwallet \| pass \| test \| memory) |
| --keyring-dir        | string |          |                         | The client Keyring directory; if omitted, the default 'home' directory will be used |
| --ledger             |        |          |                         | Use a connected Ledger device |
| --node               | string |          | tcp://localhost:26657   | \<host>:\<port> to tendermint rpc interface for this chain |
| --note               | string |          |                         | Note to add a description to the transaction (previously --memo) |
| --offline            |        |          |                         | Offline mode (does not allow any online functionality) |
| -o, --output         | string |          | json                    | Output format (text \| json) |
| -s, --sequence       | uint   |          |                         | The sequence number of the signing account (offline mode only) |
| --sign-mode          | string |          |                         | Choose sign mode (direct \| amino-json \| direct-aux), this is an advanced feature |
| --timeout-height     | uint   |          |                         | Set a block timeout height to prevent the tx from being committed past a certain height |
| --tip                | string |          |                         | Tip is the amount that is going to be transferred to the fee payer on the target chain. This flag is only valid when used with --aux, and is ignored if the target chain didn't enable the TipDecorator |
| -y, --yes            |        |          |                         | Skip tx broadcasting prompt confirmation |
| --chain-id           | string |          |                         | The network chain ID |
| --home               | string |          | $HOME/.ununifi          | directory for config and data |
| --log\_format        | string |          |                         | The logging format (json \| plain) (default "plain") |
| --log\_level         | string |          | info                    | The logging level (trace \| debug \| info \| warn \| error \| fatal \| panic) |
| --trace              |        |          |                         | print out full stack trace on errors |


### ununifid tx nftmarket cancelbid <a id="tx-cancelbid"></a>

Cancel bid on nft.

```text
ununifid tx nftmarket cancelbid [class-id] [nft-id] [flags]
```

**Flags:**

| Name, shorthand      | Type   | Required | Default                 | Description |
| :------------------- | :----- | :------- | :---------------------- | :---------- |
| -a, --account-number | uint   |          |                         | The account number of the signing account (offline mode only) |
| --aux                |        |          |                         | Generate aux signer data instead of sending a tx |
| -b, --broadcast-mode | string |          | sync                    | Transaction broadcasting mode (sync \| async \| block) |
| --dry-run            |        |          |                         | ignore the --gas flag and perform a simulation of a transaction, but don't broadcast it (when enabled, the local Keybase is not accessible) |
| --fee-granter        | string |          |                         | Fee granter grants fees for the transaction |
| --fee-payer          | string |          |                         | Fee payer pays fees for the transaction instead of deducting from the signer |
| --fees               | string |          |                         | Fees to pay along with transaction; eg: 10uatom |
| --from               | string |          |                         | Name or address of private key with which to sign |
| --gas                | string |          | 200000                  | gas limit to set per-transaction; set to "auto" to calculate sufficient gas automatically |
| --gas-adjustment     | float  |          | 1                       | adjustment factor to be multiplied against the estimate returned by the tx simulation; if the gas limit is set manually this flag is ignored |
| --gas-prices         | string |          |                         | Gas prices in decimal format to determine the transaction fee (e.g. 0.1uatom) |
| --generate-only      |        |          |                         | Build an unsigned transaction and write it to STDOUT (when enabled, the local Keybase only accessed when providing a key name) |
| -h, --help           |        |          |                         | help for cancelbid |
| --keyring-backend    | string |          | test                    | Select keyring's backend (os \| file \| kwallet \| pass \| test \| memory) |
| --keyring-dir        | string |          |                         | The client Keyring directory; if omitted, the default 'home' directory will be used |
| --ledger             |        |          |                         | Use a connected Ledger device |
| --node               | string |          | tcp://localhost:26657   | \<host>:\<port> to tendermint rpc interface for this chain |
| --note               | string |          |                         | Note to add a description to the transaction (previously --memo) |
| --offline            |        |          |                         | Offline mode (does not allow any online functionality) |
| -o, --output         | string |          | json                    | Output format (text \| json) |
| -s, --sequence       | uint   |          |                         | The sequence number of the signing account (offline mode only) |
| --sign-mode          | string |          |                         | Choose sign mode (direct \| amino-json \| direct-aux), this is an advanced feature |
| --timeout-height     | uint   |          |                         | Set a block timeout height to prevent the tx from being committed past a certain height |
| --tip                | string |          |                         | Tip is the amount that is going to be transferred to the fee payer on the target chain. This flag is only valid when used with --aux, and is ignored if the target chain didn't enable the TipDecorator |
| -y, --yes            |        |          |                         | Skip tx broadcasting prompt confirmation |
| --chain-id           | string |          |                         | The network chain ID |
| --home               | string |          | $HOME/.ununifi          | directory for config and data |
| --log\_format        | string |          |                         | The logging format (json \| plain) (default "plain") |
| --log\_level         | string |          | info                    | The logging level (trace \| debug \| info \| warn \| error \| fatal \| panic) |
| --trace              |        |          |                         | print out full stack trace on errors |


### ununifid tx nftmarket endlisting <a id="tx-endlisting"></a>

end listing.

```text
ununifid tx nftmarket endlisting [class-id] [nft-id] [flags]
```

**Flags:**

| Name, shorthand      | Type   | Required | Default                 | Description |
| :------------------- | :----- | :------- | :---------------------- | :---------- |
| -a, --account-number | uint   |          |                         | The account number of the signing account (offline mode only) |
| --aux                |        |          |                         | Generate aux signer data instead of sending a tx |
| -b, --broadcast-mode | string |          | sync                    | Transaction broadcasting mode (sync \| async \| block) |
| --dry-run            |        |          |                         | ignore the --gas flag and perform a simulation of a transaction, but don't broadcast it (when enabled, the local Keybase is not accessible) |
| --fee-granter        | string |          |                         | Fee granter grants fees for the transaction |
| --fee-payer          | string |          |                         | Fee payer pays fees for the transaction instead of deducting from the signer |
| --fees               | string |          |                         | Fees to pay along with transaction; eg: 10uatom |
| --from               | string |          |                         | Name or address of private key with which to sign |
| --gas                | string |          | 200000                  | gas limit to set per-transaction; set to "auto" to calculate sufficient gas automatically |
| --gas-adjustment     | float  |          | 1                       | adjustment factor to be multiplied against the estimate returned by the tx simulation; if the gas limit is set manually this flag is ignored |
| --gas-prices         | string |          |                         | Gas prices in decimal format to determine the transaction fee (e.g. 0.1uatom) |
| --generate-only      |        |          |                         | Build an unsigned transaction and write it to STDOUT (when enabled, the local Keybase only accessed when providing a key name) |
| -h, --help           |        |          |                         | help for endlisting |
| --keyring-backend    | string |          | test                    | Select keyring's backend (os \| file \| kwallet \| pass \| test \| memory) |
| --keyring-dir        | string |          |                         | The client Keyring directory; if omitted, the default 'home' directory will be used |
| --ledger             |        |          |                         | Use a connected Ledger device |
| --node               | string |          | tcp://localhost:26657   | \<host>:\<port> to tendermint rpc interface for this chain |
| --note               | string |          |                         | Note to add a description to the transaction (previously --memo) |
| --offline            |        |          |                         | Offline mode (does not allow any online functionality) |
| -o, --output         | string |          | json                    | Output format (text \| json) |
| -s, --sequence       | uint   |          |                         | The sequence number of the signing account (offline mode only) |
| --sign-mode          | string |          |                         | Choose sign mode (direct \| amino-json \| direct-aux), this is an advanced feature |
| --timeout-height     | uint   |          |                         | Set a block timeout height to prevent the tx from being committed past a certain height |
| --tip                | string |          |                         | Tip is the amount that is going to be transferred to the fee payer on the target chain. This flag is only valid when used with --aux, and is ignored if the target chain didn't enable the TipDecorator |
| -y, --yes            |        |          |                         | Skip tx broadcasting prompt confirmation |
| --chain-id           | string |          |                         | The network chain ID |
| --home               | string |          | $HOME/.ununifi          | directory for config and data |
| --log\_format        | string |          |                         | The logging format (json \| plain) (default "plain") |
| --log\_level         | string |          | info                    | The logging level (trace \| debug \| info \| warn \| error \| fatal \| panic) |
| --trace              |        |          |                         | print out full stack trace on errors |


### ununifid tx nftmarket expand_nft_listing <a id="tx-expand_nft_listing"></a>

Expand nft listing.

```text
ununifid tx nftmarket expand_nft_listing [class-id] [nft-id] [flags]
```

**Flags:**

| Name, shorthand      | Type   | Required | Default                 | Description |
| :------------------- | :----- | :------- | :---------------------- | :---------- |
| -a, --account-number | uint   |          |                         | The account number of the signing account (offline mode only) |
| --aux                |        |          |                         | Generate aux signer data instead of sending a tx |
| -b, --broadcast-mode | string |          | sync                    | Transaction broadcasting mode (sync \| async \| block) |
| --dry-run            |        |          |                         | ignore the --gas flag and perform a simulation of a transaction, but don't broadcast it (when enabled, the local Keybase is not accessible) |
| --fee-granter        | string |          |                         | Fee granter grants fees for the transaction |
| --fee-payer          | string |          |                         | Fee payer pays fees for the transaction instead of deducting from the signer |
| --fees               | string |          |                         | Fees to pay along with transaction; eg: 10uatom |
| --from               | string |          |                         | Name or address of private key with which to sign |
| --gas                | string |          | 200000                  | gas limit to set per-transaction; set to "auto" to calculate sufficient gas automatically |
| --gas-adjustment     | float  |          | 1                       | adjustment factor to be multiplied against the estimate returned by the tx simulation; if the gas limit is set manually this flag is ignored |
| --gas-prices         | string |          |                         | Gas prices in decimal format to determine the transaction fee (e.g. 0.1uatom) |
| --generate-only      |        |          |                         | Build an unsigned transaction and write it to STDOUT (when enabled, the local Keybase only accessed when providing a key name) |
| -h, --help           |        |          |                         | help for expand_nft_listing |
| --keyring-backend    | string |          | test                    | Select keyring's backend (os \| file \| kwallet \| pass \| test \| memory) |
| --keyring-dir        | string |          |                         | The client Keyring directory; if omitted, the default 'home' directory will be used |
| --ledger             |        |          |                         | Use a connected Ledger device |
| --node               | string |          | tcp://localhost:26657   | \<host>:\<port> to tendermint rpc interface for this chain |
| --note               | string |          |                         | Note to add a description to the transaction (previously --memo) |
| --offline            |        |          |                         | Offline mode (does not allow any online functionality) |
| -o, --output         | string |          | json                    | Output format (text \| json) |
| -s, --sequence       | uint   |          |                         | The sequence number of the signing account (offline mode only) |
| --sign-mode          | string |          |                         | Choose sign mode (direct \| amino-json \| direct-aux), this is an advanced feature |
| --timeout-height     | uint   |          |                         | Set a block timeout height to prevent the tx from being committed past a certain height |
| --tip                | string |          |                         | Tip is the amount that is going to be transferred to the fee payer on the target chain. This flag is only valid when used with --aux, and is ignored if the target chain didn't enable the TipDecorator |
| -y, --yes            |        |          |                         | Skip tx broadcasting prompt confirmation |
| --chain-id           | string |          |                         | The network chain ID |
| --home               | string |          | $HOME/.ununifi          | directory for config and data |
| --log\_format        | string |          |                         | The logging format (json \| plain) (default "plain") |
| --log\_level         | string |          | info                    | The logging level (trace \| debug \| info \| warn \| error \| fatal \| panic) |
| --trace              |        |          |                         | print out full stack trace on errors |


### ununifid tx nftmarket liquidate <a id="tx-liquidate"></a>

liquidate.

```text
ununifid tx nftmarket liquidate [class-id] [nft-id] [flags]
```

**Flags:**

| Name, shorthand      | Type   | Required | Default                 | Description |
| :------------------- | :----- | :------- | :---------------------- | :---------- |
| -a, --account-number | uint   |          |                         | The account number of the signing account (offline mode only) |
| --aux                |        |          |                         | Generate aux signer data instead of sending a tx |
| -b, --broadcast-mode | string |          | sync                    | Transaction broadcasting mode (sync \| async \| block) |
| --dry-run            |        |          |                         | ignore the --gas flag and perform a simulation of a transaction, but don't broadcast it (when enabled, the local Keybase is not accessible) |
| --fee-granter        | string |          |                         | Fee granter grants fees for the transaction |
| --fee-payer          | string |          |                         | Fee payer pays fees for the transaction instead of deducting from the signer |
| --fees               | string |          |                         | Fees to pay along with transaction; eg: 10uatom |
| --from               | string |          |                         | Name or address of private key with which to sign |
| --gas                | string |          | 200000                  | gas limit to set per-transaction; set to "auto" to calculate sufficient gas automatically |
| --gas-adjustment     | float  |          | 1                       | adjustment factor to be multiplied against the estimate returned by the tx simulation; if the gas limit is set manually this flag is ignored |
| --gas-prices         | string |          |                         | Gas prices in decimal format to determine the transaction fee (e.g. 0.1uatom) |
| --generate-only      |        |          |                         | Build an unsigned transaction and write it to STDOUT (when enabled, the local Keybase only accessed when providing a key name) |
| -h, --help           |        |          |                         | help for liquidate |
| --keyring-backend    | string |          | test                    | Select keyring's backend (os \| file \| kwallet \| pass \| test \| memory) |
| --keyring-dir        | string |          |                         | The client Keyring directory; if omitted, the default 'home' directory will be used |
| --ledger             |        |          |                         | Use a connected Ledger device |
| --node               | string |          | tcp://localhost:26657   | \<host>:\<port> to tendermint rpc interface for this chain |
| --note               | string |          |                         | Note to add a description to the transaction (previously --memo) |
| --offline            |        |          |                         | Offline mode (does not allow any online functionality) |
| -o, --output         | string |          | json                    | Output format (text \| json) |
| -s, --sequence       | uint   |          |                         | The sequence number of the signing account (offline mode only) |
| --sign-mode          | string |          |                         | Choose sign mode (direct \| amino-json \| direct-aux), this is an advanced feature |
| --timeout-height     | uint   |          |                         | Set a block timeout height to prevent the tx from being committed past a certain height |
| --tip                | string |          |                         | Tip is the amount that is going to be transferred to the fee payer on the target chain. This flag is only valid when used with --aux, and is ignored if the target chain didn't enable the TipDecorator |
| -y, --yes            |        |          |                         | Skip tx broadcasting prompt confirmation |
| --chain-id           | string |          |                         | The network chain ID |
| --home               | string |          | $HOME/.ununifi          | directory for config and data |
| --log\_format        | string |          |                         | The logging format (json \| plain) (default "plain") |
| --log\_level         | string |          | info                    | The logging level (trace \| debug \| info \| warn \| error \| fatal \| panic) |
| --trace              |        |          |                         | print out full stack trace on errors |


### ununifid tx nftmarket listing <a id="tx-listing"></a>

Creates a new listing.

```text
ununifid tx nftmarket listing [class-id] [nft-id] [flags]
```

**Flags:**

| Name, shorthand      | Type   | Required | Default                 | Description |
| :------------------- | :----- | :------- | :---------------------- | :---------- |
| -a, --account-number | uint   |          |                         | The account number of the signing account (offline mode only) |
| --aux                |        |          |                         | Generate aux signer data instead of sending a tx |
| --bid-active-rank    | uint   | 1        |                         | bid active rank |
| --bid-token          | string | uguu     |                         | bid token |
| -b, --broadcast-mode | string |          | sync                    | Transaction broadcasting mode (sync \| async \| block) |
| --dry-run            |        |          |                         | ignore the --gas flag and perform a simulation of a transaction, but don't broadcast it (when enabled, the local Keybase is not accessible) |
| --fee-granter        | string |          |                         | Fee granter grants fees for the transaction |
| --fee-payer          | string |          |                         | Fee payer pays fees for the transaction instead of deducting from the signer |
| --fees               | string |          |                         | Fees to pay along with transaction; eg: 10uatom |
| --from               | string |          |                         | Name or address of private key with which to sign |
| --gas                | string |          | 200000                  | gas limit to set per-transaction; set to "auto" to calculate sufficient gas automatically |
| --gas-adjustment     | float  |          | 1                       | adjustment factor to be multiplied against the estimate returned by the tx simulation; if the gas limit is set manually this flag is ignored |
| --gas-prices         | string |          |                         | Gas prices in decimal format to determine the transaction fee (e.g. 0.1uatom) |
| --generate-only      |        |          |                         | Build an unsigned transaction and write it to STDOUT (when enabled, the local Keybase only accessed when providing a key name) |
| -h, --help           |        |          |                         | help for listing |
| --keyring-backend    | string |          | test                    | Select keyring's backend (os \| file \| kwallet \| pass \| test \| memory) |
| --keyring-dir        | string |          |                         | The client Keyring directory; if omitted, the default 'home' directory will be used |
| --ledger             |        |          |                         | Use a connected Ledger device |
| --min-bid            | uint   | 1        |                         | min bid amount |
| --node               | string |          | tcp://localhost:26657   | \<host>:\<port> to tendermint rpc interface for this chain |
| --note               | string |          |                         | Note to add a description to the transaction (previously --memo) |
| --offline            |        |          |                         | Offline mode (does not allow any online functionality) |
| -o, --output         | string |          | json                    | Output format (text \| json) |
| -s, --sequence       | uint   |          |                         | The sequence number of the signing account (offline mode only) |
| --sign-mode          | string |          |                         | Choose sign mode (direct \| amino-json \| direct-aux), this is an advanced feature |
| --timeout-height     | uint   |          |                         | Set a block timeout height to prevent the tx from being committed past a certain height |
| --tip                | string |          |                         | Tip is the amount that is going to be transferred to the fee payer on the target chain. This flag is only valid when used with --aux, and is ignored if the target chain didn't enable the TipDecorator |
| -y, --yes            |        |          |                         | Skip tx broadcasting prompt confirmation |
| --chain-id           | string |          |                         | The network chain ID |
| --home               | string |          | $HOME/.ununifi          | directory for config and data |
| --log\_format        | string |          |                         | The logging format (json \| plain) (default "plain") |
| --log\_level         | string |          | info                    | The logging level (trace \| debug \| info \| warn \| error \| fatal \| panic) |
| --trace              |        |          |                         | print out full stack trace on errors |


### ununifid tx nftmarket mint <a id="tx-mint"></a>

Mint an nft.

```text
ununifid tx nftmarket mint [class-id] [nft-id] [uri] [uri-hash] [flags]
```

**Flags:**

| Name, shorthand      | Type   | Required | Default                 | Description |
| :------------------- | :----- | :------- | :---------------------- | :---------- |
| -a, --account-number | uint   |          |                         | The account number of the signing account (offline mode only) |
| --aux                |        |          |                         | Generate aux signer data instead of sending a tx |
| -b, --broadcast-mode | string |          | sync                    | Transaction broadcasting mode (sync \| async \| block) |
| --dry-run            |        |          |                         | ignore the --gas flag and perform a simulation of a transaction, but don't broadcast it (when enabled, the local Keybase is not accessible) |
| --fee-granter        | string |          |                         | Fee granter grants fees for the transaction |
| --fee-payer          | string |          |                         | Fee payer pays fees for the transaction instead of deducting from the signer |
| --fees               | string |          |                         | Fees to pay along with transaction; eg: 10uatom |
| --from               | string |          |                         | Name or address of private key with which to sign |
| --gas                | string |          | 200000                  | gas limit to set per-transaction; set to "auto" to calculate sufficient gas automatically |
| --gas-adjustment     | float  |          | 1                       | adjustment factor to be multiplied against the estimate returned by the tx simulation; if the gas limit is set manually this flag is ignored |
| --gas-prices         | string |          |                         | Gas prices in decimal format to determine the transaction fee (e.g. 0.1uatom) |
| --generate-only      |        |          |                         | Build an unsigned transaction and write it to STDOUT (when enabled, the local Keybase only accessed when providing a key name) |
| -h, --help           |        |          |                         | help for mint |
| --keyring-backend    | string |          | test                    | Select keyring's backend (os \| file \| kwallet \| pass \| test \| memory) |
| --keyring-dir        | string |          |                         | The client Keyring directory; if omitted, the default 'home' directory will be used |
| --ledger             |        |          |                         | Use a connected Ledger device |
| --node               | string |          | tcp://localhost:26657   | \<host>:\<port> to tendermint rpc interface for this chain |
| --note               | string |          |                         | Note to add a description to the transaction (previously --memo) |
| --offline            |        |          |                         | Offline mode (does not allow any online functionality) |
| -o, --output         | string |          | json                    | Output format (text \| json) |
| -s, --sequence       | uint   |          |                         | The sequence number of the signing account (offline mode only) |
| --sign-mode          | string |          |                         | Choose sign mode (direct \| amino-json \| direct-aux), this is an advanced feature |
| --timeout-height     | uint   |          |                         | Set a block timeout height to prevent the tx from being committed past a certain height |
| --tip                | string |          |                         | Tip is the amount that is going to be transferred to the fee payer on the target chain. This flag is only valid when used with --aux, and is ignored if the target chain didn't enable the TipDecorator |
| -y, --yes            |        |          |                         | Skip tx broadcasting prompt confirmation |
| --chain-id           | string |          |                         | The network chain ID |
| --home               | string |          | $HOME/.ununifi          | directory for config and data |
| --log\_format        | string |          |                         | The logging format (json \| plain) (default "plain") |
| --log\_level         | string |          | info                    | The logging level (trace \| debug \| info \| warn \| error \| fatal \| panic) |
| --trace              |        |          |                         | print out full stack trace on errors |


### ununifid tx nftmarket mint_stablecoin <a id="tx-mint_stablecoin"></a>

mint stablecoin.

```text
ununifid tx nftmarket mint_stablecoin [class-id] [nft-id] [amount] [flags]
```

**Flags:**

| Name, shorthand      | Type   | Required | Default                 | Description |
| :------------------- | :----- | :------- | :---------------------- | :---------- |
| -a, --account-number | uint   |          |                         | The account number of the signing account (offline mode only) |
| --aux                |        |          |                         | Generate aux signer data instead of sending a tx |
| -b, --broadcast-mode | string |          | sync                    | Transaction broadcasting mode (sync \| async \| block) |
| --dry-run            |        |          |                         | ignore the --gas flag and perform a simulation of a transaction, but don't broadcast it (when enabled, the local Keybase is not accessible) |
| --fee-granter        | string |          |                         | Fee granter grants fees for the transaction |
| --fee-payer          | string |          |                         | Fee payer pays fees for the transaction instead of deducting from the signer |
| --fees               | string |          |                         | Fees to pay along with transaction; eg: 10uatom |
| --from               | string |          |                         | Name or address of private key with which to sign |
| --gas                | string |          | 200000                  | gas limit to set per-transaction; set to "auto" to calculate sufficient gas automatically |
| --gas-adjustment     | float  |          | 1                       | adjustment factor to be multiplied against the estimate returned by the tx simulation; if the gas limit is set manually this flag is ignored |
| --gas-prices         | string |          |                         | Gas prices in decimal format to determine the transaction fee (e.g. 0.1uatom) |
| --generate-only      |        |          |                         | Build an unsigned transaction and write it to STDOUT (when enabled, the local Keybase only accessed when providing a key name) |
| -h, --help           |        |          |                         | help for mint_stablecoin |
| --keyring-backend    | string |          | test                    | Select keyring's backend (os \| file \| kwallet \| pass \| test \| memory) |
| --keyring-dir        | string |          |                         | The client Keyring directory; if omitted, the default 'home' directory will be used |
| --ledger             |        |          |                         | Use a connected Ledger device |
| --node               | string |          | tcp://localhost:26657   | \<host>:\<port> to tendermint rpc interface for this chain |
| --note               | string |          |                         | Note to add a description to the transaction (previously --memo) |
| --offline            |        |          |                         | Offline mode (does not allow any online functionality) |
| -o, --output         | string |          | json                    | Output format (text \| json) |
| -s, --sequence       | uint   |          |                         | The sequence number of the signing account (offline mode only) |
| --sign-mode          | string |          |                         | Choose sign mode (direct \| amino-json \| direct-aux), this is an advanced feature |
| --timeout-height     | uint   |          |                         | Set a block timeout height to prevent the tx from being committed past a certain height |
| --tip                | string |          |                         | Tip is the amount that is going to be transferred to the fee payer on the target chain. This flag is only valid when used with --aux, and is ignored if the target chain didn't enable the TipDecorator |
| -y, --yes            |        |          |                         | Skip tx broadcasting prompt confirmation |
| --chain-id           | string |          |                         | The network chain ID |
| --home               | string |          | $HOME/.ununifi          | directory for config and data |
| --log\_format        | string |          |                         | The logging format (json \| plain) (default "plain") |
| --log\_level         | string |          | info                    | The logging level (trace \| debug \| info \| warn \| error \| fatal \| panic) |
| --trace              |        |          |                         | print out full stack trace on errors |

### ununifid tx nftmarket mint_stablecoin <a id="tx-mint_stablecoin"></a>

mint stablecoin.

```text
ununifid tx nftmarket mint_stablecoin [class-id] [nft-id] [amount] [flags]
```

**Flags:**

| Name, shorthand      | Type   | Required | Default                 | Description |
| :------------------- | :----- | :------- | :---------------------- | :---------- |
| -a, --account-number | uint   |          |                         | The account number of the signing account (offline mode only) |
| --aux                |        |          |                         | Generate aux signer data instead of sending a tx |
| -b, --broadcast-mode | string |          | sync                    | Transaction broadcasting mode (sync \| async \| block) |
| --dry-run            |        |          |                         | ignore the --gas flag and perform a simulation of a transaction, but don't broadcast it (when enabled, the local Keybase is not accessible) |
| --fee-granter        | string |          |                         | Fee granter grants fees for the transaction |
| --fee-payer          | string |          |                         | Fee payer pays fees for the transaction instead of deducting from the signer |
| --fees               | string |          |                         | Fees to pay along with transaction; eg: 10uatom |
| --from               | string |          |                         | Name or address of private key with which to sign |
| --gas                | string |          | 200000                  | gas limit to set per-transaction; set to "auto" to calculate sufficient gas automatically |
| --gas-adjustment     | float  |          | 1                       | adjustment factor to be multiplied against the estimate returned by the tx simulation; if the gas limit is set manually this flag is ignored |
| --gas-prices         | string |          |                         | Gas prices in decimal format to determine the transaction fee (e.g. 0.1uatom) |
| --generate-only      |        |          |                         | Build an unsigned transaction and write it to STDOUT (when enabled, the local Keybase only accessed when providing a key name) |
| -h, --help           |        |          |                         | help for mint_stablecoin |
| --keyring-backend    | string |          | test                    | Select keyring's backend (os \| file \| kwallet \| pass \| test \| memory) |
| --keyring-dir        | string |          |                         | The client Keyring directory; if omitted, the default 'home' directory will be used |
| --ledger             |        |          |                         | Use a connected Ledger device |
| --node               | string |          | tcp://localhost:26657   | \<host>:\<port> to tendermint rpc interface for this chain |
| --note               | string |          |                         | Note to add a description to the transaction (previously --memo) |
| --offline            |        |          |                         | Offline mode (does not allow any online functionality) |
| -o, --output         | string |          | json                    | Output format (text \| json) |
| -s, --sequence       | uint   |          |                         | The sequence number of the signing account (offline mode only) |
| --sign-mode          | string |          |                         | Choose sign mode (direct \| amino-json \| direct-aux), this is an advanced feature |
| --timeout-height     | uint   |          |                         | Set a block timeout height to prevent the tx from being committed past a certain height |
| --tip                | string |          |                         | Tip is the amount that is going to be transferred to the fee payer on the target chain. This flag is only valid when used with --aux, and is ignored if the target chain didn't enable the TipDecorator |
| -y, --yes            |        |          |                         | Skip tx broadcasting prompt confirmation |
| --chain-id           | string |          |                         | The network chain ID |
| --home               | string |          | $HOME/.ununifi          | directory for config and data |
| --log\_format        | string |          |                         | The logging format (json \| plain) (default "plain") |
| --log\_level         | string |          | info                    | The logging level (trace \| debug \| info \| warn \| error \| fatal \| panic) |
| --trace              |        |          |                         | print out full stack trace on errors |


### ununifid tx nftmarket pay_fullbid <a id="tx-pay_fullbid"></a>

Pay full bid on nft.

```text
ununifid tx nftmarket pay_fullbid [class-id] [nft-id] [flags]
```

**Flags:**

| Name, shorthand      | Type   | Required | Default                 | Description |
| :------------------- | :----- | :------- | :---------------------- | :---------- |
| -a, --account-number | uint   |          |                         | The account number of the signing account (offline mode only) |
| --aux                |        |          |                         | Generate aux signer data instead of sending a tx |
| -b, --broadcast-mode | string |          | sync                    | Transaction broadcasting mode (sync \| async \| block) |
| --dry-run            |        |          |                         | ignore the --gas flag and perform a simulation of a transaction, but don't broadcast it (when enabled, the local Keybase is not accessible) |
| --fee-granter        | string |          |                         | Fee granter grants fees for the transaction |
| --fee-payer          | string |          |                         | Fee payer pays fees for the transaction instead of deducting from the signer |
| --fees               | string |          |                         | Fees to pay along with transaction; eg: 10uatom |
| --from               | string |          |                         | Name or address of private key with which to sign |
| --gas                | string |          | 200000                  | gas limit to set per-transaction; set to "auto" to calculate sufficient gas automatically |
| --gas-adjustment     | float  |          | 1                       | adjustment factor to be multiplied against the estimate returned by the tx simulation; if the gas limit is set manually this flag is ignored |
| --gas-prices         | string |          |                         | Gas prices in decimal format to determine the transaction fee (e.g. 0.1uatom) |
| --generate-only      |        |          |                         | Build an unsigned transaction and write it to STDOUT (when enabled, the local Keybase only accessed when providing a key name) |
| -h, --help           |        |          |                         | help for pay_fullbid |
| --keyring-backend    | string |          | test                    | Select keyring's backend (os \| file \| kwallet \| pass \| test \| memory) |
| --keyring-dir        | string |          |                         | The client Keyring directory; if omitted, the default 'home' directory will be used |
| --ledger             |        |          |                         | Use a connected Ledger device |
| --node               | string |          | tcp://localhost:26657   | \<host>:\<port> to tendermint rpc interface for this chain |
| --note               | string |          |                         | Note to add a description to the transaction (previously --memo) |
| --offline            |        |          |                         | Offline mode (does not allow any online functionality) |
| -o, --output         | string |          | json                    | Output format (text \| json) |
| -s, --sequence       | uint   |          |                         | The sequence number of the signing account (offline mode only) |
| --sign-mode          | string |          |                         | Choose sign mode (direct \| amino-json \| direct-aux), this is an advanced feature |
| --timeout-height     | uint   |          |                         | Set a block timeout height to prevent the tx from being committed past a certain height |
| --tip                | string |          |                         | Tip is the amount that is going to be transferred to the fee payer on the target chain. This flag is only valid when used with --aux, and is ignored if the target chain didn't enable the TipDecorator |
| -y, --yes            |        |          |                         | Skip tx broadcasting prompt confirmation |
| --chain-id           | string |          |                         | The network chain ID |
| --home               | string |          | $HOME/.ununifi          | directory for config and data |
| --log\_format        | string |          |                         | The logging format (json \| plain) (default "plain") |
| --log\_level         | string |          | info                    | The logging level (trace \| debug \| info \| warn \| error \| fatal \| panic) |
| --trace              |        |          |                         | print out full stack trace on errors |


### ununifid tx nftmarket placebid <a id="tx-placebid"></a>

Creates a new place bid.

```text
ununifid tx nftmarket placebid [class-id] [nft-id] [amount] [flags]
```

**Flags:**

| Name, shorthand      | Type   | Required | Default                 | Description |
| :------------------- | :----- | :------- | :---------------------- | :---------- |
| -a, --account-number | uint   |          |                         | The account number of the signing account (offline mode only) |
| -p, --automatic-payment |     |          |                         | automation payment |
| --aux                |        |          |                         | Generate aux signer data instead of sending a tx |
| -b, --broadcast-mode | string |          | sync                    | Transaction broadcasting mode (sync \| async \| block) |
| --dry-run            |        |          |                         | ignore the --gas flag and perform a simulation of a transaction, but don't broadcast it (when enabled, the local Keybase is not accessible) |
| --fee-granter        | string |          |                         | Fee granter grants fees for the transaction |
| --fee-payer          | string |          |                         | Fee payer pays fees for the transaction instead of deducting from the signer |
| --fees               | string |          |                         | Fees to pay along with transaction; eg: 10uatom |
| --from               | string |          |                         | Name or address of private key with which to sign |
| --gas                | string |          | 200000                  | gas limit to set per-transaction; set to "auto" to calculate sufficient gas automatically |
| --gas-adjustment     | float  |          | 1                       | adjustment factor to be multiplied against the estimate returned by the tx simulation; if the gas limit is set manually this flag is ignored |
| --gas-prices         | string |          |                         | Gas prices in decimal format to determine the transaction fee (e.g. 0.1uatom) |
| --generate-only      |        |          |                         | Build an unsigned transaction and write it to STDOUT (when enabled, the local Keybase only accessed when providing a key name) |
| -h, --help           |        |          |                         | help for placebid |
| --keyring-backend    | string |          | test                    | Select keyring's backend (os \| file \| kwallet \| pass \| test \| memory) |
| --keyring-dir        | string |          |                         | The client Keyring directory; if omitted, the default 'home' directory will be used |
| --ledger             |        |          |                         | Use a connected Ledger device |
| --node               | string |          | tcp://localhost:26657   | \<host>:\<port> to tendermint rpc interface for this chain |
| --note               | string |          |                         | Note to add a description to the transaction (previously --memo) |
| --offline            |        |          |                         | Offline mode (does not allow any online functionality) |
| -o, --output         | string |          | json                    | Output format (text \| json) |
| -s, --sequence       | uint   |          |                         | The sequence number of the signing account (offline mode only) |
| --sign-mode          | string |          |                         | Choose sign mode (direct \| amino-json \| direct-aux), this is an advanced feature |
| --timeout-height     | uint   |          |                         | Set a block timeout height to prevent the tx from being committed past a certain height |
| --tip                | string |          |                         | Tip is the amount that is going to be transferred to the fee payer on the target chain. This flag is only valid when used with --aux, and is ignored if the target chain didn't enable the TipDecorator |
| -y, --yes            |        |          |                         | Skip tx broadcasting prompt confirmation |
| --chain-id           | string |          |                         | The network chain ID |
| --home               | string |          | $HOME/.ununifi          | directory for config and data |
| --log\_format        | string |          |                         | The logging format (json \| plain) (default "plain") |
| --log\_level         | string |          | info                    | The logging level (trace \| debug \| info \| warn \| error \| fatal \| panic) |
| --trace              |        |          |                         | print out full stack trace on errors |


### ununifid tx nftmarket repay <a id="tx-repay"></a>

repay loan on nft.

```text
ununifid tx nftmarket repay [class-id] [nft-id] [amount] [flags]
```

**Flags:**

| Name, shorthand      | Type   | Required | Default                 | Description |
| :------------------- | :----- | :------- | :---------------------- | :---------- |
| -a, --account-number | uint   |          |                         | The account number of the signing account (offline mode only) |
| --aux                |        |          |                         | Generate aux signer data instead of sending a tx |
| -b, --broadcast-mode | string |          | sync                    | Transaction broadcasting mode (sync \| async \| block) |
| --dry-run            |        |          |                         | ignore the --gas flag and perform a simulation of a transaction, but don't broadcast it (when enabled, the local Keybase is not accessible) |
| --fee-granter        | string |          |                         | Fee granter grants fees for the transaction |
| --fee-payer          | string |          |                         | Fee payer pays fees for the transaction instead of deducting from the signer |
| --fees               | string |          |                         | Fees to pay along with transaction; eg: 10uatom |
| --from               | string |          |                         | Name or address of private key with which to sign |
| --gas                | string |          | 200000                  | gas limit to set per-transaction; set to "auto" to calculate sufficient gas automatically |
| --gas-adjustment     | float  |          | 1                       | adjustment factor to be multiplied against the estimate returned by the tx simulation; if the gas limit is set manually this flag is ignored |
| --gas-prices         | string |          |                         | Gas prices in decimal format to determine the transaction fee (e.g. 0.1uatom) |
| --generate-only      |        |          |                         | Build an unsigned transaction and write it to STDOUT (when enabled, the local Keybase only accessed when providing a key name) |
| -h, --help           |        |          |                         | help for repay |
| --keyring-backend    | string |          | test                    | Select keyring's backend (os \| file \| kwallet \| pass \| test \| memory) |
| --keyring-dir        | string |          |                         | The client Keyring directory; if omitted, the default 'home' directory will be used |
| --ledger             |        |          |                         | Use a connected Ledger device |
| --node               | string |          | tcp://localhost:26657   | \<host>:\<port> to tendermint rpc interface for this chain |
| --note               | string |          |                         | Note to add a description to the transaction (previously --memo) |
| --offline            |        |          |                         | Offline mode (does not allow any online functionality) |
| -o, --output         | string |          | json                    | Output format (text \| json) |
| -s, --sequence       | uint   |          |                         | The sequence number of the signing account (offline mode only) |
| --sign-mode          | string |          |                         | Choose sign mode (direct \| amino-json \| direct-aux), this is an advanced feature |
| --timeout-height     | uint   |          |                         | Set a block timeout height to prevent the tx from being committed past a certain height |
| --tip                | string |          |                         | Tip is the amount that is going to be transferred to the fee payer on the target chain. This flag is only valid when used with --aux, and is ignored if the target chain didn't enable the TipDecorator |
| -y, --yes            |        |          |                         | Skip tx broadcasting prompt confirmation |
| --chain-id           | string |          |                         | The network chain ID |
| --home               | string |          | $HOME/.ununifi          | directory for config and data |
| --log\_format        | string |          |                         | The logging format (json \| plain) (default "plain") |
| --log\_level         | string |          | info                    | The logging level (trace \| debug \| info \| warn \| error \| fatal \| panic) |
| --trace              |        |          |                         | print out full stack trace on errors |


### ununifid tx nftmarket selling_decision <a id="tx-selling_decision"></a>

broadcast selling decision message.

```text
ununifid tx nftmarket selling_decision [class-id] [nft-id] [flags]
```

**Flags:**

| Name, shorthand      | Type   | Required | Default                 | Description |
| :------------------- | :----- | :------- | :---------------------- | :---------- |
| -a, --account-number | uint   |          |                         | The account number of the signing account (offline mode only) |
| --aux                |        |          |                         | Generate aux signer data instead of sending a tx |
| -b, --broadcast-mode | string |          | sync                    | Transaction broadcasting mode (sync \| async \| block) |
| --dry-run            |        |          |                         | ignore the --gas flag and perform a simulation of a transaction, but don't broadcast it (when enabled, the local Keybase is not accessible) |
| --fee-granter        | string |          |                         | Fee granter grants fees for the transaction |
| --fee-payer          | string |          |                         | Fee payer pays fees for the transaction instead of deducting from the signer |
| --fees               | string |          |                         | Fees to pay along with transaction; eg: 10uatom |
| --from               | string |          |                         | Name or address of private key with which to sign |
| --gas                | string |          | 200000                  | gas limit to set per-transaction; set to "auto" to calculate sufficient gas automatically |
| --gas-adjustment     | float  |          | 1                       | adjustment factor to be multiplied against the estimate returned by the tx simulation; if the gas limit is set manually this flag is ignored |
| --gas-prices         | string |          |                         | Gas prices in decimal format to determine the transaction fee (e.g. 0.1uatom) |
| --generate-only      |        |          |                         | Build an unsigned transaction and write it to STDOUT (when enabled, the local Keybase only accessed when providing a key name) |
| -h, --help           |        |          |                         | help for selling_decision |
| --keyring-backend    | string |          | test                    | Select keyring's backend (os \| file \| kwallet \| pass \| test \| memory) |
| --keyring-dir        | string |          |                         | The client Keyring directory; if omitted, the default 'home' directory will be used |
| --ledger             |        |          |                         | Use a connected Ledger device |
| --node               | string |          | tcp://localhost:26657   | \<host>:\<port> to tendermint rpc interface for this chain |
| --note               | string |          |                         | Note to add a description to the transaction (previously --memo) |
| --offline            |        |          |                         | Offline mode (does not allow any online functionality) |
| -o, --output         | string |          | json                    | Output format (text \| json) |
| -s, --sequence       | uint   |          |                         | The sequence number of the signing account (offline mode only) |
| --sign-mode          | string |          |                         | Choose sign mode (direct \| amino-json \| direct-aux), this is an advanced feature |
| --timeout-height     | uint   |          |                         | Set a block timeout height to prevent the tx from being committed past a certain height |
| --tip                | string |          |                         | Tip is the amount that is going to be transferred to the fee payer on the target chain. This flag is only valid when used with --aux, and is ignored if the target chain didn't enable the TipDecorator |
| -y, --yes            |        |          |                         | Skip tx broadcasting prompt confirmation |
| --chain-id           | string |          |                         | The network chain ID |
| --home               | string |          | $HOME/.ununifi          | directory for config and data |
| --log\_format        | string |          |                         | The logging format (json \| plain) (default "plain") |
| --log\_level         | string |          | info                    | The logging level (trace \| debug \| info \| warn \| error \| fatal \| panic) |
| --trace              |        |          |                         | print out full stack trace on errors |
