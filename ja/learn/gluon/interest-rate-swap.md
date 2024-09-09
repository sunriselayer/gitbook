# Interest Rate Swap（金利スワップ）

Gluon は、利子率をスワップする機能として機能します。これにより、ユーザーはインターチェーンの利回りに対して固定の利回りポジションまたはレバレッジされた可変利回りポジションを持つことができます。

## Mechanism（メカニズム）

固定利回り率は、zero coupon bond（ゼロクーポンボンド）を使用して実現されます。基本的なメカニズムは Pendle finance と似ています。

利子率スワップ（IRS: Interest Rate Swap）は、基礎となる利回り資産（UT）をプリンシパルトークンとイールドトークンにトークン化するものです。固定利回りユーザー向けのプリンシパルトークン（PT）と、レバレッジされた可変利回りユーザー向けのイールドトークン（YT）があります。

### Terminology （用語集）

- Vault（IRSVault）：ストラテジーコントラクトとサイクルを持つオンチェーンの登録済みレコード。定期的に Tranche（トランチ）を作成します。
- Tranche（IRSTranche）：ライフタイムを持つプールで、PT/YT トークンの発行、バーン、および基礎となるトークンとの交換を管理します。
- UT：基礎となるトークン（例：ATOM）
- UYT：基礎となるイールドトークン（例：stATOM）
- PT：プリンシパルトークン
- YT：可変イールドトークン
- IRS AMM プール：PT/UT または PT/UYT 間のスワップリクエストをサポートするために内部で管理される AMM プール。流動性は、流動性を提供してスワップ手数料を得たいユーザーによって提供されます。したがって、バニラ AMM の場合、LP 提供者者は避けられないインパーマネントロスを抱えることになります。

### IRS AMM pool swap formula（IRS AMM プールスワップの式）

#### PT と YT のために特別な AMM が必要な理由：

PT の価格は満期に従って自動的に変動します。なぜなら PT はゼロクーポンボンド（固定利回り）だからです。したがって、通常の AMM だと LP 提供者に必ずインパーマーネントロスを強いてしまいます。

#### 計算式

`x^(1-t)+y^(1-t)=k` t∊\[0,1)

`t=0.999...`の場合、この式は `xy=k` のように機能します。`t=0` の場合、この式は `x+y=k`（stable swap）のように機能します。

### 機能

#### 利回りを得る 3 つの方法

- Fixed Yield Tranche（固定利回りトランシェ）：Pendle の主要トークンを購入するのと同様です。
- Leveraged Variable Yield Tranche（レバレッジ変動利回りトランシェ）：Pendle の利回りトークンを購入するのと同様です。
- Liquidity Pool（流動性プール）：スワップ手数料収入が安定しており、インパーマネントロスが低いです。PT の価格は自動的に変動し、満期に従って変動します。なぜなら、PT はゼロクーポンボンド（固定利回り）だからです。

#### Minting PT/YT（PT/YT の発行）

- IRS Vault account に基礎資産をトランスファーします
- PT/YT の発行数量を計算します
  - PT の数量：**`depositUnderlying * (1-(strategyAmount-ptSupply)/ytSupply)`**（**`(strategyUTAmount-ptSupply)/ytSupply`**は 1YT の価値（UT ベース）です）。
  - YT の数量：**`depositUnderlying`**。
- ストラテジーコントラクトにデポジットする。
- PT/YT コインを発行し、ユーザーに送信する。

#### Redeeming PT/YT pair before maturity（満期前の PT/YT ペアの償還）

- ユーザーは**`redeemAmount`**と**`maxPtYtIns`**を指定する必要があります。
- 要求された償還額から必要な PT/YT の数量を計算します（PT 供給量：YT 供給量と PT/YT の償還数量の比率は同じである必要があります）。
- **`maxPtYtIns`**が十分であるかを確認します。
- ユーザーから PT/YT コインを破棄します。
- 償還額に応じて戦略から**`sender`**にアンステークを実行します。

#### Adding liquidity for underlying token and PT（基礎トークンと PT の流動性の追加）

- ユーザーは**`trancheId`**、**`shareOutAmount`**、および**`tokenInMaxs`**を指定する必要があります。
- 既存のプールが空の場合、全トークン（**`tokenInMaxs`**）を入れ、**`OneShare`**トークンを発行します。
- 既存のプールが空でない場合、**`shareOutAmount`**から**`neededLpLiquidity`**を計算します。
- **`tokenInMaxs`**が**`neededLpLiquidity`**に十分であることを確認します。
- **`neededLpLiquidity`**を入れ、**`shareOutAmount`**を発行します。

#### Buying PT for fixed yield（利回りのための PT の購入）

- AMM プールで UT を PT にスワップします。

注意：ファンドへの早期アクセスのために、ユーザーは満期前に PT を UT に売却することができます。

#### Buying YT for leveraged variable yield（レバレッジ変動利回りのための YT の購入）

- ユーザーは**`requiredYtAmount`**と**`tokenIn`**を指定する必要があります。
- **`requiredYtAmount`**を得るために必要な UT のデポジットを計算します。
- 流動性プールから必要な UT の量のローンを借ります。
- ローンで PT と YT を発行します。
- 発行された PT トークンを UT で AMM で売却します。
- **`tokenIn`**と PT スワップで受け取った UT でローンを返済します。

#### Redeeming PT after maturity（満期後の PT の償還）

- ユーザーのアカウントから PT トークンを破棄します。
- PT の数量と償還率（stATOM -> ATOM）から償還額（stATOM の数量）を計算します。
- 償還額に応じて戦略から**`sender`**にアンステークを実行します。

#### Redeeming YT after maturity（満期後の YT の償還）

- **`ytAmount`** - **`ytRate * ytAmount`**（**`ytRate = (strategyUtAmount - ptSupply) / ytSupply`**）から償還額を計算します。
- ユーザーの残高から**`ytAmount`**をバーンします。
- 償還額に応じてストラテジーから**`sender`**にアンステークを実行します。

## Strategies（ストラテジー）

ストラテジーは CosmWasm スマートコントラクトを使用して拡張することができます。たとえば、CosmWasm スマートコントラクトで実装された stATOM ストラテジーは、ATOM ステーキング報酬の固定利回りポジションに使用することができます。

### IRS strategy restrictions（IRS ストラテジーの制約）

- stATOM のような Liquid Staking
- USDC/USDT のような安定したペアの LP
- プロトコルは固定利回りの返却を保証する必要があるため、一時的な損失のない戦略のみをサポートできます。利回りをもたらすトークンの損失が返却額を上回る場合、プロトコルは補償する必要があります。

## IRS Vaults

Valut 登録にはガバナンスプロセスが必要です。
