# IBCHooksを使用した外部CosmWasmチェーン

これは`QueryMsg`を必要としませんが、[こちら](https://github.com/UnUniFi/gitbook/blob/main/develop/iya-strategy/strategy.md)で説明されている戦略コントラクトと同様に`ExecuteMsg`を必要とします。

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
