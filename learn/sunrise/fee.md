# Fee

The `x/fee` module is a core component of the Sunrise blockchain responsible for managing transaction fees. It introduces mechanisms for burning a portion of $RISE tokens used as fees, enforcing fee denominations, and providing flexibility through bypass denominations. This module supports deflationary tokenomics while maintaining an efficient fee system.

## Key Features of `x/fee`

1. **Burn Mechanism:**
    - A portion of $RISE tokens used as transaction fees is burned to reduce the circulating supply.
    - The burn ratio is determined by the `burn_ratio` parameter (default: 50%).
    - Burn operations are atomic and verified on-chain.

2. **Fee Denomination (`fee_denom`):**
    - Specifies the denomination required for transaction fees (default: **`"urise"`**).
    - Transactions must pay fees in this denomination unless bypassed.
    - Strict validation of fee denominations is enforced.

3. **Bypass Denominations (`bypass_denoms`):**
    - Allows certain denominations to bypass standard fee restrictions.
    - Default bypass denomination: **`"uvrise"`**.
    - Useful for specialized transaction scenarios.

4. **Dynamic Parameter Configuration:**
    - Developers can configure parameters dynamically with validation enforced by the module.
    - Parameters can be updated through governance proposals.

5. **Integration with Bribe System:**
    - Handles unclaimed bribes from expired epochs
    - Processes fees from bribe transactions
    - Manages fee collection for bribe operations

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

### Integration with Bribe System

**Bribe Fee Handling:**

1. Track bribe fees through the BribeFee structure
2. Process unclaimed bribes at epoch end
3. Calculate and handle fees for unclaimed amounts
4. Transfer processed fees to appropriate accounts

## Parameter Configuration

> **Note:** The following section covers advanced topics intended for experienced users or developers.

| Parameter | Description | Default Value | Constraints |
|-----------|-------------|---------------|-------------|
| `fee_denom` | Required denomination for transaction fees | `"urise"` | Must be a valid denomination |
| `burn_ratio` | Percentage of fees to burn | `0.5` | Must be between 0 and 1 |
| `bypass_denoms` | Denominations exempt from fee restrictions | `["uvrise"]` | List of valid denominations |

## Example Usage

Developers can query fee parameters using Sunrise Client JS:

```javascript
import { SunriseClient } from "@sunriselayer/client";

async function queryFeeParams() {
    const cometRpc = "https://sunrise-test-da-1.cauchye.net/";
    const client = await SunriseClient.connect(cometRpc);
    const queryClient = client.getQueryClient();

    if (!queryClient) {
        console.error("Query client not initialized");
        return;
    }

    const feeParams = await queryClient.fee.params({});
    console.log("Fee Parameters:", feeParams.params);
}
queryFeeParams();
```

**Example Output:**

```json
{
  "fee_denom": "urise",
  "burn_ratio": "0.5",
  "bypass_denoms": ["uvrise"]
}
```

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
