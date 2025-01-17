# Sunrise Data

[Sunrise Data](https://github.com/sunriselayer/sunrise-data) acts as a relay server connecting the L2 chain to the Sunrise DA layer.
In some cases, additional software is required to support the OP Stack, such as the [Sunrise OP DA Server](./op-da-server.md).

## Sunrise Consensus Node

Requires a networked Sunrise node to operate. [Networks](../../networks/README.md) running Sunrise v0.3.0 or higher support Data Availability Layer.

Follow the [Node Guide](../consensus/README.md) on how to create a consensus node.

### How to set up sunrise-data

1. Clone sunrise-data repo

   ```bash
   cd ~
   git clone https://github.com/sunriselayer/sunrise-data.git
   cd sunrise-data
   make install
   ```

1. Create and edit `config.toml`

   ```bash
   cp config.default.toml config.toml
   nano config.toml
   ```

   To connect to a local IPFS daemon, leave the `ipfs_api_url` field empty

   Chage `home_path` to your .sunrise directory and `publisher_account` to your sunrised key's name

   ```toml
   [api]
   port = 8000
   ipfs_api_url = ""
   ipfs_addrinfo = ""
   submit_challenge = true
   submit_proof = true

   [chain]
   addr_prefix="sunrise"
   keyring_backend="test"
   home_path="/home/ubuntu/.sunrise"
   publisher_account="validator" # your key name
   fees="10000uvrise"
   cometbft_rpc="http://localhost:26657" # or available RPC
   vote_extension_period=2
   ```

1. Start Daemon

   ```bash
   sunrise-data
   ```

### Integrate IPFS

1. Run IPFS

   ```bash
   wget https://dist.ipfs.tech/kubo/v0.31.0/kubo_v0.31.0_linux-amd64.tar.gz
   tar -xvzf kubo_v0.31.0_linux-amd64.tar.gz
   cd kubo
   sudo ./install.sh
   ipfs init --profile=lowpower
   ipfs daemon
   ```

1. Check the IPFS node ID and optionally share and add a remote peer

   ```bash
   ipfs id
   ```
