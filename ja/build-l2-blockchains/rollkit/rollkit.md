# How to run Sunrise Rollkit

As an example, here is how to use Rollkit to create an L2 chain and run it on the Sunrise's Data Availability Layer.

## Dependencies

Dependencies and general installation instructions for Ubuntu 22.04.

## Set up Sunrise Data

Rollkit support is provided via a server included in sunrise-data.
See [Rollkit documentation](https://rollkit.dev/tutorials/da/overview) for the role of the DA server.

See [Sunrise Data document](./sunrise-data.md) to set it up.
By default, the GRPC server for Rollkit support listens on port 7980.

## Run Rollkit

1. Clone rollkit repo

   ```bash
   cd ~
   git clone https://github.com/rollkit/rollkit.git
   cd rollkit
   git checkout v0.14.1 # latest major version
   make install
   ```

1. Start rollkit chain
  Use `--rollkit.da_address` option to connect to the DA server.
  The other port specification options are used to avoid conflicts when running sunrised locally.
  See [Rollkit documentation](https://rollkit.dev/) for other chain configuration.

   ```bash
   rollkit start --rollkit.aggregator \
   --rollkit.sequencer_rollup_id sunrise \
   --rollkit.da_address grpc://localhost:7980 \
   --p2p.laddr tcp://0.0.0.0:25656 --rpc.laddr tcp://127.0.0.1:25657
   ```

1. Work

## Links

- [Rollkit](https://rollkit.dev/learn/intro)
