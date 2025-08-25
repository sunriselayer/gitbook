# RISEの自己委任

バリデーターは、ステーキング報酬を得るためにRISEを自己委任することができます。

{% hint style="warning" %}
**注**: vRISEの委任とは異なり、RISEを委任してもガバナンスの投票権は付与されません。
{% endhint %}

RISEを委任する方法は、トークンが通常のウォレット残高にあるか、ロックアップアカウントにあるかによって異なります。それぞれの場合で使用するモジュールとコマンドは異なります。

---

## 通常の残高からの委任（`x/shareclass`）

ウォレットに直接保有されているRISEを委任するには、`x/shareclass`モジュールの`non-voting-delegate`コマンドを使用します。

### 委任方法

**使用法:**

```bash
sunrised tx shareclass non-voting-delegate [validator_address] [amount] [flags]
```

**例:**

```bash
# バリデーターアドレスを取得
VALIDATOR_ADDRESS=$(sunrised keys show <your_validator_key> --bech val -a)

# 委任を実行
sunrised tx shareclass non-voting-delegate $VALIDATOR_ADDRESS 10000000urise \
    --from <your_validator_key> \
    --chain-id <your_chain_id> \
    --gas-prices=0.025uusdrise --gas-adjustment 1.2 \
    --gas=auto \
    -y
```

### 報酬の請求方法

`x/shareclass`モジュールの`claim-rewards`コマンドを使用して、蓄積されたステーキング報酬を請求します。報酬はウォレットに送られます。

**使用法:**

```bash
sunrised tx shareclass claim-rewards [validator_address] [flags]
```

**例:**

```bash
VALIDATOR_ADDRESS=$(sunrised keys show <your_validator_key> --bech val -a)

sunrised tx shareclass claim-rewards $VALIDATOR_ADDRESS \
    --from <your_validator_key> \
    --chain-id <your_chain_id> \
    --gas-prices=0.025uusdrise --gas-adjustment 1.2 \
    --gas=auto \
    -y
```

---

## ロックアップアカウントからの委任（`x/lockup`）

ロックアップの一部であるRISE（例：エアドロップから）を委任するには、`x/lockup`モジュールを使用する必要があります。

### 1. ロックアップアカウントIDを見つける

まず、委任したいロックアップアカウントのIDを特定する必要があります。`lockup-accounts`クエリを使用して、キーが所有するすべてのロックアップアカウントを一覧表示できます。

**使用法:**

```bash
sunrised query lockup lockup-accounts [owner] [flags]
```

**例:**

```bash
OWNER_ADDRESS=$(sunrised keys show <your_validator_key> -a)

sunrised query lockup lockup-accounts $OWNER_ADDRESS --output json
```

このコマンドの出力から、正しいアカウントを見つけてその`id`をメモします。

### 2. 委任方法

ロックアップアカウントIDを取得したら、`x/lockup`モジュールの`non-voting-delegate`コマンドを使用します。

**使用法:**

```bash
sunrised tx lockup non-voting-delegate [lockup_account_id] [validator_address] [amount] [flags]
```

**例:**

```bash
LOCKUP_ID="<your_lockup_account_id>"
VALIDATOR_ADDRESS=$(sunrised keys show <your_validator_key> --bech val -a)

sunrised tx lockup non-voting-delegate $LOCKUP_ID $VALIDATOR_ADDRESS 10000000urise \
    --from <your_validator_key> \
    --chain-id <your_chain_id> \
    --gas-prices=0.025uusdrise --gas-adjustment 1.2 \
    --gas=auto \
    -y
```

### 3. 報酬の請求方法

`x/lockup`モジュールの`claim-rewards`コマンドを使用します。

{% hint style="info" %}
**重要**: ロックアップ委任から請求された報酬は、メインウォレットではなく、ロックアップアカウント自体に送り返されます。報酬のRISE部分は、元のロックアップスケジュールに従います。
{% endhint %}

**使用法:**

```bash
sunrised tx lockup claim-rewards [lockup_account_id] [flags]
```

**例:**

```bash
LOCKUP_ID="<your_lockup_account_id>"

sunrised tx lockup claim-rewards $LOCKUP_ID \
    --from <your_validator_key> \
    --chain-id <your_chain_id> \
    --gas-prices=0.025uusdrise --gas-adjustment 1.2 \
    --gas=auto \
    -y
```

---

## Sunriseアプリの使用

これらの委任および報酬請求操作は、**Sunriseアプリ**インターフェースを介して簡単に行うこともできます。

詳細については、次のドキュメントを参照してください。

- **通常の委任の場合:** [ガバナンス](../../learn/sunrise-app/gov.md)
- **ロックされた資産の委任の場合:** [ロックアップ](../../learn/sunrise-app/lockup.md)
