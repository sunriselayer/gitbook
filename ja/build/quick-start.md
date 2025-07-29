# 🚀 Quick Start

> Get a local Sunrise DA node, a minimal Rollkit‑based sovereign rollup,
> and a sample dApp running in **≤ 20 minutes**.

> **Note**: For a comprehensive guide covering all aspects of building on Sunrise, including detailed module references, and advanced integration patterns, check out the [Sunrise Builders Kit](https://cauchye.notion.site/Sunrise-Builders-Kit-1e02cd22bc1680f3bebcd4f02f2fbc18?pvs=4).

This guide will walk you through setting up a complete development environment for building on Sunrise Layer. You'll learn how to:

- Set up a local Sunrise Data Availability (DA) node
- Create a minimal sovereign rollup using Rollkit
- Interact with the network using the Sunrise client
- Run a sample dApp that demonstrates key features

For a more comprehensive guide covering all aspects of building on Sunrise, check out the [Sunrise Builders Kit](https://cauchye.notion.site/Sunrise-Builders-Kit-1e02cd22bc1680f3bebcd4f02f2fbc18?pvs=4).

---

## Prerequisites

Before you begin, ensure you have the following tools installed:

| Tool | Version | Purpose |
|------|---------|---------|
| **Go** | `>=1.22` | Build Sunrise binaries and core components |
| **Rust + Cargo** | stable | Build Rollkit demo chain and smart contracts |
| **Node.js** | `>=20` | Run JS client, scripts, and web applications |
| **Docker + Docker Compose** | latest | Run containerized services and development stack |
| (Optional) **direnv** | any | Automatically load environment variables in your shell |

```bash
# macOS (brew) example
brew install go rustup node docker direnv
rustup default stable
```

## 1. Clone the repositories

We'll create a development playground with three main components:

```bash
mkdir sunrise-playground && cd $_
git clone https://github.com/sunriselayer/network     sunrise-da
git clone https://github.com/rollkit/rollkit          rollkit
git clone https://github.com/sunriselayer/examples    examples
```

- `sunrise-da`: The core Sunrise network implementation
- `rollkit`: A framework for building sovereign rollups
- `examples`: Sample applications and integration examples

## 2. Spin up a local Sunrise DA node

The Sunrise DA node is the foundation of the network, providing data availability services for rollups:

```bash
cd sunrise-da
make install             # builds 'sunrised'
sunrised init dev --chain-id goldberg-local
sunrised start
```

> Tip: want it in Docker instead?
>
> ```bash
> docker compose -f docker/local-da.yml up --build
> ```

### Ports

| Service | Port | Purpose |
|---------|------|---------|
| Tendermint RPC | 26657 | Main RPC endpoint for transactions and queries |
| gRPC | 9090 | Protocol buffer interface for advanced operations |

## 3. Fund an account (faucet)

Create and fund a test account to interact with the network:

```bash
sunrised keys add alice --keyring-backend test
sunrised tx bank mint $(sunrised keys show alice -a) 1000000000urise \
  --from alice --keyring-backend test --yes
```

This creates a new account named "alice" and mints 1 billion micro-RISE tokens (`urise`) for testing.

## 4. Launch a minimal Rollkit sovereign rollup

Rollkit is a framework for building sovereign rollups that can use Sunrise for data availability:

```bash
cd ../rollkit
make demo                # builds demo binary 'demo-rollup'

# Configure Rollkit to store blobs on Sunrise DA
cat <<EOF > rollup.config.toml
[da]
rpc_address = "http://localhost:26657"
fee_denom   = "uusdrise"
gas_price   = "0.025"
[rollup]
chain_id = "demo-rollup-1"
EOF

./demo-rollup start --config rollup.config.toml
```

The rollup automatically publishes its block data to Sunrise and retrieves DA proofs.

## 5. Post and verify a blob with @sunriselayer/client

The Sunrise client is a JavaScript/TypeScript library for interacting with the Sunrise network. Here's how to use it:

```bash
# inside the root playground directory
npm create vite@latest js-client-demo -- --template vanilla
cd js-client-demo && npm i @sunriselayer/client

cat <<'JS' > src/index.js
import { SunriseClient } from "@sunriselayer/client";

const rpc = "http://localhost:26657";
const main = async () => {
  const client = await SunriseClient.connect(rpc);

  const { transactionHash } = await client.da.submitBlob(
    "Hello Sunrise!",
    { gasLimit: 200_000, feeDenom: "uusdrise", gasPrice: "0.025" }
  );
  console.log("Blob tx:", transactionHash);

  const proof = await client.da.getBlobProof(transactionHash);
  console.log("Inclusion proof:", proof);
};
main();
JS
node src/index.js
```

This example demonstrates:

- Connecting to a Sunrise node
- Submitting a data blob
- Retrieving a Merkle proof of inclusion

## 6. Run the sample dApp (token swap)

The example dApp demonstrates a token swap using Sunrise's liquidity pool module:

```bash
cd ../../examples/swap-demo
npm i
npm run dev        # opens http://localhost:5173
```

The demo UI:

- connects to @sunriselayer/client
- swaps test‑tokens via the rollup's x/swap module
- shows live balances pulled from Sunrise DA

## 7. Next steps

| What | Where | Description |
|------|-------|-------------|
| Full client reference | [Client Documentation](/build/client/README.md) | Complete API documentation for @sunriselayer/client |
| Build a production Rollkit chain | [Rollkit Guide](/build/l2-blockchains/rollkit/README.md) | Guide to deploying a production rollup |
| Validators & DA proofs | [Validators Guide](/build/validators/README.md) | Learn about validator setup and DA proof generation |
| Conceptual deep dives | [Learn Section](/learn/sunrise/README.md) | Understanding Sunrise's core concepts |

## Troubleshooting

| Symptom | Fix | Explanation |
|---------|-----|-------------|
| ECONNREFUSED on port 26657 | sunrised start not running or wrong RPC URL | Ensure the Sunrise node is running and accessible |
| Rollkit cannot post blobs | Check ~/.sunrise/config/app.toml for min-gas-prices | Verify gas price settings match network requirements |
| Blob tx stuck in mempool | Low gas price → use --gas-prices 0.025urise | Increase gas price to ensure transaction processing |

## Clean up

```bash
pkill sunrised demo-rollup || true
docker compose -f docker/local-da.yml down -v || true
rm -rf ~/sunrise-playground
```

Happy hacking! 🎉
