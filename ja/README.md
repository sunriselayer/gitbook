---
cover: .gitbook/assets/Sunrise Cover.png
coverY: 0
---

# Sunrise 日本語ドキュメント

**ドキュメントは現在作成中であり、定期的に更新されています。最新の情報については、後日再度ご確認ください。**

Sunrise は、Proof of Liquidity と Fee Abstraction に特化した Data Availability Layer（DA Layer: データ可用性層）です。モジュラーパラダイムをサポートし、開発者がセキュリティと流動性を強化したロールアップやアプリケーションを構築することを可能にします。Sunrise は Berachain の Proof of Liquidity（PoL）モデルをロールアップや L2 に拡張し、Celestia アーキテクチャとの互換性を維持しています。モジュラークロスチェーンイールドハブ（Gluon）が Sovereign Rollup（L2）として Sunrise L1 ブロックチェーンにデプロイされます。このイールドハブと Sunrise が直接通信し、blobspace と引き換えに流動性（PoL の複製）を提供することで、既存の AltDA プロバイダーよりも純価値抽出の少ないスケーリングソリューションを実現します。Sunrise 上の PoL は、ロールアップと Sunrise 双方のセキュリティと流動性を相互に高め、Berachain で見られる PoL と同様のフライホイール効果を生み出します。

Celestia アーキテクチャとの互換性により、ロールアップのオンボーディングの難しさを最小限に抑えています。これは、Sunrise がネイティブに IBC 互換であることも意味します。Celestia を統合した Rollup-as-a-Service（RaaS）プロバイダーは、Sunrise を簡単に統合できます。また、Celestia をサポートするロールアップ SDK（例：OP stack、Polygon CDK、Rollkit、Sovereign SDK など）は、自動的に Sunrise と互換性を持つことになります。

## Sunrise の機能

Celestia 互換機能：

- Blob Tx
- BlobStream

Sunrise 固有の機能：

- Proof of Liquidity（PoL）
- DA Fee Abstraction（DA 手数料抽象化）
- Off Chain Blob Data Availability（オフチェーンによる Blob Data の公開検証性）（Sunrise DA v2）
- Sovereign Proof of Liquidity by Gluon（Gluon による主権的な流動性証明）

## Proof of Liquidity x Data Availability

前述の通り、Sunrise は Proof of Liquidity を利用して Sunrise L1 のセキュリティを強化し、Sunrise 上の L2 の流動性と主権性を高めます。Sunrise は他の DA ネットワークが利他主義や自発的な貢献に依存しているのに対し、DA ネットワークにインセンティブを与える仕組みも持っており、DA ネットワークのスループットを向上させることができます。この特徴と任意の長期データ可用性へのインセンティブにより、開発者はスケーラブルな L2 だけでなく、AI やゲーミングなどのフルオンチェーンの新技術も構築できます。

Sunrise は、Data Availability（DA）ネットワークにインセンティブを与えることができます。これは、他の DA ネットワークが利他主義や自発的な貢献に依存しているのとは対照的です。そのため、Sunrise は DA ネットワークのスループットを向上させることができます。この機能と、オプションの長期的な Data Availability へのインセンティブにより、開発者はスケーラブルな L2（レイヤー 2）を構築できるだけでなく、AI、ゲーミングなどのフルオンチェーンの新技術も探求することができます。

## 開発者が Sunrise を使用すべき理由

- ユーザーは手数料なしで流動性を提供することで DA を利用できます。
- 多数の DEX（分散型取引所）がすでに存在していますが、トークン発行者にとっての差別化は限られています。Sunrise の存在に関わらず、L2 開発者は常に流動性を提供する必要があります。しかし、Sunrise の DEX に流動性を提供することで、トークン発行者は Sunrise の DA を通じて追加のユーティリティにアクセスできます。これにより、同様の利点を持たない他の DA レイヤーや DEX よりも Sunrise を選択する動機付けとなります。

## Modules

- `x/da` モジュール
- `x/tokenconverter` モジュール
- `x/liquiditypool` モジュール
- `x/liquidityincentive` モジュール
- `x/swap` モジュール
- `x/fee` モジュール

### 収益（手数料構造）

プロトコルは 3 つの異なる収益源を通じて収益を生み出します。

- Transaction fees（トランザクション手数料）
- Swap fees in the liquidity pool（流動性プールでのスワップ手数料）
- MEV captured with [Skip Protocol](https://docs.skip.money/)（Skip Protocol を使用して捕捉される MEV（Miner Extractable Value））
