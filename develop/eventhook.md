# Event Hook contracts

Under construction.

## Basic idea

The `eventhook` module on UnUniFi can call a functionality of the smart contracts that are registered as a **Hook**.
When every block ends, the module will inspect all events that are emitted on that block, and call hooks that designated the type of the event.

By using this module, you can make smart contracts that react to events emitted by other smart contracts or core modules.
For example, you can realize

- "Automatic bid pool for designated NFT class" for NFT backed loan module, by reacting to `nft_listing` event emitted by `nftbackedloan` module.
  - If you create a pool for bidding to "A NFT that means it is a dummy NFT for no collateral loan", you can realize unsecured loan on `nftbackedloan` module.
- "Copy trading for designated address" for derivatives module, by reacting to `open_position` event emitted by `derivatives` module.

Hook contracts have to follow the interface described below.

```rust
pub enum ExecuteMsg {
    HandleEvent(HandleEventMsg),
}

#[derive(Serialize, Deserialize, Clone, Debug, PartialEq, JsonSchema)]
pub struct HandleEventMsg {
    pub event_type: String,
    pub event_attributes: HashMap<String, String>,
}
```
