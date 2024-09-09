# **Thesis（テーゼ）**

## Monolithic vs Modular（モノリシック vs モジュラー）

ブロックチェーンには 4 つのレイヤーがあります：

- Execution layer（実行レイヤー）
- Settlement layer（決済レイヤー）
- Consensus layer（コンセンサスレイヤー）
- Data Availability layer（ブロックチェーンデータ可用性レイヤー）

「モジュラー・ブロックチェーン」は、これらの分離されたレイヤーを組み合わせ、スケーラブルなブロックチェーンを構築することができるパラダイムです。

## ブロックチェーンデータ可用性レイヤー

簡単に言うと、ブロックチェーンデータ可用性（DA）レイヤーは、L2 トランザクションが L1 ブロックチェーンで最終的に Finalize（確定）するまで、L2 ブロックチェーンのトランザクションデータを保存する役割を果たします。

## レイヤーの組み合わせ

### 従来のロールアップ

Optimism の例：

|                         |          |
| ----------------------- | -------- |
| Execution layer         | Optimism |
| Settlement layer        | Ethereum |
| Consensus layer         | Ethereum |
| Data Availability layer | Ethereum |

### altDA を使用したスマートコントラクトロールアップ

Eclipse の例：

|                         |          |
| ----------------------- | -------- |
| Execution layer         | Eclipse  |
| Settlement layer        | Ethereum |
| Consensus layer         | Ethereum |
| Data Availability layer | Celestia |

### ソブリンロールアップ

Gluon の例：

|                         |         |
| ----------------------- | ------- |
| Execution layer         | Gluon   |
| Settlement layer        | Gluon   |
| Consensus layer         | Sunrise |
| Data Availability layer | Sunrise |
