# Welcome to the Sunrise App

Sunrise is a decentralized application (dApp) that provides a comprehensive suite of tools for interacting with the Sunrise blockchain and its ecosystem. This guide provides an overview of the key concepts and features to get you started.

## The Sunrise Token Trio: RISE, vRISE, and USDrise

The Sunrise ecosystem is powered by three distinct tokens, each with a specific purpose.

- ![RISE](../../images/RISE.png) **RISE**: The primary value-accrual and consensus token of the network. It can be staked to help secure the network and earn rewards.
- ![vRISE](../../images/vRISE.png) **vRISE**: The non-transferable governance and utility token. **vRISE is essential for participating in the protocol's governance.**
  - **How to Earn vRISE**: You can only earn vRISE by providing liquidity in the **[Liquidity Pool](./liquidity-pool.md)**.
  - **How to Use vRISE**: Stake your vRISE to gain voting power for **[Governance](./gov.md)** proposals and to direct liquidity pool incentives through Gauge Voting.
- ![USDrise](../../images/USDrise.png) **USDrise**: The native stablecoin of the protocol. It is used as the base currency for all transaction fees.

## Core Features

Here's a quick overview of the primary sections of the app. Each feature has its own detailed documentation page.

- **[Liquidity Pool](./liquidity-pool.md)**
  - Provide liquidity to various token pairs to earn trading fees and **vRISE rewards**. Managing your liquidity positions is the key to earning vRISE.
- **[Swap](./swap.md)**
  - Exchange tokens seamlessly across different blockchains.
- **[Governance](./gov.md)**
  - Use your staked **vRISE** to vote on governance proposals and liquidity pool incentives. You can also stake RISE to earn consensus rewards.
- **[Lockup](./lockup.md)**
  - Manage your locked tokens received from airdrops or other programs. You can stake these locked tokens to earn rewards while they vest.
- **[Point Program](./point-program/README.md)**
  - Earn points by participating in various activities within the ecosystem, such as staking, providing liquidity, and referring new users.

## Understanding Fees on Sunrise

The Sunrise Chain uses a Fee Abstraction mechanism, making transactions smooth for users.

- **USDrise is the Core Fee Token**: All transaction fees on the network are calculated and paid in USDrise.
- **Pay with (Almost) Any Token**: Thanks to Fee Abstraction, you can select another token you hold to pay for fees. The protocol automatically handles the swap to USDrise on-chain as part of the transaction.

For a more detailed explanation of how fees work and how to configure your preferred fee token, please see the **[Fee Documentation](./fee.md)**.

## Connecting Your Wallet

To get started, you'll need to connect a Cosmos wallet. Sunrise currently supports the following wallets:

- Keplr
- Leap

### How to Connect

1. Click the **"Connect Wallet"** button, usually found in the header.
2. A list of supported wallets (Keplr or Leap) will be displayed.
3. Select the wallet you want to use and approve the connection request within the wallet extension.

Once connected, your address will appear in the header, and you can click it to copy the address or disconnect.

## Settings

You can customize your app experience through the **Settings** menu, accessible via the gear icon in the header.

- **Theme**: Choose between System, Light, or Dark mode to suit your preference.
- **Fee Token**: Select which token you prefer to use for paying transaction fees.
- **Assets Visibility**: Manage which tokens from external blockchains are visible throughout the app.
- **Node Selection**: Advanced users can select specific RPC nodes to connect to for network interactions.
