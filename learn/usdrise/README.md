# $USDrise

$USDrise is the native stablecoin of the Sunrise protocol, issued by wrapping noble's USDN. This document provides an overview of USDrise, its features, and how it integrates into the Sunrise ecosystem.

## Overview

USDrise is designed to be a stable and reliable medium of exchange within the Sunrise protocol. It aims to maintain a 1:1 peg with the US Dollar. The issuance and burning of USDrise are managed by the `x/stable` module. The exchange rate for minting and burning is fixed at 1 USDN = 1 USDrise. This process ensures transparency and control over the token supply.

For more detailed information on the `x/stable` module, please refer to the [x/stable module documentation](../sunrise/stable.md).

## Key Features

- **Yield Bearing:** USDrise offers a yield equivalent to that of USDN, allowing holders to earn passive income.
- **Transaction Fees:** All transaction fees within the Sunrise protocol are paid in USDrise, making it a central component of the network's economy.

## About USDN

USDrise is backed by Noble Dollar (USDN), a stablecoin from the noble network. It is important for users to understand the mechanics and risks associated with USDN. We strongly encourage users to conduct their own research on USDN to make informed decisions.

Noble Dollar (USDN) is a stablecoin built on the foundation of composable yield. USDN leverages the M^0 Protocol to deliver stablecoin yield collateralized by short term U.S. Treasury Bills.
USDN is purpose built for the modular ecosystem and is constructed to allow yield to be directed in a customizable, programmatic and transparent fashion.

For more information, please refer to the official documentation from Noble: [Noble Dollar (USDN)](https://www.noble.xyz/usdn)

## Related Documents

- **[x/stable Module](../sunrise/stable.md)**
