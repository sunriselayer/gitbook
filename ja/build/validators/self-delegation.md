# セルフデリゲーション

バリデータは、自身に$RISEをステーキングすることで議決権（Voting Power）を増やすことができます。この機能は、MsgCreateValidatorなどでバリデータとして登録されたアドレスのみが利用できます。

## x/selfdelegation Msg

1. MsgSelfDelegate
1. MsgWithdrawSelfDelegationUnbonded

- MsgSelfDelegate
セルフデリゲーションプロキシアカウントが存在しない場合、作成します。$RISEはプロキシアカウントに送信され、デリゲーションが開始されます。

```bash
sunrised tx selfdelegation self-delegate [amount] [flags]
```

- MsgWithdrawSelfDelegationUnbonded
Undelegateの後、一定期間が経過し、Unbondedの状態になったとき、引き出しを行うことができます。$RISEはあなたのアカウントの残高に返金されます。
Undelegateは、以下に説明するプロキシアカウントのTxで実行できます。

```bash
sunrised tx selfdelegation withdraw-self-delegation-unbonded [amount] [flags]
```

## セルフデリゲーションプロキシアカウント

$RISEのセルフデリゲーションは、セルフデリゲーションプロキシアカウントを通じて処理されます。

セルフデリゲーションが行われると、$RISEはプロキシアカウントに移動します。プロキシアカウントは$RISEを$vRISEに変換し、あなたのデリゲータとして機能します。

### クエリ

`x/selfdelegation`クエリを使用して、プロキシアカウントを見つけます。

```bash
sunrised q selfdelegation self-delegation-proxy-account-by-owner [your-address]
```

### Msg実行

1. MsgUndelegate
1. MsgWithdrawReward
1. MsgSend

CLIでは、以下を使用します

```bash
sunrised tx accounts execute [proxy-account-address] [execute-msg-type-url] [json-message] [flags]
```

- MsgUndelegate
プロキシアカウントからのデリゲーションがキャンセルされます。一定期間後、x/selfdelegationのMsgWithdrawSelfDelegationUnbondedによって引き出し可能になります。
- MsgWithdrawReward
デリゲーション報酬を引き出します。引き出された報酬はMsgSendを通じて他のアカウントに送信できます。
- MsgSend
利用可能な資金を他のアカウントに送信します。

#### sunrise.accounts.self_delegation_proxy.v1.MsgUndelegate

```bash
sunrised tx accounts execute sunrise1jpaxtum2vckspj6nqe0pjkk7pxel0avuyz8dehpe87qxk5w0yc5s4qtzul sunrise.accounts.self_delegation_proxy.v1.MsgUndelegate "{\"amount\":\"4000\"}"
```

```protobuf
message MsgUndelegate {
  option (cosmos.msg.v1.signer) = "sender";
  string sender = 1 [(cosmos_proto.scalar) = "cosmos.AddressString"];
  // Amount of bond denom
  string amount = 2 [
    (cosmos_proto.scalar) = "cosmos.Int",
    (gogoproto.customtype) = "cosmossdk.io/math.Int",
    (gogoproto.nullable) = false
  ];
}
```

#### sunrise.accounts.self_delegation_proxy.v1.MsgWithdrawReward

```protobuf
message MsgWithdrawReward {
  option (cosmos.msg.v1.signer) = "sender";

  string sender = 1 [(cosmos_proto.scalar) = "cosmos.AddressString"];
  string validator_address = 2 [(cosmos_proto.scalar) = "cosmos.ValidatorAddressString"];
}
```

#### sunrise.accounts.self_delegation_proxy.v1.MsgSend

```protobuf
message MsgSend {
  option (cosmos.msg.v1.signer) = "sender";

  string sender = 1 [(cosmos_proto.scalar) = "cosmos.AddressString"];
  string to_address = 2 [(cosmos_proto.scalar) = "cosmos.AddressString"];
  repeated cosmos.base.v1beta1.Coin amount = 3 [
    (gogoproto.nullable) = false,
    (gogoproto.castrepeated) = "github.com/cosmos/cosmos-sdk/types.Coins"
  ];
}
```

## デリゲート可能なロックアップアカウント

Sunrise メインネットでは、エアドロップやジェネシスで付与された他の資金は、ロックアップアカウントとして一定期間ロックされます。
詳細については、[ロックアップアカウント](../../learn/sunrise/lockup-account.md)を参照してください。

セルフデリゲータブルロックアップアカウントにより、バリデータはセルフデリゲーションを行うことができます。

### Tx実行

セルフデリゲータブルロックアップアカウントでは以下のTxがサポートされています

1. MsgSelfDelegate
1. MsgWithdrawSelfDelegationUnbonded

CLIでは、以下を使用します

```bash
sunrised tx accounts execute [account-address] [execute-msg-type-url] [json-message] [flags]
```

#### sunrise.accounts.self_delegatable_lockup.v1.MsgSelfDelegate

```bash
sunrised tx accounts execute sunrise1jpaxtum2vckspj6nqe0pjkk7pxel0avuyz8dehpe87qxk5w0yc5s4qtzul sunrise.accounts.self_delegatable_lockup.v1.MsgSelfDelegate "{\"amount\":\"4000\"}"
```

```protobuf
message MsgSelfDelegate {
  string sender = 1 [(cosmos_proto.scalar) = "cosmos.AddressString"];
  // Amount of fee denom
  string amount = 2 [
    (cosmos_proto.scalar) = "cosmos.Int",
    (gogoproto.customtype) = "cosmossdk.io/math.Int",
    (gogoproto.nullable) = false
  ];
}
```

#### sunrise.accounts.self_delegatable_lockup.v1.MsgWithdrawSelfDelegationUnbonded

```protobuf
message MsgWithdrawSelfDelegationUnbonded {
  string sender = 1 [(cosmos_proto.scalar) = "cosmos.AddressString"];
  // Amount of bond denom
  string amount = 2 [
    (cosmos_proto.scalar) = "cosmos.Int",
    (gogoproto.customtype) = "cosmossdk.io/math.Int",
    (gogoproto.nullable) = false
  ];
}
```