# Sunrise Bridge Node

The Bridge nodes connect the data availability layer and the consensus layer.

## Hardware requirements

The following hardware minimum requirements are recommended for running the bridge node:

- Memory: 4 GB RAM (minimum)
- CPU: 6 cores
- Disk: 10 TB SSD Storage
- Bandwidth: 1 Gbps for Download/1 Gbps for Upload

## Dependencies

The tutorial is done on Ubuntu 22.04 (LTS).
Follow [the environment tutorial](../../resources/enviromant.md)

## Run the bridge node

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
sunrise bridge init --core.ip <URI> --p2p.network <NETWORK>
```

The `--core.ip` gRPC port defaults to 9090. You can add the port after the IP address or use the `--core.grpc.port` flag to specify another port.
Refer to [the Resource page](../../resources/README.md) for information on which ports are required to be open.

example:

```bash
sunrise bridge init --core.ip sunrise-private-2.cauchye.net --p2p.network private
```

### Run the Node

Start the bridge node with a connection to a validator node's gRPC endpoint (normally port :9090):

```bash
sunrise bridge start --core.ip <URI> --p2p.network <NETWORK>
```

example:

```bash
sunrise bridge start --core.ip sunrise-private-2.cauchye.net --p2p.network private
```
