# Sunrise Data

[Sunrise Data](https://github.com/sunriselayer/sunrise-data) acts as a relay server connecting the L2 chain to the Sunrise DA layer.

## Sunrise Consensus Node

Requires a networked Sunrise node to operate. [Networks](../../../run-a-sunrise-node/networks/) running Sunrise v0.3.0 or higher support Data Availability Layer.

Follow the [Node Guide](../../../run-a-sunrise-node/types/consensus/) on how to create a consensus node.

### How to set up sunrise-data

1. Running `sunrised` See [Consensus Node](https://github.com/SunriseLayer/gitbook/blob/main/build/node/types/consensus/full-consensus-node.md) for setting up.
2.  Clone sunrise-data repo

    ```bash
    cd ~
    git clone https://github.com/sunriselayer/sunrise-data.git
    cd sunrise-data
    make install
    ```
3.  Create and edit `config.toml`

    ```bash
    cp config.default.toml config.toml
    nano config.toml
    ```

    To connect to a local IPFS daemon, leave the `ipfs_api_url` field empty

    Change `home_path` to your .sunrise directory and `publisher_account` to your sunrised key's name

    ```toml
    [api]
    port = 8000
    ipfs_api_url = ""
    ipfs_addrinfo = ""

    [chain]
    address_prefix="sunrise"
    home_path="/home/ubuntu/.sunrise"
    keyring_backend="test"
    sunrised_rpc="http://localhost:26657"

    [publish]
    publisher_account="your_publisher_account"
    publish_fees="10000uusdrise"

    [optimism]
    listen_address="127.0.0.1"
    port=3100
    data_shard_count=10
    parity_shard_count=10
    ```

　 `home_path`, `keyring_backend`, `publisher_account` must be entered values on your sunrised keyring. See [Local Key Pair document](../../../run-a-sunrise-node/types/consensus/full-consensus-node.md#create-or-restore-a-local-key-pair) and set with `--keyring-backend test` option. For `home_path`, enter the path where the sunrise keyring exists. 　 For `sunrised_rpc`, it is preferable to run sunrised locally, but if this is not possible, use the published RPC. See our [Network Document](../../../run-a-sunrise-node/networks/). A local key pair is still required in such cases.

The other fields can be left as is.

### Run IPFS on local

1.  Run IPFS

    ```bash
    wget https://dist.ipfs.tech/kubo/v0.31.0/kubo_v0.31.0_linux-amd64.tar.gz
    tar -xvzf kubo_v0.31.0_linux-amd64.tar.gz
    cd kubo
    sudo ./install.sh
    ipfs init --profile=lowpower
    ipfs daemon
    ```
2.  Check the IPFS node ID and optionally share and add a remote peer

    ```bash
    ipfs id
    ```

### Start

```bash
sunrise-data optimism
```
