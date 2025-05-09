# Sunrise Client SDKs

The Sunrise client libraries let you **query** the chain, **submit blobs** and **sign / broadcast transactions** from your application without having to run custom protobuf tooling or hand‑craft Tendermint JSON‑RPC calls.

## Available SDKs

* **JavaScript / TypeScript** - Primary SDK available on npm
* **Rust** - gRPC + protobuf type generation with Buf/Prost
* **Go** and **Python** bindings - Coming soon (contributions welcome)

## JavaScript / TypeScript SDK

### Installation

```bash
npm install @sunriselayer/client
# or
pnpm add @sunriselayer/client
# or
yarn add @sunriselayer/client
```

### Basic Usage

```typescript
import { SunriseClient } from "@sunriselayer/client";

const RPC = "https://goldberg-rpc.sunrise.node";   // Replace with your node
const SENDER_MNEMONIC = process.env.MNEMONIC!;     // Never commit private keys

async function main() {
  // 1. Connect to the network
  const client = await SunriseClient.connect(RPC);

  // 2. Query chain parameters
  const params = await client.da.params({});
  console.log("DA params:", params);

  // 3. Submit a test blob transaction
  const signer = await SunriseClient.fromMnemonic(SENDER_MNEMONIC);
  const { transactionHash } = await client.da.submitBlob(
    "Hello Sunrise",
    { signer }
  );
  console.log("Transaction hash:", transactionHash);
}

main().catch(console.error);
```

All methods are fully typed when using TypeScript.

## Rust SDK

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
