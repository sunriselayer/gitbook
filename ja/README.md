---
cover: .gitbook/assets/Sunrise_Cover.png
coverY: 0
---

# 👋 Sunrise

**ドキュメントは現在作成中であり、定期的に更新されています。最新の情報については、後日再度ご確認ください。**

Sunriseは、開発者がセキュリティと流動性を強化されたロールアップ/アプリを構築できるようにすることで、モジュラーパラダイムをサポートするProof of LiquidityとFee Abstractionに特化したデータ可用性（DA）レイヤーです。
SunriseはBerachainのProof of Liquidity（PoL）モデルをロールアップとL2に拡張し、RollkitとOP Stackと互換性のある柔軟なモジュラーデザインを特徴としています。GluonはSunrise L1ブロックチェーン上にSovereign Rollup（L2）としてデプロイされ、オーダーブック形式の取引プラットフォームとして機能します。これはWeb2のようなユーザー認証、オンチェーン決済を備えたオフチェーンの注文マッチングエンジン、そしてIBCベースの入出金機能を特徴としています。GluonとSunriseは直接通信し、既存のAltDAプロバイダーよりも純価値抽出の少ないスケーリングソリューションを可能にするため、blobspaceと引き換えに流動性の提供（PoLの複製）を可能にします。Sunrise上のPoLは、ロールアップとSunrise両方のセキュリティと流動性を相互に高め、Berachainで見られるPoLと並行したフライホイール効果をもたらします。



## Sunrise の機能

- Proof of Liquidity（PoL）
- DA Fee Abstraction（DA 手数料抽象化）
- Off Chain Blob Data Availability（オフチェーンによる Blob Data の公開検証性）

## Proof of Liquidity x Data Availability

SunriseはProof of Liquidityを活用してDA体験を向上させながら、Sunrise上のL2とSunrise L1自体の流動性と主権性を高める相互に有益な環境を提供します。
Sunriseは、純粋に利他的または自発的な貢献に依存するのではなく、主にProof of Liquidity（PoL）モデルを通じてデータ可用性（DA）ネットワークにインセンティブを与えます。実際には、特定のホワイトリストされたプールに流動性を提供するユーザーまたは開発者は、その見返りとしてデータを公開する権利（すなわちblobspace）を受け取ります。これにより、DA手数料は単一のネイティブトークンで支払われる方式から、参加者が資産をロックしてblobspaceを獲得するというより柔軟な仕組みへと変化します。流動性提供者は経済的恩恵を受けるため、信頼性の高い安全なデータ可用性を維持することに直接的な利害関係を持ち、ネットワーク全体でインセンティブが調整されます。この機能と任意の長期的なデータ可用性へのインセンティブにより、開発者はスケーラブルなL2を構築するだけでなく、AI、ゲームなどの新しい完全オンチェーン技術も探索できるようになります。


## 開発者が Sunrise を使用すべき理由

- ユーザーはDA手数料を必要とせず、流動性提供だけでSunrise DAを利用できます
- 多数のDEXが既に存在していますが、トークン発行者に対する差別化は限られています。L2開発者はSunriseの存在にかかわらず、常に流動性を提供する必要があります。一方、SunriseのDEXに流動性を提供することで、トークン発行者はSunriseのDAを通じて追加のユーティリティにアクセスでき、同等の利点を持たない他のDAレイヤーやDEXよりもSunriseを選択する動機となります


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
