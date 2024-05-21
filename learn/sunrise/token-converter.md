# TokenConverter

$SR can be minted by burning $SSR 1 to 1 if the following rule satisfies

$$
  \text{if} \ \text{CurrentSupplySR} + \text{OutputSR} \le \text{MaxSupplySR}
$$

## MsgConvertExactAmountIn

By sending tx with this msg, users can convert $SSR to $SR with designating the amount of $SSR for input.

## MsgConvertExactAmountOut

By sending tx with this msg, users can convert $SSR to $SR with designating the amount of $SR for output.
