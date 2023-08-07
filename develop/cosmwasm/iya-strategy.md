# Strategy contracts for Interchain Yield Aggregator

Development requires the knowledge of [CosmWasm](../cosmwasm.md).

## Basic idea

The `yieldaggregator` module on UnUniFi can call a functionality of the smart contracts that are registered as a **Strategy**.
When users deposit their funds into the **Vault** on `yieldaggregator` module, the module will automatically allocate the funds to strategies that are contained in the **Vault**.
Strategy contracts have to follow the interface described below.

## ExecuteMsg

```rust
#[cw_serde]
pub enum ExecuteMsg {
    Stake(StakeMsg),
    Unstake(UnstakeMsg),
    ExecuteEpoch(ExecuteEpochMsg),
}

#[cw_serde]
pub struct StakeMsg {}

#[cw_serde]
pub struct UnstakeMsg {
    pub amount: Uint128,
}

#[cw_serde]
pub struct ExecuteEpochMsg {}

```

### `ExecuteMsg::Stake`

On `ExecuteMsg::Stake`, staking amount is configured on `info.funds`.

### `ExecuteMsg::Unstake`

On `ExecuteMsg::Unstake`, unstaking amount is put as `Uint128` variable on `UnstakeMsg`.

### `ExecuteMsg::ExecuteEpoch`

On `ExecuteMsg::ExecuteEpoch`, the strategy contract has to execute the periodical process of the strategy. For example, auto compounding.

This Msg is called by `yieldaggregator` module periodically.
However, this Msg can be called by anyone (because this is not `SudoMsg`), so the strategy contract must not implement logics that can be abused by malicious users.

## QueryMsg

````rust
#[cw_serde]
#[derive(QueryResponses)]
pub enum QueryMsg {
    #[returns(BondedResp)]
    Bonded { addr: String },
    #[returns(UnbondingResp)]
    Unbonding { addr: String },
    #[returns(FeeResp)]
    Fee {},
}
````

### `QueryMsg::Bonded`

`QueryMsg::Bonded` needs following info for querying:

- `addr`: address of the **Vault** that deposit funds to the strategy.

This query returns the amount of bonded tokens of the address.

### Unbonding

`QueryMsg::Unbonding` needs following info for querying:

- `addr`: address of the **Vault** that deposit funds to the strategy.

This query returns the amount unbonding tokens of the address.

### `QueryMsg::Fee`

`QueryMsg::Fee` needs no info for querying.

This query returns `FeeResp` object that contains information of fees.

```rust
pub struct FeeResp {
    pub deposit_fee_rate: Decimal,
    pub withdraw_fee_rate: Decimal,
    pub interest_fee_rate: Decimal,
}
```

Developers who developed strategy contracts have to implement this query properly, to show how much fees are charged on the strategy to users.
Otherwise, the proposal for registering the strategy will be rejected.

### Source codes

- <https://github.com/UnUniFi/contracts/blob/main/packages/strategy/src/v0/msgs.rs>

## Proposal

Under construction.
