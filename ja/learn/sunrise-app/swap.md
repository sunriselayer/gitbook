# Swap

Sunrise's Swap feature is a powerful tool for directly exchanging tokens across different blockchains. It utilizes IBC and other cross-chain technologies to provide a seamless asset exchange experience.

The swap page has two main functions:

- **Inter-Blockchain Swap**: Exchange assets between different chains (e.g., Cosmos, Ethereum).
- **vRISE**: Convert vRISE tokens to RISE tokens.

It also provides a feature to check your past transaction history.

## Inter-Blockchain Swap

This is the standard swap feature in Sunrise. You can exchange your desired tokens between various supported blockchains.

### How to Perform a Swap

1. **Select Source and Destination**:
    - In the `From` field, select the asset you want to swap and the blockchain it's on.
    - In the `To` field, select the asset you want to receive and its blockchain.

2. **Enter the Amount**:
    - When you enter the amount of tokens you want to swap in the `From` field, the amount of tokens you will receive is automatically calculated and displayed in the `To` field.
    - Conversely, you can also enter the desired amount in the `To` field to calculate the required amount of the source token. (This reverse calculation may not be available for some routes, such as those involving EVM chains).

3. **Check Rate and Details**:
    - After entering an amount, the current exchange rate is calculated. You will be notified upon successful calculation.
    - Note that this rate is an estimate and may change by the time the transaction is included in a block.

4. **Confirm the Swap**:
    - Review the details and click the "Swap" button to approve the transaction. Wallet connection and approval are required.

### Notes and Errors

- **Fees**: Swaps may incur fees. Standard IBC transfers between chains within the Cosmos ecosystem typically do not have relay fees. However, for swaps with chains outside of Cosmos, such as Ethereum, a relay fee is incurred as it uses "IBC Eureka" from [Skip Protocol](https://docs.skip.build/go/general/fee-info). This fee is automatically included in the rate calculation.
- **Calculation Error**: If you see a "Failed to calculate swap rate" error, the amount you entered may be too low to cover the fees or too high for the liquidity pool's capacity. Try a different route or adjust the amount.
- **Clear Function**: The "Clear All" button resets all the information you have entered.

## Transaction History

You can view your past swap transaction history in a side panel by clicking the "View History" button in the upper-right corner.

- **Display**: Shows the source and destination chains, assets, transaction hashes, and timestamps.
- **Explorer**: Each transaction hash is a link to the corresponding blockchain explorer for more details.
- **Clear History**: Clicking the trash can icon allows you to delete the locally stored history. (This does not erase the on-chain record).

## vRISE to RISE Conversion

This is a dedicated feature for converting vRISE tokens to RISE tokens on a 1-to-1 basis.

- **Purpose**: Use this to convert vRISE obtained from staking or other activities back into tradable RISE.
- **How to use**: Enter the amount of vRISE you wish to convert and click the "Convert vRISE to RISE" button.
- **Direction**: This conversion is one-way only, from vRISE to RISE.
