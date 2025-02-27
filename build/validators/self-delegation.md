# Self Delegation

Validators can increase their Voting Power by staking &#36;RISE to themselves. This feature is only available for addresses registered as validators, such as MsgCreateValidator.

## x/selfdelegation Msg

1. MsgSelfDelegate
1. MsgWithdrawSelfDelegationUnbonded

- MsgSelfDelegate
It creates a self-delegation proxy account if one does not exist. &#36;RISE is sent to the proxy account to start delegation.

```bash
sunrised tx selfdelegation self-delegate [amount] [flags]
```

- MsgWithdrawSelfDelegationUnbonded
After Undelegate, after a certain period has expired, and when Unbonded, you can make a withdrawal; &#36;RISE will be refunded to the balance in your account.
Undelegate can be done with Proxy Account Tx as described below.

```bash
sunrised tx selfdelegation withdraw-self-delegation-unbonded [amount] [flags]
```

## Self Delegation Proxy Account

&#36;RISE self-delegation is processing through the Self Delegation Proxy Account.

When self-delegation takes place, the &#36;RISE is moved to the Proxy Account. The Proxy Account converts the &#36;RISE to &#36;vRISE and acts as your delegator.

### Query

Use `x/selfdelegation` query and find your proxy account.

```bash
sunrised q selfdelegation self-delegation-proxy-account-by-owner [your-address]
```

### Excute Msg

1. MsgUndelegate
1. MsgWithdrawReward
1. MsgSend

On CLI, use

```bash
sunrised tx accounts execute [proxy-account-address] [execute-msg-type-url] [json-message] [flags]
```

- MsgUndelegate
Delegation from Proxy Account is cancelled. After a certain amount period, it becomes withdrawable by MsgWithdrawSelfDelegationUnbonded of x/selfdelegation.
- MsgWithdrawReward
Withdraws the delegation reward. Withdrawn rewards can be sent to other accounts via MsgSend.
- MsgSend
Send available funds to other accounts.

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

## Delegatable Lockup Account

In Sunrise mainnet, Airdrops and other funds granted by Genesis are locked for a certain period of time as a lockup account.
For more details, see [Lockup Account](../../learn/sunrise/lockup-account.md).

A self-delegatable lockup account allows validators to self-delegation.

### Excute Tx

The following Txs are supported with self-delegatable lockup accounts

1. MsgSelfDelegate
1. MsgWithdrawSelfDelegationUnbonded

On CLI, use

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
