# CosmWasm tutorial on UnUniFi

## How to use wasm CLI

First of all, install `ununifid` to use wasm CLI and [Rust](https://www.rust-lang.org/tools/install).
To learn how to install `ununifid`, see [here](../../cli/cli-introduction.md)

There are two ways of using wasm CLI.

```bash
ununifid tx wasm --help
ununifid query wasm --help
```

## Compiling and Testing a Contract

Quoted from [CosmWasm Documentation](https://docs.cosmwasm.com/docs/getting-started/compile-contract)

```bash
# Download the repository
git clone https://github.com/CosmWasm/cw-plus
cd cw-plus
git checkout main
cd contracts/cw20-ics20

# compile the wasm contract with stable toolchain
rustup default stable
cargo wasm
```

### Unit Tests

Quoted from [CosmWasm Documentation](https://docs.cosmwasm.com/docs/getting-started/compile-contract)

```bash
RUST_BACKTRACE=1 cargo unit-test
```

### Build with Optimizer

Quoted from [CosmWasm Documentation](https://docs.cosmwasm.com/docs/getting-started/compile-contract)

```bash
docker run --rm -v "$(pwd)":/code \
  --mount type=volume,source="$(basename "$(pwd)")_cache",target=/code/target \
  --mount type=volume,source=registry_cache,target=/usr/local/cargo/registry \
  cosmwasm/rust-optimizer:0.12.11
```

### Deployment and Interaction

Quoted from [CosmWasm Documentation](https://docs.cosmwasm.com/docs/getting-started/compile-contract)

To deploy your wasm smart contract that you built, use `ununifid tx wasm store` commands.

```bash
ununifid tx wasm store --help
```

Converse to Solidity smart contracts, CosmWasm has two stages to activate smart contracts. That are deploy and instantiate.
So after you deployed your wasm smart contract, use `ununifid tx wasm instantiate` commands.

```bash
ununifid tx wasm instantiate --help
```
