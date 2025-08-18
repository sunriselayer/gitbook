# Fee

The Sunrise Chain utilizes a **Fee Abstraction** mechanism for paying transaction fees.

## Base Currency for Transaction Fees

The base currency for transaction fees on the Sunrise Chain is ![USDrise](../../.gitbook/assets/USDrise.png) **$USDrise** . All transaction fees are internally calculated and processed in USDrise.

For more details on $USDrise, please refer to this document:

* [What is USDrise?](../usdrise.md)

## Fee Abstraction

Fee Abstraction is a feature that allows users to pay transaction fees with tokens other than USDrise. This feature enables users to use the tokens they hold directly for fees.

Even when a token other than USDrise is set as the fee token using this feature, the fee displayed in your wallet (e.g., Keplr) will still be denominated in USDrise. When the transaction is executed, the selected token is automatically swapped to USDrise at the current swap rate to pay the fee.

### Available Tokens for Fees

Only tokens that have a liquidity pair with $USDrise in a liquidity pool can be set as a fee token through Fee Abstraction.

***

## How to Configure the Fee Token

You can change the token used for transaction fees from the application's settings screen.

1. **Open Settings**: Click the gear icon in the application header to open the settings menu.
2. **Fee Token Section**: In the settings menu, you will find a "Fee Token" section.
3. **Select a Token**: Choose your desired fee token from the dropdown menu. Only tokens that are swappable with $USDrise will be displayed.

After selection, future transactions will use the specified token for fees.

***

## USDrise Converter Guide

The USDrise Converter is a utility that allows eligible users to convert a fixed amount of RISE into USDrise. This is intended as a one-time opportunity for early participants in the ecosystem.

### Eligibility

To use the USDrise Converter, your wallet address must be included in the official whitelist. This list is comprised of accounts from the `genesis.json` file, which includes participants from events like the Airdrop and Public Sale.

If your connected wallet address is on the whitelist, the "USDrise Converter" button will automatically appear in the application's header. If the button is not visible, your address is not eligible.

### How to Use

1. **Connect Your Wallet**: Start by connecting the wallet that holds your whitelisted address.
2. **Find the Converter Button**: If eligible, you will see a "USDrise Converter" button in the header menu.
3. **Open the Converter**: Click the button to open the conversion dialog.
4. **Review and Confirm**: The dialog will display the fixed conversion rate:
   * **You Send**: ![RISE](../../.gitbook/assets/RISE.png) 0.625 RISE
   * **You Receive**: ![USDrise](../../.gitbook/assets/USDrise.png) 0.05 USDrise
5. **Submit the Request**: Click the "Send Request" button to proceed. The transaction will be processed, and you will receive USDrise in your wallet.

### Important Notes

* **Fixed Rate**: The conversion amounts are fixed and cannot be changed.
* **One-Time Action**: Each whitelisted address can only use the converter once.
* **TGE Price**: Please be aware that this conversion rate may be lower than the TGE (Token Generation Event) price of RISE.
