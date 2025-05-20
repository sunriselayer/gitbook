# Lockup Account

In Sunrise mainnet, Airdrops and other funds granted by Genesis are locked for a certain period of time.
This will be unlocked gradually over time and can be sent to other accounts.

## Lockup Account Types

In Sunrise, the following lock-up accounts are exist

1. [continuous-locking-account](https://docs.cosmos.network/v0.52/build/modules/auth/vesting#continuously-vesting-accounts)
1. [delayed-locking-account](https://docs.cosmos.network/v0.52/build/modules/auth/vesting#continuously-vesting-accounts)
1. [periodic-locking-account](https://docs.cosmos.network/v0.52/build/modules/auth/vesting#continuously-vesting-accounts)
1. permanent-locking-account

- ContinuousLocking: A lockup account implementation that vests coins linearly over time.
- DelayedLocking: A lockup account implementation that only fully vests all coins at a given time.
- PeriodicLocking: A lockup account implementation that vests coins according to a custom lockup schedule.
- PermanentLocking: It does not ever release coins, locking them indefinitely. Coins in this account can still be used for delegating and for governance votes even while locked.

Basically, continuous-locking-account is used. The lock funds is gradually unlocked over time.

## Self Delegatable Lockup Account

In Sunrise, `seld-delegatable` is prefixed, as in `seld-delegatable-continuous-locking-account`. This means that self-delegating, a feature for validators, is available. See [Self Delegation](../../build/validators/self-delegation.md) for more details.

## Excute Tx

The following Txs are supported with lockup accounts

1. MsgSend
<!-- 1. MsgDelegate
1. MsgUndelegate
1. MsgWithdrawReward -->

MsgSend can move unlocked funds to other accounts.
<!-- MsgDelegate can also delegate locked funds.
MsgWithdrawReward can claim the delegation reward to the validator. The reward is added to the lockup account and is subject to lockup. -->

You can see the status of your lockup account by searching your account in [Risescan](https://risescan.sunriselayer.io). If you want to retrieve your lockup balance, go to [Sunrise App](https://app.sunriselayer.io/accounts/lockup) and send this tx.

On CLI, use

```bash
sunrised tx accounts execute [lockup-account-address] sunrise.accounts.self_delegatable_lockup.v1.MsgSend "{\"sender\":<owner-account-address>,\"to_address\":<recipient-account-address>,\"amount\":[{\"amount\":\"4000\", \"denom\":\"urise\"}]}" [flags]
```

## Query

Use `x/selfdelegation` query and find your lockup accounts.

```bash
sunrised q selfdelegation lockup-accounts-by-owner [your-address]
```

The following queries are supported with lockup accounts

1. QueryLockupAccountInfoRequest
1. QuerySpendableAmountRequest

Sunrise App & Risescan supports to display these info.
On CLI, use

```bash
sunrised query accounts query [lockup-account-address] [query-request-type-url] [json-message] [flags]
```
