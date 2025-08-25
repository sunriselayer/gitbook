# フロントエンドアプリケーションの開発

これらのライブラリを使用して、フロントエンドアプリケーションを開発できます。

- [cosmos-client-ts](https://github.com/cosmos-client/cosmos-client-ts)
- [ununifi-client](https://github.com/cosmos-client/ununifi-ts)
- [ts-codegen](https://github.com/CosmWasm/ts-codegen)
- [cosmjs](https://github.com/cosmos/cosmjs)

## エコシステムインセンティブ

{% hint style="warn" %}
この機能はテストネットで利用可能ですが、メインネットにはまだ存在しません。
{% endhint %}

UnUniFiプロトコルのエコシステムインセンティブは、アプリケーション開発者に報酬を与えるように設計されています。
開発者は、アプリから提供されるTxガスの請求額の一部で報酬を受け取ります。

この機能を使用するには登録が必要です。
UnUniFiポータルの`Incentive`から登録してください。報酬は複数のアドレスに分配できます。

登録後、次のJSON文字列が出力されます。

```json
{ "version": "v1", "recipient_container_id": "ununifi_core" }
```

これを、アプリケーションから送信されるTxの`TxMemo`に追加します。

報酬はUnUniFiポータルに表示され、請求トランザクションによって取得できます。
