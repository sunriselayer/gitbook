---
description: >-
  `wasm`モジュールを使用すると、CosmWasmスマートコントラクトを管理できます。
---

# `wasm`

**クエリ:**

| 名前 | 説明 |
| :------------------------------------------------------------- | :----------------------------------------------------------- |
| [build-address](wasm.md#build-address) | コントラクトアドレスを構築する |
| [code](wasm.md#code) | 指定されたコードIDのwasmバイトコードをダウンロードする |
| [code-info](wasm.md#code-info) | コードIDのメタデータを出力する |
| [contract](wasm.md#contract) | 指定されたアドレスのコントラクトのメタデータを出力する |
| [contract-history](wasm.md#contract-history) | 指定されたアドレスのコントラクトのコード履歴を出力する |
| [contract-state](wasm.md#contract-state) | wasmモジュールのクエリコマンド |
| [libwasmvm-version](wasm.md#libwasmvm-version) | libwasmvmのバージョンを取得する |
| [list-code](wasm.md#list-code) | チェーン上のすべてのwasmバイトコードを一覧表示する |
| [list-contract-by-code](wasm.md#list-contract-by-code) | 指定されたコードIDのチェーン上のすべてのwasmバイトコードを一覧表示する |
| [list-contracts-by-creator](wasm.md#list-contracts-by-creator) | 作成者別にすべてのコントラクトを一覧表示する |
| [params](wasm.md#params) | 現在のwasmパラメータを照会する |
| [pinned](wasm.md#pinned) | すべての固定されたコードIDを一覧表示する |

**Tx:**

| 名前 | 説明 |
| :------------------------------------------------------------- | :-------------------------------------------------------- |
| [clear-contract-admin](wasm.md#clear-contract-admin) | さらなる移行を防ぐためにコントラクトの管理者をクリアする |
| [execute](wasm.md#execute) | wasmコントラクトでコマンドを実行する |
| [grant](wasm.md#grant) | アドレスに承認を付与する |
| [instantiate](wasm.md#instantiate) | wasmコントラクトをインスタンス化する |
| [instantiate2](wasm.md#instantiate2) | 予測可能なアドレスでwasmコントラクトをインスタンス化する |
| [migrate](wasm.md#migrate) | wasmコントラクトを新しいコードバージョンに移行する |
| [set-contract-admin](wasm.md#set-contract-admin) | コントラクトの新しい管理者を設定する |
| [store](wasm.md#store) | wasmバイナリをアップロードする |
| [update-instantiate-config](wasm.md#update-instantiate-config) | codeIDのインスタンス化設定を更新する |

## `wasm`クエリの共通フラグ

`wasm`クエリコマンドの共通フラグをまとめます。

**フラグ:**

| 名前、省略形 | 型 | 必須 | デフォルト | 説明 |
| :-------------- | :----- | :------- | :-------------------- | :------------------------------------------------------------------------------------ |
| --grpc-addr | string | | | このチェーンに使用するgRPCエンドポイント |
| --grpc-insecure | | | | 安全でないチャネル経由のgRPCを許可する、TLSでない場合、サーバーはTLSを使用する必要があります |
| --height | int | | | 状態を照会する特定の高さを使用する（ノードが状態をプルーニングしている場合、エラーになる可能性があります） |
| -h, --help | | | | \<module name>のヘルプ |
| --node | string | | tcp://localhost:26657 | このチェーンのTendermint RPCインターフェースへの\<host>:\<port> |
| -o, --output | string | | text | 出力形式（text \| json） |

**グローバルフラグ:**

| 名前、省略形 | 型 | 必須 | デフォルト | 説明 |
| :-------------- | :----- | :------- | :------------- | :---------------------------------------------------------------------------- |
| --chain-id | string | | | ネットワークチェーンID |
| --home | string | | $HOME/.ununifi | 設定とデータのディレクトリ |
| --log_format | string | | | ログ形式（json \| plain）（デフォルトは"plain"） |
| --log_level | string | | info | ログレベル（trace \| debug \| info \| warn \| error \| fatal \| panic） |
| --trace | | | | エラー時に完全なスタックトレースを出力する |

### エンコードフラグ

**フラグ:**

| 名前、省略形 | 型 | 必須 | デフォルト | 説明 |
| :-------------- | :--- | :------- | :------ | :------------------ |
| --ascii | | | | asciiエンコードされたソルト |
| --b64 | | | | base64エンコードされたソルト |
| --hex | | | | hexエンコードされたソルト |

### ページネーションフラグ

**フラグ:**

| 名前、省略形 | 型 | 必須 | デフォルト | 説明 |
| :-------------- | :----- | :------- | :------ | :---------------------------------------------------------------------------------------------------- |
| --count-total | | | | 照会するコントラクト履歴のレコードの総数をカウントする |
| --limit | uint | | | 照会するコントラクト履歴のページネーション制限（デフォルトは100） |
| --offset | uint | | | 照会するコントラクト履歴のページネーションオフセット |
| --page | uint | | | 照会するコントラクト履歴のページネーションページ。これにより、オフセットがlimitの倍数に設定されます（デフォルトは1） |
| --page-key | string | | | 照会するコントラクト履歴のページネーションページキー |
| --reverse | | | | 結果を降順でソートする |

## クエリ

### ununifid query wasm build-address

コントラクトアドレスを構築する

```bash
ununifid query wasm build-address [code-hash] [creator-address] [salt-hex-encoded] [json_encoded_init_args (fixedに設定されている場合は必須)] [flags]
```

**フラグ:**

{% hint style="info" %}
フラグの詳細については、[共通フラグ](wasm.md#common-query-flags)と[エンコードフラグ](wasm.md#encode-flags)を参照してください。
{% endhint %}

### ununifid query wasm code

指定されたコードIDのwasmバイトコードをダウンロードする

```bash
ununifid query wasm code [code_id] [output filename] [flags]
```

**フラグ:**

{% hint style="info" %}
フラグの詳細については、[共通フラグ](wasm.md#common-query-flags)を参照してください。
{% endhint %}

### ununifid query wasm code-info

コードIDのメタデータを出力する

```bash
ununifid query wasm code-info [code_id] [flags]
```

**フラグ:**

{% hint style="info" %}
フラグの詳細については、[共通フラグ](wasm.md#common-query-flags)を参照してください。
{% endhint %}

### ununifid query wasm contract

指定されたアドレスのコントラクトのメタデータを出力する

```bash
ununifid query wasm contract [bech32_address] [flags]
```

**フラグ:**

{% hint style="info" %}
フラグの詳細については、[共通フラグ](wasm.md#common-query-flags)を参照してください。
{% endhint %}

### ununifid query wasm contract-history

指定されたアドレスのコントラクトのコード履歴を出力する

```bash
ununifid query wasm contract-history [bech32_address] [flags]
```

**フラグ:**

{% hint style="info" %}
フラグの詳細については、[共通フラグ](wasm.md#common-query-flags)と[ページネーションフラグ](wasm.md#pagination-flags)を参照してください。
{% endhint %}

### ununifid query wasm contract-state

wasmモジュールのクエリコマンド

```bash
ununifid query wasm contract-state [flags]
ununifid query wasm contract-state [command]
```

**コマンド:**

| 名前、省略形 | 型 | 必須 | デフォルト | 説明 |
| :-------------- | :--- | :------- | :------ | :------------------------------------------------------------------------------- |
| all | | | | 指定されたアドレスのコントラクトのすべての内部状態を出力する |
| raw | | | | 指定されたアドレスのコントラクトのキーの内部状態を出力する |
| smart | | | | 指定されたアドレスのコントラクトをクエリデータで呼び出し、返された結果を出力する |

```bash
ununifid query wasm contract-state all [bech32_address] [flags]
```

**フラグ:**

{% hint style="info" %}
フラグの詳細については、[共通フラグ](wasm.md#common-query-flags)と[ページネーションフラグ](wasm.md#pagination-flags)を参照してください。
{% endhint %}

```bash
ununifid query wasm contract-state raw [bech32_address] [key] [flags]
ununifid query wasm contract-state smart [bech32_address] [query] [flags]
```

**フラグ:**

{% hint style="info" %}
フラグの詳細については、[共通フラグ](wasm.md#common-query-flags)と[エンコードフラグ](wasm.md#encode-flags)を参照してください。
{% endhint %}

### ununifid query wasm libwasmvm-version

libwasmvmのバージョンを取得する

```bash
ununifid query wasm libwasmvm-version [flags]
```

**フラグ:**

{% hint style="info" %}
フラグの詳細については、[共通フラグ](wasm.md#common-query-flags)を参照してください。
{% endhint %}

### ununifid query wasm list-code

チェーン上のすべてのwasmバイトコードを一覧表示する

```bash
ununifid query wasm list-code [flags]
```

**フラグ:**

{% hint style="info" %}
フラグの詳細については、[共通フラグ](wasm.md#common-query-flags)と[ページネーションフラグ](wasm.md#pagination-flags)を参照してください。
{% endhint %}

### ununifid query wasm list-contract-by-code

指定されたコードIDのチェーン上のすべてのwasmバイトコードを一覧表示する

```bash
ununifid query wasm list-contract-by-code [code_id] [flags]
```

**フラグ:**

{% hint style="info" %}
フラグの詳細については、[共通フラグ](wasm.md#common-query-flags)と[ページネーションフラグ](wasm.md#pagination-flags)を参照してください。
{% endhint %}

### ununifid query wasm list-contracts-by-creator

作成者別にすべてのコントラクトを一覧表示する

```bash
ununifid query wasm list-contracts-by-creator [creator] [flags]
```

**フラグ:**

{% hint style="info" %}
フラグの詳細については、[共通フラグ](wasm.md#common-query-flags)と[ページネーションフラグ](wasm.md#pagination-flags)を参照してください。
{% endhint %}

### ununifid query wasm params

現在のwasmパラメータを照会する

```bash
ununifid query wasm params [flags]
```

**フラグ:**

{% hint style="info" %}
フラグの詳細については、[共通フラグ](wasm.md#common-query-flags)を参照してください。
{% endhint %}

### ununifid query wasm pinned

すべての固定されたコードIDを一覧表示する

```bash
ununifid query wasm pinned [flags]
```

**フラグ:**

{% hint style="info" %}
フラグの詳細については、[共通フラグ](wasm.md#common-query-flags)と[ページネーションフラグ](wasm.md#pagination-flags)を参照してください。
{% endhint %}

## nftmint txの共通フラグ

nftmint txコマンドの共通フラグをまとめます。

**フラグ:**

| 名前、省略形 | 型 | 必須 | デフォルト | 説明 |
| :------------------- | :----- | :------- | :-------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| -a, --account-number | uint | | | 署名アカウントのアカウント番号（オフラインモードのみ） |
| --aux | | | | txを送信する代わりにaux署名者データを生成する |
| -b, --broadcast-mode | string | | sync | トランザクションブロードキャストモード（sync \| async \| block） |
| --dry-run | | | | --gasフラグを無視してトランザクションのシミュレーションを実行するが、ブロードキャストしない（有効にすると、ローカルキーベースにアクセスできなくなります） |
| --fee-granter | string | | | 手数料支払人がトランザクションの手数料を支払う |
| --fee-payer | string | | | 手数料支払人が署名者から差し引く代わりにトランザクションの手数料を支払う |
| --fees | string | | | トランザクションと一緒に支払う手数料。例：10uatom |
| --from | string | | | 署名する秘密鍵の名前またはアドレス |
| --gas | string | | 200000 | トランザクションごとに設定するガス制限。"auto"に設定すると、十分なガスが自動的に計算されます |
| --gas-adjustment | float | | 1 | txシミュレーションによって返された推定値に乗算される調整係数。ガス制限が手動で設定されている場合、このフラグは無視されます |
| --gas-prices | string | | | トランザクション手数料を決定するための10進形式のガス価格（例：0.1uatom） |
| --generate-only | | | | 未署名のトランザクションをビルドし、STDOUTに書き込む（有効にすると、キー名を提供する場合にのみローカルキーベースにアクセスできます） |
| -h, --help | | | | \<module name>のヘルプ |
| --keyring-backend | string | | test | キーリングのバックエンドを選択する（os \| file \| kwallet \| pass \| test \| memory） |
| --keyring-dir | string | | | クライアントキーリングディレクトリ。省略した場合、デフォルトの「ホーム」ディレクトリが使用されます |
| --ledger | | | | 接続されたLedgerデバイスを使用する |
| --node | string | | tcp://localhost:26657 | このチェーンのtendermint rpcインターフェースへの\<host>:\<port> |
| --note | string | | | トランザクションに説明を追加するためのメモ（以前は--memo） |
| --offline | | | | オフラインモード（オンライン機能は許可されません） |
| -o, --output | string | | json | 出力形式（text \| json） |
| -s, --sequence | uint | | | 署名アカウントのシーケンス番号（オフラインモードのみ） |
| --sign-mode | string | | | 署名モードを選択する（direct \| amino-json \| direct-aux）、これは高度な機能です |
| --timeout-height | uint | | | txが特定の高さを超えてコミットされないようにブロックタイムアウトの高さを設定する |
| --tip | string | | | チップは、ターゲットチェーンの手数料支払人に転送される金額です。このフラグは--auxと一緒に使用する場合にのみ有効で、ターゲットチェーンがTipDecoratorを有効にしていない場合は無視されます |
| -y, --yes | | | | txブロードキャストのプロンプト確認をスキップする |

**グローバルフラグ:**

| 名前、省略形 | 型 | 必須 | デフォルト | 説明 |
| :-------------- | :----- | :------- | :------------- | :---------------------------------------------------------------------------- |
| --chain-id | string | | | ネットワークチェーンID |
| --home | string | | $HOME/.ununifi | 設定とデータのディレクトリ |
| --log_format | string | | | ログ形式（json \| plain）（デフォルトは"plain"） |
| --log_level | string | | info | ログレベル（trace \| debug \| info \| warn \| error \| fatal \| panic） |
| --trace | | | | エラー時に完全なスタックトレースを出力する |

## Tx

### ununifid tx wasm clear-contract-admin

さらなる移行を防ぐためにコントラクトの管理者をクリアする

````bash
ununifid tx wasm clear-contract-admin [contract_addr_bech32] [flags]```
````

**フラグ:**

{% hint style="info" %}
フラグの詳細については、[cosmwasm txの共通フラグ](wasm.md#common-tx-flags)を参照してください。
{% endhint %}

### ununifid tx wasm execute

wasmコントラクトでコマンドを実行する

```bash
ununifid tx wasm execute [contract_addr_bech32] [json_encoded_send_args] --amount [coins,optional] [flags]
```

**フラグ:**

{% hint style="info" %}
フラグの詳細については、[cosmwasm txの共通フラグ](wasm.md#common-tx-flags)を参照してください。
{% endhint %}

### ununifid tx wasm grant

アドレスに承認を付与する

```bash
ununifid tx wasm grant [grantee] [message_type="execution"|"migration"] [contract_addr_bech32] --allow-raw-msgs [msg1,msg2,...] --allow-msg-keys [key1,key2,...] --allow-all-messages [flags]
```

**例:**

```bash
ununifid tx grant <grantee_addr> execution <contract_addr> --allow-all-messages --max-calls 1 --no-token-transfer --expiration 1667979596

ununifid tx grant <grantee_addr> execution <contract_addr> --allow-all-messages --max-funds 100000uwasm --expiration 1667979596

ununifid tx grant <grantee_addr> execution <contract_addr> --allow-all-messages --max-calls 5 --max-funds 100000uwasm --expiration 1667979596
```

**フラグ:**

{% hint style="info" %}
フラグの詳細については、[cosmwasm txの共通フラグ](wasm.md#common-tx-flags)を参照してください。
{% endhint %}

### ununifid tx wasm instantiate

アップロードされたwasmコードの新しいインスタンスを、指定された「コンストラクタ」メッセージで作成します。
各コントラクトインスタンスには、一意のアドレスが割り当てられます。

```bash
ununifid tx wasm instantiate [code_id_int64] [json_encoded_init_args] --label [text] --admin [address,optional] --amount [coins,optional] [flags]
```

**例:**

```bash
$ ununifid tx wasm instantiate 1 '{"foo":"bar"}' --admin="$(ununifid keys show mykey -a)" \
  --from mykey --amount="100ustake" --label "local0.1.0"
```

**フラグ:**

{% hint style="info" %}
フラグの詳細については、[cosmwasm txの共通フラグ](wasm.md#common-tx-flags)を参照してください。
{% endhint %}

### ununifid tx wasm instantiate2

アップロードされたwasmコードの新しいインスタンスを、指定された「コンストラクタ」メッセージで作成します。
各コントラクトインスタンスには、一意のアドレスが割り当てられます。それらは自動的に割り当てられますが、特別なユースケースのために予測可能なアドレスを持つために、指定された「salt」引数と「--fix-msg」パラメータを使用してカスタムアドレスを生成できます。

```bash
ununifid tx wasm instantiate2 [code_id_int64] [json_encoded_init_args] [salt] --label [text] --admin [address,optional] --amount [coins,optional] --fix-msg [bool,optional] [flags]
```

**予測可能なアドレスの例（「ununifid query wasm build-address -h」も参照してください）：**

```bash
$ ununifid tx wasm instantiate2 1 '{"foo":"bar"}' $(echo -n "testing" | xxd -ps) --admin="$(ununifid keys show mykey -a)" \
  --from mykey --amount="100ustake" --label "local0.1.0" \
   --fix-msg
```

**フラグ:**

{% hint style="info" %}
フラグの詳細については、[cosmwasm txの共通フラグ](wasm.md#common-tx-flags)を参照してください。
{% endhint %}

### ununifid tx wasm migrate

wasmコントラクトを新しいコードバージョンに移行する

```bash
ununifid tx wasm migrate [contract_addr_bech32] [new_code_id_int64] [json_encoded_migration_args] [flags]
```

**フラグ:**

{% hint style="info" %}
フラグの詳細については、[cosmwasm txの共通フラグ](wasm.md#common-tx-flags)を参照してください。
{% endhint %}

### ununifid tx wasm set-contract-admin

コントラクトの新しい管理者を設定する

```bash
ununifid tx wasm set-contract-admin [contract_addr_bech32] [new_admin_addr_bech32] [flags]
```

**フラグ:**

{% hint style="info" %}
フラグの詳細については、[cosmwasm txの共通フラグ](wasm.md#common-tx-flags)を参照してください。
{% endhint %}

### ununifid tx wasm store

wasmバイナリをアップロードする

```bash
ununifid tx wasm store [wasm file] [flags]
```

**フラグ:**

{% hint style="info" %}
フラグの詳細については、[cosmwasm txの共通フラグ](wasm.md#common-tx-flags)を参照してください。
{% endhint %}

### ununifid tx wasm update-instantiate-config

codeIDのインスタンス化設定を更新する

```bash
ununifid tx wasm update-instantiate-config [code_id_int64] [flags]
```

**フラグ:**

{% hint style="info" %}
フラグの詳細については、[cosmwasm txの共通フラグ](wasm.md#common-tx-flags)を参照してください。
{% endhint %}
