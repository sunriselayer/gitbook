# Interest Rate Swap

Gluon serves a functionality to swap interest rate.
It enables users to have fixed yield position or leveraged variable yield position for an interchain yield.

## Mechanism

The fixed yield rate will be realized by using zero coupon bond.
The basic mechanism is similar to Pendle finance.

IRS(Interest Rate Swap) is to tokenize underlying yield asset (UT) into principal tokens and yield tokens.
Principal tokens (PT) for fixed yield users and yield tokens (YT) for leveraged variable yield users.

### Terminology

- Vault (IRSVault): On-chain registered record with strategy contract & cycle to periodically create tranches.
- Tranche (IRSTranche): A pool with lifetime, where it manages PT/YT token mints, burns, and swap with underlying tokens.
- UT: Underlying token (e.g. ATOM)
- UYT: Underlying yield token (e.g. stATOM)
- PT: Principal token
- YT: Variable yield token
- IRS AMM pool: An amm pool internally managed to support swap requests between PT/UT or PT/UYT. Liquidity is provided by the users who would like to get swap fees by providing liquidity on the pair. The swap fee income is stable and it has low Impermanent Loss. PT's price will automatically fluctuate following the maturity because PT is zero-coupon bond (fixed yield). Hence if it is vanilla AMM, it will force LPers to have impermanent loss inevitably.

### IRS AMM pool swap formula

- TODO:

### Functionalities

- TODO:

#### Minting PT/YT

- TODO:

#### Redeeming PT/YT pair before maturity

- TODO:

#### Adding liquidity for underlying token and PT

- TODO:

#### Buying PT from liquidity

- TODO:

#### Buying YT from liquidity

- TODO:

#### Redeeming PT after maturity

- TODO:

#### Redeeming YT after maturity

- TODO:

## Strategies

Strategies can be extended by using CosmWasm smart contract.
For example, stATOM strategy that is implemented by CosmWasm smart contract can be used for the fixed yield position of ATOM staking reward.
