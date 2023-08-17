# Strategy contracts interface on External CosmWasm IBC Hooks chain

This doesn't require `QueryMsg`, but requires `ExecuteMsg` as well as Strategy contract described [here](./strategy.md)

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
