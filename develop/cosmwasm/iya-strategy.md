# Strategy contracts for Interchain Yield Aggregator

Development requires the knowledge of [CosmWasm](../cosmwasm.md).

## Basic idea

The `yieldaggregator` module on UnUniFi can call a functionality of the smart contracts that are registered as a **Strategy**.
When users deposit their funds into the **Vault** on `yieldaggregator` module, the module will automatically allocate the funds to strategies that are contained in the **Vault**.
Strategy contracts have to follow the interface described below.

## ExecuteMsg

```rust
    pub enum ExecuteMsg {
        Stake(StakeMsg),
        Unstake(UnstakeMsg),
    }

    #[derive(Serialize, Deserialize, Clone, Debug, PartialEq, JsonSchema)]
    pub struct StakeMsg {}

    #[derive(Serialize, Deserialize, Clone, Debug, PartialEq, JsonSchema)]
    pub struct UnstakeMsg {
        pub amount: Uint128,
    }
```

### `ExecuteMsg::Stake`

On `ExecuteMsg::Stake`, staking amount is configured on `info.funds`

### `ExecuteMsg::Unstake`

On `ExecuteMsg::Unstake`, unstaking amount is put Uint128 variable on `UnstakeMsg`

## QueryMsg

````rust
    pub enum QueryMsg {
        Bonded { addr: String },
        Unbonding { addr: String },
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

`QueryMsg::Unbonding` needs no info for querying.

This query returns `FeeInfo` object that contains information of fees.

```rust
pub struct FeeInfo {
    pub deposit_fee_rate: Decimal,
    pub withdraw_fee_rate: Decimal,
    pub interest_fee_rate: Decimal,
}
```

Developers who developed strategy contracts have to implement this query properly, to show how much fees are charged on the strategy to users.
Otherwise, the proposal for registering the strategy will be rejected.

## Proposal

Under construction.
