# Fee

The `x/fee` module in Sunrise serves as a critical component for managing transaction fees on the network, including ***burning a portion of the $RISE tokens*** used as fees. This module ensures sustainable tokenomics while maintaining an efficient fee system.

## Key Features of `x/fee`

 **Burn Mechanism:**  A portion of $RISE tokens used as transaction fees is burned, effectively reducing the circulating supply of the token.
        The amount burned is determined by the burn_ratio parameter, which specifies the percentage of each fee to be permanently removed from circulation.

**Fee Denomination (fee_denom):** The module enforces a specific denomination for transaction fees, defined in the parameter fee_denom.
        Only transactions paying fees in the specified denomination are accepted.

**Bypass Denominations (bypass_denoms):** Certain denominations can bypass the standard fee denomination restrictions, allowing additional flexibility for specialized use cases.

**Default Parameters:** The default burn_ratio is set to 0.5, meaning 50% of the transaction fees are burned.

- The default fee_denom is "urise".

- The default bypass denomination is "uvrise".

### Parameter Configuration

The x/fee module parameters can be configured dynamically, with validation enforced by the module:

**Fee Denomination (fee_denom):**

- Must be a valid, non-empty string.
- Default: "urise".

**Burn Ratio (burn_ratio):**

- Specifies the percentage of transaction fees to burn.
- Must be a non-negative value less than 1.
- Default: 0.5 (50% of fees are burned).

**Bypass Denominations (bypass_denoms):**

- List of denominations that bypass the standard fee denomination rule.
- Each denomination must be a valid, non-empty string.
- Default: ["uvrise"].

## Core Functionality

  **Fee Deduction and Burning:**

- When a transaction is processed, fees are deducted from the sender's account and sent to the fee collector module account.
- The Burn method of the feeKeeper is invoked to burn the specified portion of the fees, reducing the supply of $RISE tokens.

    ```go
    func DeductFees(bankKeeper BankKeeper, ctx sdk.Context, acc sdk.AccountI, fees sdk.Coins, feeKeeper feekeeper.Keeper) error {
    ...
    if err := feeKeeper.Burn(ctx, fees); err != nil {
    return err
    }
    ...
    }
    ```

## Benefits of the Fee Module

- **Deflationary Pressure:**
        The burning mechanism introduces deflationary pressure on $RISE tokens, supporting long-term token value.

- **Fee Flexibility:**
        Configurable parameters like bypass_denoms provide flexibility for specialized transaction scenarios.

For more details and implementation specifics, see the [GitHub repository](https://github.com/sunriselayer/sunrise/tree/main/x/fee).
