# Proof of Liquidity

Proof of Liquidity（流動性の証明）という シビル攻撃耐性メカニズムは、ネットワーク内の Voting Power（投票力）として流動性提供の履歴を利用します。

## **Gauge voting（**ゲージ投票**）**

多くの DEX には、流動性提供者にインセンティブを与えるための Gauge Voting（ゲージ投票）システムがあります。通常、このインセンティブは DEX のネイティブトークンのインフレーションによって提供されますが、これはサスティナブルではありません。

[Pancake Swap Docs](https://docs.pancakeswap.finance/products/vecake/gauges-voting)に例があります。

## ve(3,3)

「ve(3,3)」モデルは、「(3,3)」モデルのアイデアを組み合わせることで「ve」モデルを強化したバージョンです。このモデルには「ve」投票メカニズムを持つ Gauge Voting システムが含まれていますが、このメカニズムの新しい点は、各プールの投票者がプールの利益から報酬を得られることです。このメカニズムは、より多くの利益を得る可能性のあるプールに投票するよう、ステーカーにインセンティブを与えます。

## Berachain モデル

- `$BGT`: ステーキング用の譲渡不可能トークン
- `$BERA`: ネットワーク手数料（GAS）用の譲渡可能トークン

下記の Berachain のブログ記事は、このモデルを理解するための良いリソースです。
[Flow of Value: Examining the differences between PoS and PoL - a case for a new paradigm in sustainable incentive alignment at the protocol layer](https://blog.berachain.com/blog/flow-of-value-examining-the-differences-between-pos-and-pol-a-case-for-a-new-paradigm-in-sustainable-incentive-alignment-at-the-protocol-layer)

{% hint style="info" %}
※日本語訳記事はこちら: [価値の流れ：PoS と PoL の違いを検証 - プロトコル層における持続可能なインセンティブ調整の新しいパラダイムの事例](https://qiita.com/nft/items/33c1d74a5f235c7113e2)
{% endhint %}

この モデルの重要な点は以下の通りです:

- ステーキングトークンである`$BGT`を譲渡不可能にすることで、手数料のために保有する必要なく、純粋にステーキングのためにステーキングトークンを利用できるようになります
- インフレーション報酬は`$BGT`トークンで分配されるため、`$BERA`トークンの希薄化につながりません
- Ethereum の dApps は DEX の持続可能性に関心がありませんが、Berachain 上の dApps は常に Berachain の PoL（Proof of Liquidity）への参加に関心を持っています

## Sunrise モデル

Sunrise モデルは、その基盤となるアーキテクチャと設計原則に、厳選された過去の開発成果と進化の過程を取り入れ、それらを基に構築されています。

- `$vRISE`: ステーキング用の譲渡不可能トークン。
- `$RISE`: 手数料用の譲渡可能トークン。

フローは以下のようになります：

- 一部のユーザーが`x/liquiditypool`モジュールで流動性を提供します
  - 報酬として`$vRISE`を獲得します
- 一部のユーザーが`x/staking`モジュールで`$vRISE`トークンをステーキングします
- Voting Power を持つ人々は、`x/liquidityincentive`モジュールで、どのプールが流動性提供者へのインセンティブとして`$vRISE`を獲得すべきかを投票できます
- 各プールの投票者は、プールの利益から報酬を受け取ります。

Sunrise PoL は、「Sunrise DA を使用する dApps は Sunrise PoL への参加に関心がある」という Berachain の視点を継承しています。

## $vRISE のステーキング方法

- Sunrise Web App

## 仕様

- コンセンサスアルゴリズム：CometBFT（Tendermint）
  - Mysticeti のリサーチが進行中です
- ブロックチェーンアプリケーションフレームワーク：Cosmos SDK v0.50.2
- 最大バリデータセットサイズ：100

## Mysticeti

[Mysticeti](https://sui.io/mysticeti)は、Sui の次期バージョンで採用される最新のコンセンサスプロトコルです。
私たちの基本的な考え方は、Paradigm が Narwhal と Bullshark を ABCI と共に使用する PoC（概念実証）を試みた記事と同様です。
私たちは、Sunrise の処理能力を向上させるため、Mysticeti を ABCI に、さらには Sunrise に適用することを検討しています。
