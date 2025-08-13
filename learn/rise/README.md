# RISE

$RISE token is the native token of Sunrise network. Fees are paid in $USDrise.
A part of the $USDrise tx fee will be swapped to $RISE and then burnt in the [Fee](../sunrise/fee.md) module.

$RISE is preserved as `urise` in the Sunrise blockchain. `1000000urise` on the
Sunrise network converts to 1 RISE in the real world.

- Ticker: RISE
  Denomination on blockchain: `urise`

$RISE can be minted by burning $vRISE 1 to 1.

## vRISE

$vRISE token is a non-transferable token for staking. The staked amount will be
calculated as a voting power for the governance.

- Ticker: vRISE
- Denom in the blockchain: `uvrise`

$vRISE can be staked to the Sunrise network. The staked amount will be
calculated as voting power for governance. Furthermore, the rewards for
stakers will be distributed in proportion to the staked amount.

To get $vRISE, users need to provide liquidity in
[Liquidity Pool](../sunrise/liquidity-pool.md).

## Usage of Tokens

<!-- Berachain-style summary table with icons and token names -->

| Function           | Token(s)                                                                     | Details                                                |
| ------------------ | ---------------------------------------------------------------------------- | ------------------------------------------------------ |
| Security           | ![RISE](../../images/RISE.png) RISE + ![vRISE](../../images/vRISE.png) vRISE | Both vRISE & RISE can be staked for Consensus          |
| Governance         | ![vRISE](../../images/vRISE.png) vRISE                                       | vRISE is used for On-chain governance and Gauge Voting |
| Security Emissions | ![RISE](../../images/RISE.png) RISE                                          | RISE is distributed for stakers as consensus rewards   |
| LP Emissions       | ![vRISE](../../images/vRISE.png) vRISE                                       | vRISE is distributed for LPs as incentives             |
| Fee                | Any (swapped to ![USDrise](../../images/USDrise.png) USDrise)                | USDrise is used as a transaction fee                   |

**Legend:**  
![RISE](../../images/RISE.png) = RISE  ![vRISE](../../images/vRISE.png) = vRISE  ![USDrise](../../images/USDrise.png) = USDrise

## Tokenomics

### Summary

- `[Supply] = [Supply of $RISE] + [Supply of $vRISE]`
- Supply cap is 1,000,000,000.
  - It means `[Supply of $RISE] + [Supply of $vRISE] <= 1,000,000,000`
- Initial Inflation Rate Cap is 10%.
  - Inflation Rate Cap will gradually diminish by 8% per year.
    - For example, Inflation Rate of 2nd year is 9.2%.
- A part of tx fees (paid in $USDrise) is swapped to $RISE and burnt.
- Supply will grow with following the Supply Cap and Inflation Rate Cap.
- Observed Inflation Rate is different from Inflation Rate Cap.
- Inflationally minted $vRISE will be distributed among stakers validators and
  delegators for rewards.

### Formal expression

- Year: $$ t \in \{0,\ 1,\ 2,\ \ldots\} $$
- Supply of $RISE: $$ s_t^{\text{RISE}} $$
- Supply of $vRISE: $$ s_t^{\text{vRISE}} $$
- Supply: $$ s_t = s_t^{\text{RISE}} + s_t^{\text{vRISE}} $$
- Initial Supply: $$ s_0 = \text{500,000,000} $$
- Initial Inflation Rate Cap: $$ \bar{\pi}\_0 = 0.1 = \text{10\%}$$
- Disinflation rate: $$ \delta = 0.08 = \text{8\%} $$
- Supply Cap: $$ \bar{s} = \text{1,000,000,000} $$
  - It must be satisfied: $$ s_t \le \bar{s} $$
- Inflation Rate Cap: $$ \bar{\pi}\_t $$
- Tx fee burnt $RISE: $$ b_t $$
- Supply transition:
  $$ s\_{t+1} = \min\{(1 + \bar{\pi}\_t) (s_t - b_t),\ \bar{s}\} $$
- Inflation Rate Cap transition:
  $$ \bar{\pi}\_{t+1} = \max\left\{(1 - \delta) \bar\pi_t,\ \text{0.02} \right\} $$
  - It means: $$ \min_t \bar{\pi}\_t = \text{0.02} = \text{2\%} $$
- Observed Inflation Rate: $$ \pi*t = \frac{s*{t+1} - s_t}{s_t} $$

#### Simulation

This simulation assumes that $$ b_t = 0 $$

which means that tx fee is not burnt.

- During year 0 to 10, actual Inflation Rate will be lower than this simulation
  because there must be burnt tx fees.
- Zero Observed Inflation Rate doesn't mean zero rewards for validators and
  stakers. If $$ b_t > 0$$
  , then $b_t$ amount of $vRISE will be minted for rewards
- Inflation Rate Cap is strictly complied, so there is also a possibility of Observed Inflation Rate being negative value.

| Year | Inflation Rate Cap |  Total Supply | Observed Inflation Rate |
| ---- | -----------------: | ------------: | ----------------------: |
| 0    |             10.00% |   500,000,000 |                  10.00% |
| 1    |              9.20% |   550,000,000 |                   9.20% |
| 2    |              8.46% |   600,600,000 |                   8.46% |
| 3    |              7.79% |   651,434,784 |                   7.79% |
| 4    |              7.16% |   702,161,229 |                   7.16% |
| 5    |              6.59% |   752,463,565 |                   6.59% |
| 6    |              6.06% |   802,057,048 |                   6.06% |
| 7    |              5.58% |   850,690,179 |                   5.58% |
| 8    |              5.13% |   898,145,641 |                   5.13% |
| 9    |              4.72% |   944,240,170 |                   4.72% |
| 10   |              4.34% |   988,823,543 |                   1.13% |
| 11   |              4.00% | 1,000,000,000 |                   0.00% |
| 12   |              3.68% | 1,000,000,000 |                   0.00% |
| 13   |              3.38% | 1,000,000,000 |                   0.00% |
| 14   |              3.11% | 1,000,000,000 |                   0.00% |
| 15   |              2.86% | 1,000,000,000 |                   0.00% |
| 16   |              2.63% | 1,000,000,000 |                   0.00% |
| 17   |              2.42% | 1,000,000,000 |                   0.00% |
| 18   |              2.23% | 1,000,000,000 |                   0.00% |
| 19   |              2.05% | 1,000,000,000 |                   0.00% |
| 20   |              2.00% | 1,000,000,000 |                   0.00% |
| 21   |              2.00% | 1,000,000,000 |                   0.00% |

## Supported wallet applications

### Wallets that support Cosmos blockchains

- Keplr
- Leap

### Command Line Interface (CLI)

- sunrised

## Listed exchanges

- Coming soon
