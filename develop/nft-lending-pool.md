# NFT Lending Pool

{% hint style="warn" %}
This feature is Under construction.
{% endhint %}

## Interface

The program of the pool can be written as CosmWasm smart contract by third party developers:

```rust
#[cw_serde]
#[derive(QueryResponses)]
pub enum QueryMsg {
    #[returns(DenomResp)]
    Denom {},
    #[returns(LoanLimitResp)]
    LoanLimit {
        class_id: String,
        token_id: String,
        period: Duration,
    },
}

#[cw_serde]
pub struct DenomResp {
    denom: String,
}

#[cw_serde]
pub struct LoanLimitResp {
    amount: Uint128,
    annual_interest_rate: Decimal,
}
```
