# 戦略コントラクトインターフェース

戦略コントラクトは、以下に説明する特定のインターフェースを満たします。

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

`ExecuteMsg::Stake`では、ステーキング額は`info.funds`で設定されます。

### `ExecuteMsg::Unstake`

`ExecuteMsg::Unstake`では、アンステーキング額は`UnstakeMsg`の`Uint128`変数として入力されます。

### `ExecuteMsg::ExecuteEpoch`

`ExecuteMsg::ExecuteEpoch`では、戦略コントラクトは戦略の定期的なプロセスを実行する必要があります。たとえば、自動複利です。

このMsgは`yieldaggregator`モジュールによって定期的に呼び出されます。
ただし、このMsgは誰でも呼び出すことができるため（これは`SudoMsg`ではないため）、戦略コントラクトは悪意のあるユーザーによって悪用される可能性のあるロジックを実装してはなりません。

## QueryMsg

```rust
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
```

### `QueryMsg::Bonded`

`QueryMsg::Bonded`は、クエリに次の情報を必要とします。

- `addr`: 戦略に資金を入金する**Vault**のアドレス。

このクエリは、アドレスのボンドされたトークンの量を返します。

### Unbonding

`QueryMsg::Unbonding`は、クエリに次の情報を必要とします。

- `addr`: 戦略に資金を入金する**Vault**のアドレス。

このクエリは、アドレスのアンボンディング中のトークンの量を返します。

### `QueryMsg::Fee`

`QueryMsg::Fee`は、クエリに情報を必要としません。

このクエリは、手数料の情報を含む`FeeResp`オブジェクトを返します。

```rust
pub struct FeeResp {
    pub deposit_fee_rate: Decimal,
    pub withdraw_fee_rate: Decimal,
    pub interest_fee_rate: Decimal,
}
```

戦略コントラクトを開発した開発者は、戦略で請求される手数料の額をユーザーに示すために、このクエリを適切に実装する必要があります。
そうしないと、戦略の登録に関する提案は拒否されます。

### ソースコード

- <https://github.com/UnUniFi/contracts/blob/main/packages/strategy/src/v0/msgs.rs>
