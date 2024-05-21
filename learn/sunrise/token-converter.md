# TokenConverter

$SR can be minted by burning $SSR with the following rule.

$$
  \text{OutputSR} = \text{InputSSR} \times \min\left(1, \frac{\text{MaxSupplySR}}{\text{CurrentSupplySSR}} \right) \ \text{if} \ \text{CurrentSupplySR} + \text{OutputSR} \le \text{MaxSupplySR}
$$

## MsgConvertExactAmountIn

By sending tx with this msg, users can convert $SSR to $SR with designating the amount of $SSR for input.

## MsgConvertExactAmountOut

By sending tx with this msg, users can convert $SSR to $SR with designating the amount of $SR for output.
