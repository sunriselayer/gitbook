# Develop a Frontend Application

{% hint style="info" %}
This feature is available on the testnet, but does not yet exist on the mainnet.
{% endhint %}

## Ecosystem Incentive

The Ecosystem Incentive of the UnUniFi protocol is designed to reward application developers.
Thw developers will be rewarded with a portion of the Tx Gas bill served from their apps.

Registration is required to use this feature.
Please register via `Incentive` in the UnUniFi Portal. Rewards can be distributed to multiple addresses.

After registration, the following JSON string is output.

```json
{"version":"v1","incentive-unit-id":"UnUniFi Core"}
```

Add this to the `TxMemo` of Txs sent out by your application.

Rewards will appear in the UnUniFi Portal, You get them by claiming tx.
