# ロックアップアカウント

Sunriseメインネットでは、エアドロップやジェネシスによって付与されたその他の資金は、一定期間ロックされます。
これは時間とともに徐々にアンロックされ、他のアカウントに送信できるようになります。

## ロックアップアカウントの種類

Sunriseには、以下のロックアップアカウントが存在します。

1. [continuous-locking-account](https://docs.cosmos.network/v0.52/build/modules/auth/vesting#continuously-vesting-accounts)
2. [delayed-locking-account](https://docs.cosmos.network/v0.52/build/modules/auth/vesting#continuously-vesting-accounts)
3. [periodic-locking-account](https://docs.cosmos.network/v0.52/build/modules/auth/vesting#continuously-vesting-accounts)
4. permanent-locking-account

- ContinuousLocking: 時間の経過とともにコインを直線的に権利確定させるロックアップアカウントの実装です。
- DelayedLocking: 特定の時点で初めてすべてのコインを完全に権利確定させるロックアップアカウントの実装です。
- PeriodicLocking: カスタムのロックアップスケジュールに従ってコインを権利確定させるロックアップアカウントの実装です。
- PermanentLocking: コインを一切リリースせず、無期限にロックします。このアカウントのコインは、ロックされている間もデリゲートやガバナンス投票に使用できます。

基本的には、continuous-locking-accountが使用されます。ロックされた資金は、時間の経過とともに徐々にアンロックされます。

## 自己デリゲート可能なロックアップアカウント

Sunriseでは、`seld-delegatable-continuous-locking-account`のように、`seld-delegatable`が接頭辞として付加されます。これは、バリデーター向けの機能である自己デリゲートが利用可能であることを意味します。詳細については、[自己デリゲート](../../build/validators/self-delegation.md)を参照してください。

## トランザクションの実行

ロックアップアカウントでは、以下のトランザクションがサポートされています。

1. MsgSend
<!-- 1. MsgDelegate
2. MsgUndelegate
3. MsgWithdrawReward -->

MsgSendは、アンロックされた資金を他のアカウントに移動できます。
<!-- MsgDelegateは、ロックされた資金をデリゲートすることもできます。
MsgWithdrawRewardは、バリデーターへのデリゲーション報酬を請求できます。報酬はロックアップアカウントに追加され、ロックアップの対象となります。-->

[Risescan](https://risescan.sunriselayer.io)でアカウントを検索することで、ロックアップアカウントのステータスを確認できます。ロックアップ残高を取得したい場合は、[Sunrise App](https://app.sunriselayer.io/accounts/lockup)にアクセスしてこのトランザクションを送信してください。

CLIでは、以下を使用します。

```bash
sunrised tx accounts execute [lockup-account-address] sunrise.accounts.self_delegatable_lockup.v1.MsgSend "{\"sender\":<owner-account-address>,\"to_address\":<recipient-account-address>,\"amount\":[{\"amount\":\"4000\", \"denom\":\"urise\"}]}" [flags]
```

## クエリ

`x/selfdelegation`クエリを使用して、ロックアップアカウントを見つけます。

```bash
sunrised q selfdelegation lockup-accounts-by-owner [your-address]
```

ロックアップアカウントでは、以下のクエリがサポートされています。

1. QueryLockupAccountInfoRequest
2. QuerySpendableAmountRequest

Sunrise AppとRisescanは、これらの情報を表示することをサポートしています。
CLIでは、以下を使用します。

```bash
sunrised query accounts query [lockup-account-address] [query-request-type-url] [json-message] [flags]
```
