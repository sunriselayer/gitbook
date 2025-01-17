# Sunrise OP DA Server

Sunrise OP DA Server connects the L2 blockchain to Sunrise's Data Availability Layer.
Currently, L2 chains created in the [OP Stack](./optimism.md) are supported.

See [OP Stack](./optimism.md) for L2 chain side configuration.

## How to set up OP DA Server

### sunrise-data

The Sunrise OP DA Server works by connecting to the Sunrise Data endpoint.
See [Sunrise Data document](./sunrise-data.md) to set it up.

### sunrise-op-da-server

1. Clone sunrise-op-da-server repo

   ```bash
   cd ~
   git clone https://github.com/sunriselayer/sunrise-op-da-server.git
   cd sunrise-op-da-server
   make install
   ```

1. Start DA Server

   ```bash
    da-server --sunrise.server=http://localhost:8000 \
    --sunrise.data_shard_count=10 \
    --sunrise.parity_shard_count=10
   ```
