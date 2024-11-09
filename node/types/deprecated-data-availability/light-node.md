# Sunrise Light Node

The Light nodes ensure data availability. This is the most common way to interact with Sunrise networks.

## Hardware requirements

The following hardware minimum requirements are recommended for running the Light node:

- Memory: 500 GB RAM (minimum)
- CPU: 2 cores
- Disk: 50 GB SSD Storage
- Bandwidth: 56 Kbps for Download/56 Kbps for Upload

## Dependencies

The tutorial is done on Ubuntu 22.04 (LTS).
Follow [the environment tutorial](../../resources/enviromant.md)

## Run the Light node

### Install

```bash
git clone https://github.com/sunriselayer/sunrise-da.git
cd sunrise-da
git checkout $TAG
make build
sudo make install
```

### Initialize

```bash
sunrise light init --p2p.network <NETWORK>
```

example:

```bash
sunrise light init --p2p.network private
```

### Run the Node

Start the light node with a connection to a validator node's gRPC endpoint (normally port :9090):

```bash
sunrise light start --core.ip <URI> --p2p.network <NETWORK>
```

example:

```bash
sunrise light start --core.ip sunrise-private-2.cauchye.net --p2p.network private
```
