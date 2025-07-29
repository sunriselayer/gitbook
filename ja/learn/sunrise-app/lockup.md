# Lockup

The Lockup feature is for managing tokens that have been distributed through airdrops or other incentive programs and are locked for a specific period. These tokens are progressively unlocked over the set duration.

## Lockup Overview

On the main "Lockup" page, you can see a list of all your lockup accounts. Each account displays details of the locked assets and the lockup period.

Clicking on an item in the list will take you to the details page for that lockup account.

## Lockup Account Details

The details page provides a comprehensive view of the current state of your locked assets.

- **Original/Additional Locking**: The original and any additional amounts of the lockup.
- **Lockup Start/End**: The date and time when the lockup started and when it will fully end.
- **Currently Locked/Unlocked**: A breakdown of currently locked and unlocked assets.
- **Delegated (Locked/Unlocked)**: A breakdown of the assets being staked, showing both locked and unlocked portions.

From this page, you can perform three main actions related to your lockup account.

### 1. Staking Locked Assets (Delegate)

You can delegate your locked RISE to a validator to earn staking rewards.

{% hint style="danger" %}
**Important**: While you can earn staking rewards from delegating via a lockup account, this **does not grant you voting power** in Governance Proposals or Gauge Voting.
{% endhint %}

- **How to operate**: Select "Delegate" on the lockup details page, choose a validator and amount, and delegate your assets.

### 2. Managing Delegations

Check the status of and manage your currently delegated assets.

- **Claim Rewards**: Manually claim the accrued staking rewards and return them to your lockup account.
- **Undelegate**: Unstake your assets.
  - Undelegated tokens do not become available immediately; they enter an **unbonding period** (a waiting period).
  - You can check the status of your unbonding assets on the "Pending Unstake" page.

### 3. Withdrawing Unlocked Assets

You can withdraw assets that have completed their lockup period and are not delegated to your main wallet.

- **Withdrawal Conditions**: You can only withdraw assets that are both **unlocked** and **not delegated**.
- **To withdraw delegated assets**: You must first undelegate them and wait for the unbonding period to end. After the period is over, the assets will become available for withdrawal.
- **How to operate**: Select "Withdraw" on the lockup details page and enter the amount of unlocked assets you wish to withdraw.
