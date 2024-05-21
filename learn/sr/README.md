# $SR

$SR token is the native token of Sunrise network. $SR token can be used for fee.

$SR is preserved as `microSR` in the Sunrise blockchain. `1000000microSR` in the blockchain means 1 SR in the real world.

* Ticker: SR
* Denom in the blockchain: `microSR`
* Supply cap: 1,000,000,000SR = `1_000_000_000_000_000microSR`

$SR can be minted by burning $SSR with the following rule.

$$
  \text{OutputSR} = \text{InputSSR} \times \min\left(1, \frac{\text{CurrentSupplySR}}{\text{CurrentSupplySSR}} \right) \ \text{if} \ \text{CurrentSupplySR} + \text{OutputSR} \le \text{MaxSupplySR}
$$

## $SSR

$SSR token can be used for staking.
The staked amount will be calculated as a voting power for the governance.

* Ticker: SSR
* Denom in the blockchain: `microSSR`
* Supply in genesis block: 1,000,000,000SSR = `1_000_000_000_000_000microSSR`

### Usecases

#### Staking

$SSR can be staked to the Sunrise network. The staked amount will be calculated as a voting power for the governance. Furthermore, the rewards for stakers will be distributed in proportion to the staked amount.

### Inflation rate schedule

#### On chain parameters

The actual inflation rate will vary from the target inflation rate according to the bonded ratio.

|               |     |
| ------------- | --- |
| Max inflation | 10% |
| Min inflation | 6%  |

#### Off chain parameters

|                            |    |
| -------------------------- | -- |
| Disinflation rate per year | 8% |
| Converged inflation        | 2% |

### Simulations

#### Low bonded ratio

| Year | Inflation  |
| ---- | ---------- |
| 0    | 10.000000% |
| 1    | 9.200000%  |
| 2    | 8.464000%  |
| 3    | 7.786880%  |
| 4    | 7.163930%  |
| 5    | 6.590815%  |
| 6    | 6.063550%  |
| 7    | 5.578466%  |
| 8    | 5.132189%  |
| 9    | 4.721614%  |
| 10   | 4.343885%  |
| 11   | 3.996374%  |
| 12   | 3.676664%  |
| 13   | 3.382531%  |
| 14   | 3.111928%  |
| 15   | 2.862974%  |
| 16   | 2.633936%  |
| 17   | 2.423221%  |
| 18   | 2.229364%  |
| 19   | 2.051014%  |

#### High bonded ratio

| Year | Inflation |
| ---- | --------- |
| 0    | 6.000000% |
| 1    | 5.520000% |
| 2    | 5.078400% |
| 3    | 4.672128% |
| 4    | 4.298358% |
| 5    | 3.954489% |
| 6    | 3.638130% |
| 7    | 3.347080% |
| 8    | 3.079313% |
| 9    | 2.832968% |
| 10   | 2.606331% |
| 11   | 2.397824% |
| 12   | 2.205998% |
| 13   | 2.029518% |
| 14   | 2.000000% |
| 15   | 2.000000% |
| 16   | 2.000000% |
| 17   | 2.000000% |
| 18   | 2.000000% |
| 19   | 2.000000% |

## Supported wallet applications

### Wallets that support Cosmos blockchains

* Keplr
* Leap
* XDEFI

### Command Line Interface (CLI)

* sunrised

## Listed exchanges

* Coming soon
