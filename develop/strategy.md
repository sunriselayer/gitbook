# Strategy Contract for UnUniFi Yield Aggregator

All developer can deploy their created Strategy contracts to the UnUniFi protocol without permission.

Yield aggregator is expecting following endpoints to be exposed by strategy contract.

## Message

```rs
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

### Stake

On `Stake`, staking amount is configured on `info.funds`

### Unstake

On `Unstake`, unstaking amount is put Uint128 variable on `UnstakeMsg`

## Query

````rs
    pub enum QueryMsg {
        Bonded { addr: String },
        Unbonding { addr: String },
        Fee {},
    }
````

### Bonded

`Bonded` returns the value of `addr`'s bonded tokens.
Here `addr` is the address of vault, or individual addresses that deposit funds to the strategy.

### Unbonding

`Unbonding` returns the value of `addr`'s unbonding tokens.
Here `addr` is the address of vault, or individual addresses that deposit funds to the strategy.

### Fee

`Fee` returns `FeeInfo` object that has configuration of fees.

```rs
pub struct FeeInfo {
    pub deposit_fee_rate: Decimal,
    pub withdraw_fee_rate: Decimal,
    pub interest_fee_rate: Decimal,
}
```