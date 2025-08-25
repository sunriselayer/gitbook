# IYA戦略

{% hint style="info" %}
この機能はメインネットで利用可能です！
{% endhint %}

## 基本的な考え方

UnUniFiの`yieldaggregator`モジュールは、**戦略**として登録されているスマートコントラクトの機能を呼び出すことができます。ユーザーが`yieldaggregator`モジュールの**Vault**に資金を入金すると、モジュールは自動的に**Vault**に含まれる戦略に資金を割り当てます。戦略コントラクトは、[こちら](strategy-interface.md)で説明されている特定のインターフェースを満たします。

サンプルソースコードは[こちら](https://github.com/UnUniFi/contracts/tree/main/contracts/strategy-example)です。

### インターチェーン戦略

相互運用性なしでUnUniFiチェーンのみで完全に実行できる戦略は、[こちら](strategy-interface.md)で説明されている方法で簡単に開発できます。

しかし、UnUniFi上のCosmWasmスマートコントラクトのみでインターチェーン戦略を開発することは不可能ではありませんが、困難です。これは、戦略コントラクトがインターチェーンアカウントとインターチェーンクエリ、またはEVMチェーン上のそのようなものを管理する必要があるためです。

その困難を軽減するために、戦略コントラクトを開発するためのいくつかの方法を組み合わせることができます。

- IBCフックを使用して外部CosmWasmチェーンでコントラクトを開発する
- Axelarを使用して外部EVMチェーンでコントラクトを開発する

### 外部CosmWasmチェーン上のコントラクトとの組み合わせ

この方法は、CosmWasmコントラクトのデプロイにガバナンスゲートを必要とせず、IBCフックモジュールをサポートしているCosmWasmチェーンに使用できます。たとえば、Neutronです。

IYA戦略の開発には、[CosmWasm](../cosmwasm/)の知識が必要です。

詳細は[こちら](strategy-external-cosmwasm-ibchooks.md)で説明されています。

### 外部EVMチェーン上のコントラクトとの組み合わせ

この方法は、EVMチェーンに使用できます。たとえば、Ethereum、Arbitrum、Avalanche c-chain、Polygonです。

詳細は[こちら](strategy-external-evm-axelar.md)で説明されています。

### UnUniFi上のCosmWasm戦略コントラクトのみ

この方法は、他の方法を選択できない戦略コントラクトに使用されます。たとえば、OsmosisチェーンはCosmWasmコントラクトをデプロイするためにガバナンスゲートを必要とします。これを回避するために、Osmosis LPファーミング戦略コントラクトはこの方法で開発されています。

たとえば、SeiチェーンはIBCフックをサポートしていません。したがって、たとえば、Astroport LPファーミング戦略コントラクトはこの方法で開発されます。

#### Osmosis LPファーミング戦略

ソースコードは[こちら](https://github.com/UnUniFi/contracts/tree/main/contracts/strategy-osmosis)です。

## 戦略登録の提案

準備中です。

お急ぎの場合は、直接お問い合わせください。
