# Sunrise Client SDKs

The Sunrise client libraries let you **query** the chain, **submit blobs** and **sign / broadcast transactions** from your application without having to run custom protobuf tooling or hand‑craft Tendermint JSON‑RPC calls.

## Available SDKs

* **JavaScript / TypeScript** - Primary SDK available on npm
* **Rust** - gRPC + protobuf type generation with Buf/Prost
* **Go** and **Python** bindings - Coming soon (contributions welcome)

## JavaScript / TypeScript SDK

[Sunrise Client](https://github.com/sunriselayer/sunrise-client-js)

### Installation

```bash
npm install @sunriselayer/client @cosmjs/proto-signing @cosmjs/stargate
# or
pnpm add @sunriselayer/client @cosmjs/proto-signing @cosmjs/stargate
# or
yarn add @sunriselayer/client @cosmjs/proto-signing @cosmjs/stargate
```

### Basic Usage

The client is designed to be used with [CosmJS](https://cosmos.github.io/cosmjs/), the standard library for interacting with Cosmos SDK chains.

Here's an example of how to create a concentrated liquidity position:

```typescript
import {
  createEncodeObject,
  sunriseTypesRegistry,
} from "@sunriselayer/client";
// The schemas and types for all modules are exported from the client.
// Here, we import the schema for the `MsgCreatePosition` message.
import { MsgCreatePositionSchema } from "@sunriselayer/client/types/liquiditypool";
import { DirectSecp256k1HdWallet } from "@cosmjs/proto-signing";
import { SigningStargateClient, coin } from "@cosmjs/stargate";

const RPC = "https://goldberg-rpc.sunrise.node"; // Replace with your node
const SENDER_MNEMONIC = process.env.MNEMONIC!;   // Never commit private keys

// This is a simplified example. In a real application, you would fetch pool details
// from a query client and calculate ticks from user-provided prices.
const MOCK_POOL_ID = 1n; // NOTE: Use BigInt for uint64 fields
const MOCK_LOWER_TICK = -20000n;
const MOCK_UPPER_TICK = 20000n;

async function main() {
  // 1. Create a wallet and a signer from a mnemonic
  const signer = await DirectSecp256k1HdWallet.fromMnemonic(SENDER_MNEMONIC, {
    prefix: "sunrise", // The Bech32 address prefix for Sunrise
  });
  const [account] = await signer.getAccounts();
  const senderAddress = account.address;
  console.log("Sender address:", senderAddress);

  // 2. Create a signing client with the signer and type registry
  const client = await SigningStargateClient.connectWithSigner(RPC, signer, {
    registry: sunriseTypesRegistry, // The custom type registry for Sunrise messages
  });
  console.log("Successfully connected to", RPC);

  // 3. Prepare a 'Create Position' transaction message
  // All message fields are fully typed and validated.
  const msg = createEncodeObject(MsgCreatePositionSchema, {
    sender: senderAddress,
    poolId: MOCK_POOL_ID,
    lowerTick: MOCK_LOWER_TICK,
    upperTick: MOCK_UPPER_TICK,
    // Use the `coin` helper from @cosmjs/stargate to create Coin objects
    tokenBase: coin("1000000", "urise"), // 1 RISE
    tokenQuote: coin("5000000", "uusdc"), // 5 USDC (example)
    minAmountBase: "0", // Slippage protection
    minAmountQuote: "0", // Slippage protection
  });

  // 4. Define the fee and sign and broadcast the transaction
  const fee = {
    amount: [coin("10000", "urise")],
    gas: "400000", // Gas limit
  };
  const memo = "Created position via @sunriselayer/client";

  console.log("Broadcasting transaction...");
  const { transactionHash } = await client.signAndBroadcast(
    senderAddress,
    [msg],
    fee,
    memo
  );

  console.log("Successfully created position!");
  console.log("Transaction hash:", transactionHash);
}

main().catch(console.error);
```

All methods are fully typed when using TypeScript.

## Rust SDK (Coming Soon)

The Rust SDK is currently implemented through protobuf generation. Here's how to set it up:

### Project Structure

```
my-sunrise-client/
├── src/
│   └── main.rs
├── buf.yaml
└── buf.gen.yaml
```

### Configuration Files

1. `buf.yaml`:

```yaml
version: v2
deps:
  - buf.build/cosmos/cosmos-sdk
  - buf.build/cosmos/cosmos-proto
  - buf.build/cosmos/gogo-proto
  - buf.build/protocolbuffers/wellknowntypes
```

2. `buf.gen.yaml`:

```yaml
version: v2
managed:
  enabled: true

plugins:
  - remote: buf.build/community/neoeinstein-prost:v0.4.0
    out: src
    opt:
      - compile_well_known_types
      - extern_path=.google.protobuf=::pbjson_types
  - remote: buf.build/community/neoeinstein-prost-serde:v0.3.1
    out: src
  - remote: buf.build/community/neoeinstein-tonic:v0.4.1
    out: src
    opt:
      - compile_well_known_types
      - extern_path=.google.protobuf=::pbjson_types

inputs:
  - git_repo: https://github.com/sunriselayer/sunrise.git
    branch: main
    subdir: proto
```

### Setup and Generation

```bash
# Add required dependencies
cargo add tonic tonic-build pbjson-types

# Update dependencies and generate code
buf dep update
buf generate
```

### Example Usage

```rust
use tonic::transport::Channel;
use sunriselayer::sunrise::da::v1::query_client::QueryClient;
use sunriselayer::sunrise::da::v1::ParamsRequest;

#[tokio::main]
async fn main() -> anyhow::Result<()> {
    let mut client = QueryClient::connect("http://localhost:9090").await?;
    let resp = client.params(ParamsRequest {}).await?;
    println!("DA params: {:?}", resp.into_inner());
    Ok(())
}
```

## Additional Resources

* [Full JavaScript Method Reference](/build/client/reference)
* [Rollup Integration Examples](/build/l2-blockchains)
* [Data Availability Proofs](/build/validators)

## Troubleshooting

| Problem | Solution |
|---------|----------|
| Connection refused | Verify RPC URL and ensure DA node is running |
| Authentication error | Ensure account has sufficient funds |
| Rust build failure | Update to Rust 1.74+ and run `cargo clean && buf generate` |
