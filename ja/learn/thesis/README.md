# 🎓 Thesis

## Monolithic vs Modular（モノリシック vs モジュラー）

ブロックチェーンには 4 つのレイヤーがあります：

- Execution layer（実行層）
- Settlement layer（決済層）
- Consensus layer（コンセンサス層）
- Data Availability layer（データ可用性レイヤー）

「モジュラーブロックチェーン」は、これらの分離されたレイヤーを組み合わせ、スケーラブルなブロックチェーンを構築することを可能にするパラダイムです。

## Data Availability layer（データ可用性レイヤー）

簡単に言えば、DA Layer（データ可用性レイヤー）は、Layer 2（L2）ブロックチェーンのトランザクションデータが Layer 1（L1）ブロックチェーンで Finalize（確定）されるまで、そのデータを保存する役割を果たします。

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

[『モジュラー・ブロックチェーン（Modular Blockchain）の可能性』](https://writing.tanelabs.com/%E3%83%A2%E3%82%B8%E3%83%A5%E3%83%A9%E3%83%BC%E3%83%96%E3%83%AD%E3%83%83%E3%82%AF%E3%83%81%E3%82%A7%E3%83%BC%E3%83%B3modular-blockchain%E3%81%AE%E5%8F%AF%E8%83%BD%E6%80%A7)（Tané - Writing）
{% endhint %}
