# Proof of Liquidity

- Sovereign Proof of Liquidity: ソブリン・プルーフ・オブ・リクイディティ
- Proof of Liquidity: プルーフ・オブ・リクイディティ
- Sunrise v1: DAWN: Sunrise v1: DAWN

Proof of Liquidity のシビル耐性メカニズムは、ネットワーク内の投票力に対する流動性の提供履歴を利用しています。

## **Gauge voting（**ゲージ投票**）**

多くの DEX は、流動性プロバイダーにインセンティブを与えるためにゲージ投票システムを採用しています。通常、インセンティブは DEX のネイティブトークンのインフレーションによって与えられ、持続可能ではありません。

[Pancake Swap Docs](https://docs.pancakeswap.finance/products/vecake/gauges-voting)に例があります。

## ve(3,3)

モデル「ve(3,3)」は、モデル「ve」のアイデアとモデル「(3,3)」のアイデアを組み合わせたバージョンアップ版です。このメカニズムには「ve」投票メカニズムを備えたゲージ投票システムが含まれていますが、このメカニズムの新しさは、各プールの投票者がプールの利益から報酬を得ることができる点です。このメカニズムにより、ステーカーはより多くの利益を得る可能性のあるプールに投票することがインセンティブとなります。

## Berachain モデル

- `$BGT`: ステーキング用の譲渡不可能トークン
- `$BERA`: 手数料用の譲渡可能トークン

Berachain のブログ[Flow of Value](https://blog.berachain.com/blog/flow-of-value-examining-the-differences-between-pos-and-pol-a-case-for-a-new-paradigm-in-sustainable-incentive-alignment-at-the-protocol-layer)は、このモデルを理解するための良いリソースです。

このモデルの重要なポイントは以下の通りです：

1. ステーキングトークン `$BGT` を譲渡不可能にすることで、手数料のために保有する必要なく、純粋にステーキング目的でのみトークンを利用できるようになります。
2. インフレーション報酬は `$BGT` トークンで配布されるため、`$BERA` トークンの価値の希薄化につながりません。
3. Ethereum 上の dApp では DEX の持続可能性に関心が向けられていませんが、Berachain 上の dApp は常に Berachain の PoL（Proof of Liquidity）への参加に関心を持っています。

## Sunrise モデル

Sunrise モデルは、その基盤となるアーキテクチャと設計原則において、厳選された過去の開発成果と進化の過程を取り入れ、それらを基に構築されています。

- `$vRISE`：ステーキング用の譲渡不可能トークン
- `$RISE`：手数料用の譲渡可能トークン

システムの流れは以下のようになります：

1. 一部のユーザーが `x/liquiditypool` モジュールで流動性を提供します。
   - 報酬として `$vRISE` を獲得します。
2. 一部のユーザーが `x/staking` モジュールで `$vRISE` トークンをステーキングします。
3. 投票権を持つ人々は、`x/liquidityincentive` モジュールで、どのプールが流動性提供者へのインセンティブとして `$vRISE` を受け取るべきかを投票できます。
4. 各プールの投票者は、そのプールの利益から報酬を受け取ります。

Sunrise PoL（Proof of Liquidity）は、「Sunrise DA を使用する dApp は Sunrise PoL への参加に関心がある」という Berachain の考え方を引き継いでいます。

## $vRISE のステーキング方法

- Sunrise Web App

## 仕様

- コンセンサスアルゴリズム：CometBFT（Tendermint）
  - Mysticeti のリサーチが進行中です。
- ブロックチェーンアプリケーションフレームワーク：Cosmos SDK v0.50.2
- 最大バリデータセットサイズ：100

## Mysticeti

[Mysticeti](https://sui.io/mysticeti)は、Sui の次期バージョンで採用される最新のコンセンサスプロトコルです。
私たちの基本的な考え方は、Paradigm が Narwhal と Bullshark を ABCI と共に使用する PoC（概念実証）を試みた記事と同様です。
私たちは、Sunrise の処理能力を向上させるため、Mysticeti を ABCI に、さらには Sunrise に適用することを検討しています。
