# **Thesis（テーゼ）**

## Monolithic vs Modular（モノリシック vs モジュラー）

ブロックチェーンには 4 つのレイヤーがあります：

- Execution layer（実行層）
- Settlement layer（決済層）
- Consensus layer（コンセンサス層）
- Data Availability layer（データ可用性層）

「モジュラーブロックチェーン」は、これらの分離されたレイヤーを組み合わせ、スケーラブルなブロックチェーンを構築することを可能にするパラダイムです。

## Data Availability layer（データ可用性層）

簡単に言えば、DA Layer（データ可用性層）は、Layer 2（L2）ブロックチェーンのトランザクションデータが Layer 1（L1）ブロックチェーンで Finalize（確定）されるまで、そのデータを保存する役割を果たします。

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

### Sovereign rollup（ソブリン・ロールアップ）

Gluon の例：

|                         |         |
| ----------------------- | ------- |
| Execution layer         | Gluon   |
| Settlement layer        | Gluon   |
| Consensus layer         | Sunrise |
| Data Availability layer | Sunrise |

{% hint style="info" %}
モジュラーチェーンの概要について学ぶために、下記の資料などがおすすめです。

[『モジュラーブロックチェーンの概要と潮流 ～ブロックチェーンを性能向上させる技術～』](https://www.jri.co.jp/page.jsp?id=108637)（日本総研）

[『モジュラー・ブロックチェーン（Modular Blockchain）の可能性』](https://writing.tanelabs.com/%e3%83%a2%e3%82%b8%e3%83%a5%e3%83%a9%e3%83%bc%e3%83%96%e3%83%ad%e3%83%83%e3%82%af%e3%83%81%e3%82%a7%e3%83%bc%e3%83%b3modular-blockchain%e3%81%ae%e5%8f%af%e8%83%bd%e6%80%a7)（Tané - Writing）
{% endhint %}
