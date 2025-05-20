# Fee

The `x/fee` module is a core component of the Sunrise blockchain responsible for managing transaction fees. It introduces mechanisms for burning a portion of $RISE tokens used as fees, and enforcing fee denominations. This module supports deflationary tokenomics while maintaining an efficient fee system.

## Key Features of `x/fee`

1. **Burn Mechanism:**

   - A portion of $RISE tokens used as transaction fees is burned to reduce the circulating supply.
   - The burn ratio is determined by the `burn_ratio` parameter (default: 50%).
   - Burn operations are atomic and verified on-chain.

1. **Fee Denomination (`fee_denom`):**

   - Specifies the denomination required for transaction fees (default: **`"urise"`**).
   - Transactions must pay fees in this denomination unless bypassed.
   - Strict validation of fee denominations is enforced.

1. **Dynamic Parameter Configuration:**
   - Developers can configure parameters dynamically with validation enforced by the module.
   - Parameters can be updated through governance proposals.

## Core Functionality

### Fee Collection and Processing

**Fee Collection Process:**

1. Fees are collected through the FeeCollector module account
2. The system validates:
   - Only one fee denomination per transaction
   - Fee denomination matches configured `fee_denom`
   - Fee amount is valid and non-zero

**Fee Processing Flow:**

1. Validate fees against configured parameters
2. Calculate burn amount based on burn_ratio
3. Execute burn operation for the calculated amount
4. Transfer remaining fees to fee collector

## Parameter Configuration

> **Note:** The following section covers advanced topics intended for experienced users or developers.

| Parameter    | Description                                | Default Value | Constraints                  |
| ------------ | ------------------------------------------ | ------------- | ---------------------------- |
| `fee_denom`  | Required denomination for transaction fees | `"urise"`     | Must be a valid denomination |
| `burn_ratio` | Percentage of fees to burn                 | `0.5`         | Must be between 0 and 1      |

## Workflow: Fee Processing

> **Note:** The following section covers advanced topics intended for experienced users or developers.

```mermaid
sequenceDiagram
    participant User
    participant FeeModule as x/fee Module
    participant BankKeeper as Bank Keeper
    participant FeeCollector as Fee Collector
    participant BribeModule as x/bribe Module

    User->>FeeModule: Submit Transaction
    FeeModule->>BankKeeper: Validate Fee Denomination
    BankKeeper->>FeeCollector: Transfer Fees
    FeeModule->>FeeModule: Calculate Burn Amount
    FeeModule->>FeeModule: Execute Burn
    BribeModule->>FeeModule: Process Unclaimed Bribes
    FeeModule->>FeeCollector: Transfer Unclaimed Amounts
```

For more details and implementation specifics, see the [GitHub repository](https://github.com/sunriselayer/sunrise/tree/main/x/fee).
