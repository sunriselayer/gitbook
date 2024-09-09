# **DA Fee Abstraction**

- Sunrise v1: DAWN: Sunrise v1: DAWN
- DA Fee Abstraction: DA 手数料の抽象化
- Blob Tx: ブロブトランザクション

Sunrise は「DA Fee Abstraction」（DA 手数料の抽象化）を実現しています。開発者は、Sunrise の流動性プールに流動性を提供することで、料金なしで Sunrise の Blob Spaces（ブロブスペース）を利用することができます。

## 動作方法

- ユーザーは、好きなプールの**`x/liquiditypool`**モジュールで LP トークンを作成します。
- ユーザーは報酬として$vRISE トークンを受け取ります。
- ユーザーは**`BlobTx`**の手数料に$vRISE を使用することができます。
  - **`BlobTx`**はプロトコルレベルで手数料として使用できる唯一のトランザクションです。
  - 他のトランザクションについては、ユーザーは$RISE トークンで手数料を支払う必要があります。
