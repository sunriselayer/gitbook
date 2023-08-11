# NFT Lending Pool

{% hint style="warn" %}
This feature is Under construction.
{% endhint %}

## Basic idea

`nftbackedloan` modules serves an original algorithm that is different from simple Peer-to-Peer lending. It solves the problem of simple Peer-to-Peer lending that it takes a long time to find a lender who is willing to lend the exact amount of money that the borrower wants to borrow, while the merit of Peer-to-Peer lending is preserved. For example, we don't need to depend on any oracles.

However, thanks to the algorithm, the module can integrate the element of Peer-to-Pool lending.
Though Peer-to-Pool lending depends on oracles, it can reduce the user operations.

By combining the two elements, the module can provide a new type of lending service.

The program of the pool can be written as CosmWasm smart contract by third party developers:

```rust
#[cw_serde]
#[derive(QueryResponses)]
pub enum QueryMsg {
    #[returns(DenomResp)]
    Denom { },
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
}
```
