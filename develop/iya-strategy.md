# Strategy contracts for Interchain Yield Aggregator

{% hint style="info" %}
This feature is available on the mainnet!
{% endhint %}

## Basic idea

The `yieldaggregator` module on UnUniFi can call a functionality of the smart contracts that are registered as a **Strategy**.
When users deposit their funds into the **Vault** on `yieldaggregator` module, the module will automatically allocate the funds to strategies that are contained in the **Vault**.
Strategy contracts satisfies the specific interface described [here](./iya-strategy/strategy-interface.md).

Example source codes are [here](https://github.com/UnUniFi/contracts/tree/main/contracts/strategy-example).

### Interchain Strategy

Strategies that can completely run only on UnUniFi chain without interoperability, can be developed easily by the way described [here](./iya-strategy/strategy-interface.md).

However, developing interchain strategy only with CosmWasm smart contract on UnUniFi is not impossible but difficult.
It is because Strategy contracts need to manage Interchain Account and Interchain Query, or something like that on EVM chains.

To mitigate the difficulty, you can combine some ways to develop strategy contracts.

- Developing contract on external CosmWasm chain with IBC Hooks
- Developing contract on external EVM chain with Axelar

### Combination with contract on external CosmWasm chain

This way can be used for CosmWasm chains that is not requiring governance gate for deploying CosmWasm contracts, and supporting IBC Hooks module.
For example, Neutron.

Development of IYA Strategy requires the knowledge of [CosmWasm](../develop/cosmwasm.md).

Details are described in [here](./iya-strategy/strategy-external-cosmwasm-ibchooks.md).

### Combination with contract on external EVM chain

This way can be used for EVM chains.
For example, Ethereum, Arbitrum, Avalanche c-chain, and Polygon.

Details are described in [here](./iya-strategy/strategy-external-evm-axelar.md).

### Only with CosmWasm Strategy contract on UnUniFi

This way will be used for the strategy contracts that can't choose other ways.
For example, Osmosis chain needs governance gate for deploying CosmWasm contracts.
To avoid it, Osmosis LP farming strategy contract is developed with this way.

For example, Sei chain doesn't support IBC Hooks.
So, for example, Astroport LP farming strategy contract will be developed with this way.

#### Osmosis LP farming Strategy

Source codes are [here](https://github.com/UnUniFi/contracts/tree/main/contracts/strategy-osmosis).

## Proposal to register strategy

Under construction.

If it is urgent, please contact us directly.
