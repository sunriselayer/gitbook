# Sunrise Point Program

A sustainable, multi-layered point system rewarding long-term alignment with the Sunrise ecosystem.

## Program Overview

Sunrise Point Program rewards users across multiple dimensions:

### Daily Activities

- Staking vRISE
- Providing Liquidity (LP)

### Ongoing (Up to specific time)

- Referring new users

### One-time Actions

- Connecting EVM wallet
- Connecting X (Twitter)

---

## Daily: vRISE Staking

Claim your staking points once every 24 hours. Points are calculated based on your current staking amount.

{% hint style="info" %}
Acquiring vRISE requires providing liquidity.
{% endhint %}

**Formula: `1 vRISE = 100 points / day`**

{% hint style="info" %}
Only delegations to `Bonded` validators are eligible. If the validator you are delegating to becomes unbonded, you can redelegate to another `Bonded` validator to continue earning points.
{% endhint %}

The dashboard shows:

- Your available points to claim
- Your current staked amount
- Your staking distribution across validators
- The remaining cooldown timer

## Daily: Liquidity Provision (LP)

Claim your LP points once every 24 hours. Points are based on your active LP positions.

{% hint style="info" %}
Creating a position with RISE will be possible after the RISE token is launched through the Token Generation Event (TGE).
{% endhint %}

{% hint style="info" %}
An LP position is considered `active` or `valid` when the current price is within the price range you set for the position. Invalid positions do not earn points.
{% endhint %}

### Point Calculation

Points are calculated based on the USD value of your liquidity.

- **RISE LP**: `1 USD equivalent = 120 points`
- **Other LP (with RISE)**: `1 USD equivalent = 100 points`
- **USDrise / USDN LP**: `1 USD equivalent = 140 points` (bonus multiplier)

The dashboard shows:

- Your claimable LP points
- Your active LP balance
- Your valid vs. invalid positions
- The remaining cooldown timer

---

## Referral Program

### How It Works

- Share your unique referral link to earn additional points.
- You earn **10% of your referee’s points** each time they make a successful claim.
- Referral bonuses are calculated and awarded independently for each referee.

### Referral Cap

{% hint style="info" %}
There is a limit to the number of users you can invite. No points can be earned from users invited beyond this limit. The cap is updated at regular intervals.
{% endhint %}

---

## NFT Holder Boost

{% hint style="warning" %}
This feature is planned for a future update and is not yet active.
{% endhint %}

Holding a specific NFT provides a boost to your earnings.

### With NFT

- Your daily points are multiplied: `Daily points × (1 + x%)`
- Your referral bonus also receives this boost.
- **Example**: 1,000 vRISE staking points with a 10% boost: `1,000 vRISE × 100 pt × 1.1 = 110,000 points`

### Without NFT

- You earn the base rate of points with no multipliers.
- Your referral bonus is calculated from your referee's base points only.

### Referral Boost Scenarios

**Scenario 1: Neither you (referrer) nor your referee has an NFT**

- **You (A)**: Your base points + 10% of referee (B)'s base staking/LP points.
- **Referee (B)**: Base rewards only.

**Scenario 2: Only you (referrer) have an NFT**

- **You (A)**: `(Your base points × (1 + x%))` + `10% of referee (B)'s base staking/LP points`.
- **Referee (B)**: Base rewards only.

**Scenario 3: Both you (referrer) and your referee have an NFT**

- **You (A)**: `(Your base points × (1 + x%))` + `10% of (referee (B)'s base points × (1 + x%))`.
- **Referee (B)**: `(Their base points × (1 + x%))`.

---

## One-time Bonuses

Earn a one-time point bonus for connecting your accounts.

- **EVM Wallet Connection**: `+500 points`
  - This connection is required for the NFT Holder Boost.
- **X (Twitter) Connection**: `+100 points`
  - This is also required for participation in upcoming retweet campaigns.

---

## Claim Rules

- All point claims are manual and must be initiated by you.
- Each category (Staking, LP) has its own 24-hour cooldown period after a claim.
- You can continue staking, providing liquidity, and referring during cooldown periods.
- Points are calculated at the moment you click the "Claim" button.
