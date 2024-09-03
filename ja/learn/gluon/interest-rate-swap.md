# Interest Rate Swap

Gluon serves as a functionality to swap interest rates. It enables users to have a fixed yield position or leveraged variable yield position for an interchain yield.

## Mechanism

The fixed yield rate will be realized by using zero coupon bond. The basic mechanism is similar to Pendle finance.

IRS(Interest Rate Swap) is to tokenize underlying yield asset (UT) into principal tokens and yield tokens. Principal tokens (PT) for fixed yield users and yield tokens (YT) for leveraged variable yield users.

### Terminology

* Vault (IRSVault): On-chain registered record with strategy contract & cycle to periodically create tranches.
* Tranche (IRSTranche): A pool with a lifetime, where it manages PT/YT token mints, burns, and swaps with underlying tokens.
* UT: Underlying token (e.g. ATOM)
* UYT: Underlying yield token (e.g. stATOM)
* PT: Principal token
* YT: Variable yield token
* IRS AMM pool: An AMM pool internally managed to support swap requests between PT/UT or PT/UYT. Liquidity is provided by the users who would like to get swap fees by providing liquidity on the pair. Hence if it is vanilla AMM, it will force LPers to have impermanent loss inevitably.

### IRS AMM pool swap formula

#### Why special AMM is needed for PT and YT is:

PT's price will automatically fluctuate following the maturity because PT is a zero-coupon bond (fixed yield). Hence if it is vanilla AMM, it will force LPers to have impermanent loss inevitably.

#### Formula

`x^(1-t)+y^(1-t)=k` t∊\[0,1)

When `t=0.999...`, this formula acts like `xy=k` When `t=0`, this formula acts like `x+y=k` (stable swap)

### Functionalities

#### 3 Ways to get yield

* Fixed Yield Tranche: Similar to buying principal token in Pendle
* Leveraged Variable Yield Tranche: Similar to buying yield token in Pendle
* Liquidity Pool: The swap fee income is stable and it has low Impermanent Loss. PT's price will automatically fluctuate following the maturity because PT is a zero-coupon bond (fixed yield).

#### Minting PT/YT

* Transfer underlying assets to the IRS vault account
* Calculate PT/YT mint amount
  * PT amount: `depositUnderlying * (1-(strategyAmount-ptSupply)/ytSupply)` (`(strategyUTAmount-ptSupply)/ytSupply` is 1YT value(UT based))
  * YT amount: `depositUnderlying`
* Execute deposit to strategy contract
* Mint PT/YT coins and send to the user

#### Redeeming PT/YT pair before maturity

* User should pass `redeemAmount` and `maxPtYtIns`
* Calculate the required PT/YT amount from the requested redeemed amount (The ratio between Pt Supply : Yt Supply and Pt / Yt amount redeemed should be the same)
* Check `maxPtYtIns`'s enough
* Burn PT/YT coins from the user
* Execute unstake from strategy to `sender` for redeemAmount

#### Adding liquidity for underlying token and PT

* User should pass `trancheId`, `shareOutAmount` and `tokenInMaxs`
* If the existing pool is empty, put full tokens (`tokenInMaxs`) and issue `OneShare` token
* If the existing pool is not empty, calculate `neededLpLiquidity` from `shareOutAmount`
  * Ensure `tokenInMaxs` is enough for `neededLpLiquidity`
  * Put `neededLpLiquidity` and issue `shareOutAmount`

#### Buying PT for fixed yield

* Swap UT for PT on amm pool

Note: For early access to the fund, the user can sell PT for UT before maturity.

#### Buying YT for leveraged variable yield

* User should pass `requiredYtAmount` and `tokenIn`
* Calculate the required UT deposit to get `requiredYtAmount`
* Take a loan for the required UT amount from the liquidity pool
* Mint PT and YT with loan
* Sell minted PT tokens for UT on AMM
* Payback loan with `tokenIn` and received UT from PT swap

#### Redeeming PT after maturity

* Burn PT tokens from the user's account
* Calculate redeemAmount (stATOM amount) from ptAmount and redemption rate (stATOM -> ATOM)
* Execute unstake from strategy to `sender` for redeemAmount

#### Redeeming YT after maturity

* Calculate the redemption amount from `ytAmount` - `ytRate * ytAmount` (`ytRate = (strategyUtAmount - ptSupply) / ytSupply`)
* Burn `ytAmount` from the user's balance
* Execute unstake from strategy to `sender` for redeemAmount

## Strategies

Strategies can be extended by using the CosmWasm smart contract. For example, stATOM strategy that is implemented by the CosmWasm smart contract can be used for the fixed yield position of ATOM staking reward.

### IRS strategy restrictions

* Liquid Staking like stATOM
* LP of stable pairs like USDC/USDT
* It only can support strategies with no impermanent loss because the protocol must assure the return of fixed yield. If the loss exceeds the amount of the return for yield bearing token, the protocol must compensate.

## IRS Vaults

The vault registration requires a governance process.
