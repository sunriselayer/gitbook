# Lockup Account

The `x/lockupaccount` module is a protocol-level mechanism for managing locked tokens within the Sunrise ecosystem. It provides a flexible and efficient way to lock tokens for various purposes, ensuring sustainable protocol economics while maintaining user accessibility.

## Key Features

- **Protocol-Level Locking:** Centralized lock management at the protocol level
- **Flexible Lock Types:** Support for different types of token locks
- **Time-Based Locks:** Configurable lock durations
- **Economic Sustainability:** Ensures long-term protocol viability

## Core Functionality

> **Note:** The following section covers advanced topics intended for experienced users or developers.

### Lock Management

The module manages different types of locks:

- **Time Locks:** For time-based token locking
- **Vesting Locks:** For token vesting schedules
- **Conditional Locks:** For condition-based token locking
- **Custom Locks:** For protocol-specific locking mechanisms

### Lock Operations

Locks can be managed through:

- Lock creation
- Lock extension
- Lock release
- Lock modification

### Integration with Other Modules

The module integrates with:

- **x/liquidityincentive:** For liquidity reward locking
- **x/gauges:** For gauge voting power locking
- **x/governance:** For governance power locking
- **x/fee:** For fee payment locking

## Integration Points

### With Other Modules

- **x/liquidityincentive:** For liquidity reward integration
- **x/gauges:** For gauge voting integration
- **x/governance:** For governance integration
- **x/fee:** For fee payment integration

### With External Systems

- **Wallets:** For lock management
- **Staking Platforms:** For staking lock integration
- **Analytics:** For lock performance tracking

## Parameters

The module's behavior is controlled by several parameters:

- `min_lock_duration`: Minimum duration for locks
- `max_lock_duration`: Maximum duration for locks
- `min_lock_amount`: Minimum amount for locks
- `max_lock_amount`: Maximum amount for locks
- `lock_types`: Supported lock types

## Example Usage

### Creating a Lock

```go
// Create a new time lock
lock := types.Lock{
    Id:          "lock-1",
    Type:        types.LockTypeTime,
    Owner:       owner,
    Amount:      amount,
    StartTime:   ctx.BlockTime(),
    EndTime:     ctx.BlockTime().Add(lockDuration),
    IsActive:    true,
}

err := k.CreateLock(ctx, lock)
if err != nil {
    return err
}
```

### Extending a Lock

```go
// Extend an existing lock
extension := types.LockExtension{
    LockId:      "lock-1",
    NewEndTime:  ctx.BlockTime().Add(newDuration),
}

err := k.ExtendLock(ctx, extension)
if err != nil {
    return err
}
```

### Releasing a Lock

```go
// Release a lock
err := k.ReleaseLock(ctx, "lock-1")
if err != nil {
    return err
}
```

## Benefits

1. **Flexible Locking:** Support for various lock types
2. **Time-Based Control:** Configurable lock durations
3. **Sustainable Economics:** Long-term protocol viability
4. **Transparent Operations:** Clear lock management
5. **Protocol Integration:** Seamless integration with other components

## Future Improvements

1. **Dynamic Lock Parameters:** Implement dynamic parameters based on market conditions
2. **Advanced Lock Types:** Support for more complex locking mechanisms
3. **Cross-Chain Locks:** Enable cross-chain token locking
4. **Lock Analytics:** Better tracking and analysis of lock performance
5. **User Preferences:** Allow users to set preferences for lock management

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
