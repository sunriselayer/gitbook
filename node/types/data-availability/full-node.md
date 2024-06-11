# Sunrise Full storage Node

The Full storage nodes do not connect to sunrise-app (hence not a full consensus node), but stores all the data.

## Hardware requirements

The following hardware minimum requirements are recommended for running the Full storage node:

- Memory: 4 GB RAM (minimum)
- CPU: 4 cores
- Disk: 10 TB SSD Storage
- Bandwidth: 1 Gbps for Download/1 Gbps for Upload

## Dependencies

The tutorial is done on Ubuntu 22.04 (LTS).
Follow [the environment tutorial](../../resources/enviromant.md)

## Run the Full storage node

### Install

```bash
git clone https://github.com/SunriseLayer/sunrise-da.git
cd sunrise-da
git checkout $TAG
make build
sudo make install
```

### Initialize

```bash
sunrise full init --p2p.network <NETWORK>
```

example:

```bash
sunrise full init --p2p.network private
```

### Run the Node

Start the full storage node with a connection to a validator node's gRPC endpoint (normally port :9090):

```bash
sunrise full start --core.ip <URI> --p2p.network <NETWORK>
```

example:

```bash
sunrise full start --core.ip sunrise-private-2.cauchye.net --p2p.network private
```
