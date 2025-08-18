# Governance

Sunrise's governance system allows you to contribute to the network's security and participate in shaping the protocol's future by staking (delegating) your vRISE or RISE tokens.

There are two main aspects to governance:

* **Governance Proposals**: Chain-wide decisions such as protocol upgrades, parameter changes, and use of community pool funds.
* **Gauge Voting**: Voting to determine the allocation of incentives (vRISE emissions) to liquidity pools.

{% hint style="info" %}
**Important**: To get voting power in both Governance Proposals and Gauge Voting, you must stake **vRISE**. Staking RISE does not grant voting power, but you will still earn staking rewards.
{% endhint %}

## Staking (Delegation)

You can earn staking rewards by delegating your tokens to a validator. The characteristics of delegating differ between vRISE and RISE.

| Feature             | 　![vRISE](../../.gitbook/assets/vRISE.png) vRISE | ![RISE](../../.gitbook/assets/RISE.png) RISE |
| ------------------- | ------------------------------------------------ | -------------------------------------------- |
| **Voting Power**    | Yes (Proposals & Gauges)                         | No                                           |
| **Staking Rewards** | Yes (Auto-compounding)                           | Yes (Manual claim)                           |
| **Transferability** | No                                               | Yes                                          |
| **Redelegation**    | Yes                                              | No                                           |

### How to Stake

1. Click the "Stake" button on the Governance page or navigate to the "Delegate" page.
2. Select the "vRISE" or "RISE" tab.
3. Choose a validator to delegate to from the list.
4. Enter the amount of tokens you want to delegate and approve the transaction.

{% hint style="warning" %}
To stake locked RISE, you must do so from the [**Lockup**](lockup.md) page, not this one. Please refer to the "Lockup" documentation for details.
{% endhint %}

### Managing Your Delegations

On the "Delegations" page, you can manage your current delegated positions.

* **vRISE**:
  * **Rewards**: Rewards are automatically compounded into your staked position, so no manual claim is necessary.
  * **Redelegate**: Instantly switch your delegation to another validator without unstaking.
  * **Undelegate**: Unstake your delegation. There is an unbonding period before the tokens become available.
* **RISE**:
  * **Claim Rewards**: Manually claim your accrued staking rewards, which will be sent to your wallet.
  * **Undelegate**: Unstake your delegation. Like vRISE, an unbonding period applies.

You can check the status of your unbonding delegations on the "Pending Unstake" page within the "Delegations" section.

## Governance Proposals

Important protocol decisions, such as chain parameter changes or the use of community funds, are made through governance proposals.

### Viewing and Voting on Proposals

1. On the "Proposals" page, you can see a list of current and past proposals.
2. Click on a proposal to view its details, current voting status (percentage of Yes, No, Abstain votes), and the voting period.
3. If a proposal is in its voting period, you can cast your vote using your voting power (based on your staked vRISE amount). The voting options are:
   * **Yes**
   * **No**
   * **Abstain**
   * **No With Veto**: A strong "No" vote that can override a proposal and burn the deposit.

## Gauge Voting

Gauge Voting is the mechanism for deciding how vRISE incentives are allocated to the various liquidity pools in the next epoch.

### How Gauge Voting Works

* **Voting Power**: Your voting power is determined by the amount of vRISE you have staked.
* **Voting**: On the "Your Vote" page in the "Gauge Voting" section, you can allocate your voting power to different liquidity pools by percentage. The total must add up to 100%.
* **Epochs**: Voting occurs in periods called epochs. When a new epoch begins, the vRISE reward distribution rate for each pool is determined based on the voting results.

### Bribes

Bribes are incentives offered to encourage users to vote for a specific pool.

* **Offering a Bribe**: Users can offer a bribe (e.g., in RISE) for a specific pool to attract votes. This can be done from the "Register Bribe" page in the "Bribes" section.
* **Earning Bribes**: Users who vote for a pool with bribes will earn a share of those bribes, proportional to their voting power cast on that pool. Bribes can be claimed from the "Claimable" page in the "Bribes" section.
