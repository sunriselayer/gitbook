# **DA Fee Abstraction**

Sunrise は「DA Fee Abstraction」（DA 手数料の抽象化）を実現しています。開発者は、Sunrise 上の流動性プールに流動性を提供するだけで、手数料なしで Sunrise の blobspace を利用できます。

## **仕組み**

- ユーザーは、任意のプールに対して`x/liquiditypool`モジュールで LP トークンを Mint します
- ユーザーは報酬として$vRISE トークンを受け取ります
- ユーザーは$vRISE を、Data Availability のトランザクション手数料として使用できます
  - その他のトランザクションについては、ユーザーは$RISE トークンで手数料を支払う必要があります
