# Develop a Frontend Application

You can use these libraries to develop a frontend application.

- [cosmos-client-ts](https://github.com/cosmos-client/cosmos-client-ts)
- [ununifi-client](https://github.com/cosmos-client/ununifi-ts)
- [ts-codegen](https://github.com/CosmWasm/ts-codegen)
- [cosmjs](https://github.com/cosmos/cosmjs)

## Ecosystem Incentive

{% hint style="warn" %}
This feature is available on the testnet, but does not yet exist on the mainnet.
{% endhint %}
s
The Ecosystem Incentive of the UnUniFi protocol is designed to reward application developers.
The developers will be rewarded with a portion of the Tx Gas bill served from their apps.

Registration is required to use this feature.
Please register via `Incentive` in the UnUniFi Portal. Rewards can be distributed to multiple addresses.

After registration, the following JSON string is output.

```json
{ "version": "v1", "recipient_container_id": "ununifi_core" }
```

Add this to the `TxMemo` of Txs sent out by your application.

Rewards will appear in the UnUniFi Portal, You get them by claiming tx.
