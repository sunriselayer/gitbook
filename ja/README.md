---
description: 日本語テスト
cover: .gitbook/assets/Sunrise Cover.png
coverY: 0
---

# Sunrise 日本語ドキュメント

**私たちのドキュメントは現在作成中で、定期的に更新されています。更新情報については後日再度ご確認ください。**

Sunrise は、DA Fee Abstraction（DA 手数料の抽象化）と Proof of Liquidity（プルーフ・オブ・リクイディティ）のための特殊なブロックチェーンデータ可用性（DA）レイヤーです。開発者がセキュリティと流動性を強化したロールアップ/アプリを構築できるようにすることで、モジュラーパラダイムをサポートしています。Sunrise は Berachain の Proof of Liquidity（PoL）モデルをロールアップと L2 に拡張しつつ、Celestia アーキテクチャとの互換性を維持しています。モジュラー型クロスチェーンイールドハブ（Gluon）が、独立型ロールアップ（L2）として Sunrise L1 ブロックチェーンにデプロイされます。このイールドハブと Sunrise は直接通信を行い、blobspace と引き換えに流動性の提供（PoL メカニズムの応用）を可能にし、既存の AltDA プロバイダーよりも純価値抽出の少ないスケーリングソリューションを実現します。Sunrise 上の PoL は、ロールアップと Sunrise 双方のセキュリティと流動性を相互に高め、Berachain で見られる PoL と同様の並行的なフライホイール効果（好循環効果）を生み出します。

Celestia アーキテクチャとの互換性により、ロールアップの導入の難易度が最小限に抑えられます。これはまた、Sunrise がネイティブに IBC 互換であることを意味します。Celestia を統合した Rollup-as-a-Service（RaaS）プロバイダーは、Sunrise を容易に統合できます。また、Celestia をサポートするロールアップ SDK（例：OP stack、Polygon CDK、Rollkit、Sovereign SDK など）は、自動的に Sunrise と互換性を持つことになります。

## Sunrise の機能

Celestia 互換機能：

- Blob Tx
- BlobStream

Sunrise 固有の機能：

- Proof of Liquidity（PoL）
- DA Fee Abstraction（DA 手数料抽象化）
- Off Chain Blob Data Availability（ブロックチェーン外部ブロブデータの公開検証性）（Sunrise DA v2）
- Sovereign Proof of Liquidity by Gluon（Gluon によるソブリン・プルーフ・オブ・リクイディティ）

## プルーフ・オブ・リクイディティ x ブロックチェーンデータ可用性

前述の通り、Sunrise は Proof of Liquidity を利用して Sunrise L1 のセキュリティを強化し、Sunrise 上の L2 の流動性と主権性を高めます。Sunrise は他の DA ネットワークが利他主義や自発的な貢献に依存しているのに対し、DA ネットワークにインセンティブを与える仕組みも持っており、DA ネットワークのスループットを向上させることができます。この特徴と任意の長期データ可用性へのインセンティブにより、開発者はスケーラブルな L2 だけでなく、AI やゲーミングなどのフルオンチェーンの新技術も構築できます。

## 収益（手数料構造）

プロトコルは 3 つの異なる流れで収益を生み出します。

- Transaction fees（トランザクション手数料）
- Swap fees in the liquidity pool（流動性プールのスワップ手数料）
- "MEV captured with Skip Protocol（Skip Protocol で捕捉される MEV）

## 開発者が Sunrise を使用すべき理由

- ユーザーは手数料なしで流動性提供によって DA を利用できます。
- 多数の DEX がすでに存在しますが、トークン発行者に対する差別化は限られています。L2 開発者は、Sunrise の存在にかかわらず、常に流動性を提供する必要があります。しかし、Sunrise の DEX に流動性を提供することで、トークン発行者は Sunrise の DA を通じて追加のユーティリティにアクセスでき、同等の利点を持たない他の DA レイヤーや DEX よりも Sunrise を選択するインセンティブが生まれます。

## 統合プロセスのロードマップ

### Sunrise v1: DAWN

- `*x/blob*` モジュール
- `x/blobstream` モジュール
- `*x/tokenconverter*` モジュール
- `x/liquiditypool` モジュール
- `*x/liquidityincentive*` モジュール
- `x/swap` モジュール
- `*x/fee*` モジュール

### Sunrise v2: セキュリティとインセンティブ

- Off Chain Blob Data Availability（ブロックチェーン外部ブロブデータの公開検証性）（Sunrise DA v2）
- Sovereign Proof of Liquidity by Gluon（Gluon によるソブリン・プルーフ・オブ・リクイディティ）

### 収益（手数料構造）

このプロトコルは、3 つの異なる流れを通じて収益を生み出します。

- Transaction fees（トランザクション手数料）
- Swap fees in the liquidity pool（流動性プールでのスワップ手数料）
- MEV captured with [Skip Protocol](https://docs.skip.money/)（Skip Protocol を使用して捕捉される MEV（Miner Extractable Value））
