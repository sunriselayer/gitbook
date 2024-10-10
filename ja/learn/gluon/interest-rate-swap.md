# Interest Swap（金利スワップ）

Gluon は金利をスワップする機能を提供します。これにより、ユーザーはインターチェーンのイールドに対して、固定イールドのポジションまたはレバレッジをかけた変動イールドのポジションを持つことができます。

## メカニズム

固定利回り率は、zero coupon bond（ゼロクーポン債）を使用して実現されます。基本的なメカニズムは Pendle finance と似ています。

Interest Rate Swap（IRS: 金利スワップ）は、原資産のイールド資産（UT）を Principal Token（PT: 元本トークン）と Yield Token（YT: イールドトークン）にトークン化することです。固定利回りユーザー向けの元本トークン（PT）と、レバレッジをかけた変動利回りユーザー向けのイールドトークン（YT）があります。

### 用語

- Vault（IRSVault）：ストラテジーコントラクトと Tranche（トランシェ）を定期的に作成するサイクルを持つ、オンチェーンに登録された記録
- Tranche（IRSTranche）：有効期間を持つプールで、PT/YT トークンのミント、バーン、および原資産トークンとのスワップを管理します
- UT：原資産トークン（例：ATOM）
- UYT：原資産イールドトークン（例：stATOM）
- PT：元本トークン
- YT：変動イールドトークン
- IRS AMM プール：PT/UT または PT/UYT 間のスワップリクエストをサポートするために内部で管理される AMM プール。流動性は、ペアに流動性を提供することでスワップ手数料を得たいユーザーによって提供されます。したがって、バニラ AMM の場合、LPer（流動性提供者）は避けられないインパーマネントロスを抱えることになります

### IRS AMM プールのスワップ公式

#### PT と YT に特別な AMM が必要な理由：

PT は満期に向けて自動的に価格が変動するため（PT は固定利回りなゼロクーポン債）。したがって、バニラ AMM の場合、LPer（流動性提供者） は避けられないインパーマネントロスを抱えることになります。

#### 公式

`x^(1-t)+y^(1-t)=k` t∊[0,1)

`t=0.999...` のとき、この公式は `xy=k` のように動作します。
`t=0` のとき、この公式は `x+y=k`（ステーブルスワップ）のように動作します。

### 機能

#### イールドを得る 3 つの方法

- Fixed Yield Tranche（固定利回りトランシェ）：Pendle の元本トークンの購入に似ています
- Leveraged Variable Yield Tranche（レバレッジ変動利回りトランシェ）：Pendle のイールドトークンの購入に似ています
- Liquidity Pool（流動性プール）：スワップ手数料収入が安定しており、インパーマネントロスが低いです。PT の価格は自動的に変動し、満期に従って変動します。なぜなら、PT はゼロクーポンボンド（固定利回り）だからです。

#### PT/YT のミント

- 原資産を IRS Vault Account に転送
- PT/YT ミント量の計算
  - PT 量：`depositUnderlying * (1-(strategyAmount-ptSupply)/ytSupply)` （`(strategyUTAmount-ptSupply)/ytSupply` は 1YT の価値（UT ベース））
  - YT 量：`depositUnderlying`
- ストラテジーコントラクトへのデポジットを実行
- PT/YT コインをミントしてユーザーに送信

#### 満期前の PT/YT ペアの償還

- ユーザーは `redeemAmount` と `maxPtYtIns` を渡す必要があります
- 要求された償還額から必要な PT/YT 量を計算（PT Supply : YT Supply の比率と、償還された Pt / Yt 量の比率は同じでなければなりません）
- `maxPtYtIns` が十分かチェック
- ユーザーから PT/YT コインをバーン
- ストラテジーから `sender` に `redeemAmount` のアンステークを実行

#### 原資産トークンと PT の流動性追加

- ユーザーは `trancheId`、`shareOutAmount`、`tokenInMaxs` を渡す必要があります
- 既存のプールが空の場合、全トークン（`tokenInMaxs`）を投入し、`OneShare` トークンを発行
- 既存のプールが空でない場合、`shareOutAmount` から `neededLpLiquidity` を計算
  - `tokenInMaxs` が `neededLpLiquidity` に対して十分であることを確認
  - `neededLpLiquidity` を投入し、`shareOutAmount` を発行

#### 固定イールド用の PT 購入

- AMM プールで UT を PT にスワップ

注：早期に資金にアクセスするために、ユーザーは満期前に PT を UT に売ることができます。

#### レバレッジ変動イールド用の YT 購入

- ユーザーは `requiredYtAmount` と `tokenIn` を渡す必要があります
- `requiredYtAmount` を得るために必要な UT デポジット量を計算
- 流動性プールから必要な UT 量のローンを取る
- ローンで PT と YT をミント
- ミントされた PT トークンを AMM で UT にスワップして売却
- `tokenIn` と PT スワップから受け取った UT でローンを返済

#### 満期後の PT の償還

- ユーザーのアカウントから PT トークンをバーン
- ptAmount と償還レート（stATOM -> ATOM）から redeemAmount（stATOM 量）を計算
- ストラテジーから `sender` に redeemAmount のアンステークを実行

#### 満期後の YT の償還

- `ytAmount` - `ytRate * ytAmount` から償還額を計算（`ytRate = (strategyUtAmount - ptSupply) / ytSupply`）
- ユーザーの残高から `ytAmount` をバーン
- ストラテジーから `sender` に redeemAmount のアンステークを実行

## ストラテジー

ストラテジーは CosmWasm スマートコントラクトを使用して拡張できます。例えば、CosmWasm スマートコントラクトで実装された stATOM ストラテジーは、ATOM ステーキング報酬の固定イールドポジションに使用できます。

### IRS ストラテジーの制限

- stATOM のようなリキッドステーキング
- USDC/USDT のようなステーブルペアの LP
- プロトコルは固定イールドの返還を保証しなければならないため、非永続的損失のないストラテジーのみをサポートできます。イールド生成トークンの返還額を超える損失が発生した場合、プロトコルが補償しなければなりません。

## IRS Vaults

Vault の登録にはガバナンスプロセスが必要です。
