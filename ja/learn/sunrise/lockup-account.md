# ロックアップアカウント

Sunrise メインネットでは、エアドロップやジェネシスによって付与された資金は一定期間ロックされます。
これは時間の経過とともに徐々にロック解除され、他のアカウントに送信できるようになります。

## ロックアップアカウントタイプ

Sunriseでは、以下のロックアップアカウントが存在します

1. [continuous-locking-account](https://docs.cosmos.network/v0.52/build/modules/auth/vesting#continuously-vesting-accounts)
1. [delayed-locking-account](https://docs.cosmos.network/v0.52/build/modules/auth/vesting#continuously-vesting-accounts)
1. [periodic-locking-account](https://docs.cosmos.network/v0.52/build/modules/auth/vesting#continuously-vesting-accounts)
1. permanent-locking-account

- ContinuousLocking: 時間の経過とともに直線的にコインがベスティングされるロックアップアカウントの実装。
- DelayedLocking: 指定された時間に全てのコインが完全にベスティングされるロックアップアカウントの実装。
- PeriodicLocking: カスタムロックアップスケジュールに従ってコインがベスティングされるロックアップアカウントの実装。
- PermanentLocking: コインを永久にロックし、決して解放しません。このアカウントのコインはロックされた状態でも委任やガバナンス投票に使用できます。

基本的に、continuous-locking-accountが使用されます。ロックされた資金は時間の経過とともに徐々にロック解除されます。

## セルフデリゲータブルロックアップアカウント

Sunriseでは、`seld-delegatable-continuous-locking-account`のように`seld-delegatable`が接頭辞として付けられます。これは、バリデーター向けの機能であるセルフデリゲーションが利用可能であることを意味します。詳細は[セルフデリゲーション](../../build/validators/self-delegation.md)を参照してください。

## トランザクションの実行

ロックアップアカウントでは以下のトランザクションがサポートされています

1. MsgSend
<!-- 1. MsgDelegate
1. MsgUndelegate
1. MsgWithdrawReward -->

MsgSendはロック解除された資金を他のアカウントに移動できます。
<!-- MsgDelegateはロックされた資金も委任できます。
MsgWithdrawRewardはバリデーターへの委任報酬を請求できます。報酬はロックアップアカウントに追加され、ロックアップの対象となります。 -->

[Risescan](https://risescan.sunriselayer.io)でアカウントを検索することで、ロックアップアカウントのステータスを確認できます。ロックアップ残高を取得したい場合は、[Sunrise App](https://app.sunriselayer.io/accounts/lockup)にアクセスしてこのトランザクションを送信してください。

CLIでは、以下を使用します

```bash
sunrised tx accounts execute [lockup-account-address] sunrise.accounts.self_delegatable_lockup.v1.MsgSend "{\"sender\":<owner-account-address>,\"to_address\":<recipient-account-address>,\"amount\":[{\"amount\":\"4000\", \"denom\":\"urise\"}]}" [flags]
```

## クエリ

`x/selfdelegation`クエリを使用して、ロックアップアカウントを検索します。

```bash
sunrised q selfdelegation lockup-accounts-by-owner [your-address]
```

ロックアップアカウントでは以下のクエリがサポートされています

1. QueryLockupAccountInfoRequest
1. QuerySpendableAmountRequest

Sunrise AppとRisescanはこれらの情報を表示することをサポートしています。
CLIでは、以下を使用します

```bash
sunrised query accounts query [lockup-account-address] [query-request-type-url] [json-message] [flags]
```