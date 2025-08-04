# Self-Delegating RISE

Validators can self-delegate RISE to themselves to earn staking rewards.

{% hint style="warning" %}
**Note**: Unlike delegating vRISE, delegating RISE does not grant any governance voting power.
{% endhint %}

The method for delegating RISE differs depending on whether the tokens are in a regular wallet balance or a lockup account. The module and command used will be different for each case.

---

## Delegating from a Regular Balance (`x/shareclass`)

To delegate RISE held directly in your wallet, use the `non-voting-delegate` command from the `x/shareclass` module.

### How to Delegate

**Usage:**

```bash
sunrised tx shareclass non-voting-delegate [validator_address] [amount] [flags]
```

**Example:**

```bash
# Get validator address
VALIDATOR_ADDRESS=$(sunrised keys show <your_validator_key> --bech val -a)

# Execute delegation
sunrised tx shareclass non-voting-delegate $VALIDATOR_ADDRESS 10000000urise \
    --from <your_validator_key> \
    --chain-id <your_chain_id> \
    --gas-prices=0.025uusdrise --gas-adjustment 1.2 \
    --gas=auto \
    -y
```

### How to Claim Rewards

Use the `claim-rewards` command from the `x/shareclass` module to claim your accumulated staking rewards. The rewards will be sent to your wallet.

**Usage:**

```bash
sunrised tx shareclass claim-rewards [validator_address] [flags]
```

**Example:**

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

## Delegating from a Lockup Account (`x/lockup`)

To delegate RISE that is part of a lockup (e.g., from an airdrop), you must use the `x/lockup` module.

### 1. Find Your Lockup Account ID

First, you need to identify the ID of the lockup account you wish to delegate from. You can list all lockup accounts owned by your key using the `lockup-accounts` query.

**Usage:**

```bash
sunrised query lockup lockup-accounts [owner] [flags]
```

**Example:**

```bash
OWNER_ADDRESS=$(sunrised keys show <your_validator_key> -a)

sunrised query lockup lockup-accounts $OWNER_ADDRESS --output json
```

From the output of this command, find the correct account and note its `id`.

### 2. How to Delegate

Once you have the lockup account ID, use the `non-voting-delegate` command from the `x/lockup` module.

**Usage:**

```bash
sunrised tx lockup non-voting-delegate [lockup_account_id] [validator_address] [amount] [flags]
```

**Example:**

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

### 3. How to Claim Rewards

Use the `claim-rewards` command from the `x/lockup` module.

{% hint style="info" %}
**Important**: Rewards claimed from a lockup delegation are sent back to the lockup account itself, not your main wallet. The RISE portion of the rewards will be subject to the original lockup schedule.
{% endhint %}

**Usage:**

```bash
sunrised tx lockup claim-rewards [lockup_account_id] [flags]
```

**Example:**

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

## Using the Sunrise App

These delegation and reward claiming operations can also be performed easily through the **Sunrise App** interface.

For more details, please refer to the following documents:

- **For regular delegation:** [Governance](../../learn/sunrise-app/gov.md)
- **For delegating locked assets:** [Lockup](../../learn/sunrise-app/lockup.md)
