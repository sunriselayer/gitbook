# External CosmWasm chain with IBCHooks

This doesn't require `QueryMsg`, but requires `ExecuteMsg` as well as Strategy contract described [here](https://github.com/UnUniFi/gitbook/blob/main/develop/iya-strategy/strategy.md)

```rust
#[cw_serde]
pub enum ExecuteMsg {
    Stake(StakeMsg),
    Unstake(UnstakeMsg),
    Epoch(EpochMsg),
}

#[cw_serde]
pub struct StakeMsg {}

#[cw_serde]
pub struct UnstakeMsg {
    pub amount: Uint128,
}

#[cw_serde]
pub struct EpochMsg {}
```
