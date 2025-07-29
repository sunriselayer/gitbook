# 手数料

`x/fee`モジュールは、Sunriseブロックチェーンの中核コンポーネントであり、取引手数料の管理を担当します。指定されたステーブルコイン（`fee_denom`）で手数料を徴収し、その一部を$RISE（`burned_denom`）にスワップしてバーン（焼却）します。このモジュールは、$RISEのデフレ的なトークノミクスをサポートしつつ、ユーザーにとって安定した手数料システムを維持します。

## `x/fee`の主な特徴

1.  **バーンメカニズム:**
    *   徴収された手数料（`fee_denom`）の一部は、$RISE（`burned_denom`）にスワップされた後、バーンされ、流通供給量を削減します。
    *   バーン率は`burn_ratio`パラメータによって決定されます（デフォルト：50%）。
    *   スワップとバーンの操作はアトミックであり、オンチェーンで検証されます。

2.  **手数料デノミネーション (`fee_denom`):**
    *   取引手数料に必要なデノミネーションを指定します（デフォルト：**`"uusdrise"`**）。
    *   トランザクションは、バイパスされない限り、このデノミネーションで手数料を支払う必要があります。
    *   手数料デノミネーションの厳格な検証が強制されます。

3.  **動的なパラメータ設定:**
    *   開発者は、モジュールによって強制される検証を伴って、パラメータを動的に設定できます。
    *   パラメータはガバナンス提案を通じて更新できます。

## 主要機能

### 手数料の徴収と処理

**手数料徴収プロセス:**

1.  手数料は`FeeCollector`モジュールアカウントを通じて`fee_denom`で徴収されます。
2.  システムは以下を検証します：
    *   トランザクションごとに1つの手数料デノミネーションのみ。
    *   手数料デノミネーションが設定された`fee_denom`と一致すること。
    *   手数料額が有効でゼロでないこと。

**手数料処理フロー:**

1.  `burn_ratio`によって決定される徴収手数料の一部が、バーン対象として指定されます。
2.  この部分は、`x/swap`モジュールを介して`fee_denom`から`burned_denom`にスワップされます。
3.  結果として得られた`burned_denom`トークンは供給からバーンされます。
4.  残りの`fee_denom`（バーン対象外の部分）は、他のプロトコル用途のために`FeeCollector`アカウントに残ります。

## パラメータ設定

> **注:** 以下のセクションは、経験豊富なユーザーまたは開発者向けの高度なトピックを扱います。

| パラメータ | 説明 | デフォルト値 | 制約 |
| --- | --- | --- | --- |
| `fee_denom` | 取引手数料に必要なデノミネーション | `"uusdrise"` | 有効なデノミネーションである必要があります |
| `burned_denom` | 手数料決済時にバーンされるデノミネーション | `"urise"` | 有効なデノミネーションである必要があります |
| `burn_ratio` | バーンする手数料の割合 | `0.5` | 0から1の間である必要があります |

## ワークフロー：手数料処理

> **注:** 以下のセクションは、経験豊富なユーザーまたは開発者向けの高度なトピックを扱います。

```mermaid
sequenceDiagram
    participant User
    participant FeeModule as x/fee Module
    participant BankKeeper as Bank Keeper
    participant SwapModule as x/swap Module
    participant FeeCollector as Fee Collector
    participant BribeModule as x/bribe Module

    User->>FeeModule: Submit Transaction
    FeeModule->>BankKeeper: Validate Fee Denomination
    BankKeeper->>FeeCollector: Transfer Fees (in fee_denom)
    
    note over FeeModule, SwapModule: Fee Processing
    FeeModule->>FeeModule: Calculate amount to swap & burn
    FeeModule->>SwapModule: Swap fee_denom to burned_denom
    SwapModule-->>FeeModule: Returns burned_denom
    FeeModule->>BankKeeper: Execute Burn (burned_denom)

    note over BribeModule, FeeCollector: Unclaimed Bribe Processing
    BribeModule->>FeeModule: Process Unclaimed Bribes
    FeeModule->>FeeCollector: Transfer Unclaimed Amounts
```

詳細と実装の仕様については、[GitHubリポジトリ](https://github.com/sunriselayer/sunrise/tree/main/x/fee)を参照してください。
