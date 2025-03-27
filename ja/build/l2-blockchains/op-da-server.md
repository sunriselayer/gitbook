# Sunrise OP DA Server

Sunrise OP DA Server は L2 ブロックチェーンと Sunrise のデータ可用性レイヤーを接続するソフトウェアです。
現在、[OP Stack](./optimism.md)を使用して作成された L2 チェーンをサポートしています。

L2 側の設定については[OP Stack](./optimism.md)のページを参照してください。

## Sunrise Consensus Node

動作には Sunrise のコンセンサス・フルノードが必要です。Sunrise v0.3.0 以上を実行しているネットワークがサポートされています。

公開されている RPC か同じマシン上でコンセンサスノードを実行する必要があります。[Networks](../../networks/README.md)と[Node Guide](../consensus/README.md)のページを参照してください。

## Surnise OP DA Server のセットアップ

### sunrise-data

1. `sunrise-data`のリポジトリをクローン

   ```bash
   cd ~
   git clone https://github.com/sunriselayer/sunrise-data.git
   cd sunrise-data
   make install
   ```

1. `config.toml`を作成し、編集

   ```bash
   cp config.default.toml config.toml
   nano config.toml
   ```

   ローカル上の IPFS Daemon に接続する場合は、`ipfs_api_url`フィールドを空にします。
   `home_path`をあなたの環境の.sunrise ディレクトリに設定します。また、`publisher_account`は設定している sunrised key の名前にします。

   ```toml
   [api]
   port = 8000
   ipfs_api_url = ""
   ipfs_addrinfo = ""
   submit_challenge = true
   submit_proof = true

   [chain]
   address_prefix="sunrise"
   keyring_backend="test"
   home_path="/home/ubuntu/.sunrise"
   publisher_account="validator"
   fees="10000uvrise"
   cometbft_rpc="http://localhost:26657"
   vote_extension_period=2
   ```

1. Daemon を開始

   ```bash
   sunrise-data
   ```

### IPFS の統合

1. IPFS の実行

   ```bash
   wget https://dist.ipfs.tech/kubo/v0.31.0/kubo_v0.31.0_linux-amd64.tar.gz
   tar -xvzf kubo_v0.31.0_linux-amd64.tar.gz
   cd kubo
   sudo ./install.sh
   ipfs init --profile=lowpower
   ipfs daemon
   ```

   リモートのピアとして IPFS node ID を公開する必要がある場合は以下のコマンドで確認できます。

   ```bash
   ipfs id
   ```

### sunrise-op-da-server

1. `sunrise-op-da-server`のリポジトリをクローン

   ```bash
   cd ~
   git clone https://github.com/sunriselayer/sunrise-op-da-server.git
   cd sunrise-op-da-server
   make install
   ```

1. DA Server を開始

   ```bash
    da-server --sunrise.server=http://localhost:8000 \
    --sunrise.data_shard_count=10 \
    --sunrise.parity_shard_count=10
   ```
