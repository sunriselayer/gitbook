# Sunriseデータ

[Sunrise Data](https://github.com/sunriselayer/sunrise-data)は、L2チェーンをSunrise DAレイヤーに接続するリレーサーバーとして機能します。

## Sunriseコンセンサスノード

動作には、ネットワーク化されたSunriseノードが必要です。Sunrise v0.3.0以降を実行している[ネットワーク](../../../run-a-sunrise-node/networks/)は、データ可用性レイヤーをサポートしています。

コンセンサスノードの作成方法については、[ノードガイド](../../../run-a-sunrise-node/types/consensus/)に従ってください。

### sunrise-dataの設定方法

1. `sunrised`を実行します。設定については、[コンセンサスノード](https://github.com/SunriseLayer/gitbook/blob/main/build/node/types/consensus/full-consensus-node.md)を参照してください。
2. sunrise-dataリポジトリをクローンします。

   ```bash
   cd ~
   git clone https://github.com/sunriselayer/sunrise-data.git
   cd sunrise-data
   make install
   ```

3. `config.toml`を作成して編集します。

   ```bash
   cp config.default.toml config.toml
   nano config.toml
   ```

   ローカルのIPFSデーモンに接続するには、`ipfs_api_url`フィールドを空のままにします。

   `home_path`を`.sunrise`ディレクトリに、`publisher_account`をsunrisedキーの名前に変更します。

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

`home_path`、`keyring_backend`、`publisher_account`は、sunrisedキーリングで入力された値でなければなりません。[ローカルキーペアのドキュメント](../../../run-a-sunrise-node/types/consensus/full-consensus-node.md#create-or-restore-a-local-key-pair)を参照し、`--keyring-backend test`オプションで設定してください。`home_path`には、sunriseキーリングが存在するパスを入力してください。`sunrised_rpc`については、ローカルでsunrisedを実行することが望ましいですが、不可能な場合は公開されているRPCを使用してください。私たちの[ネットワークドキュメント](../../../run-a-sunrise-node/networks/)を参照してください。このような場合でも、ローカルキーペアは必要です。

その他のフィールドはそのままにしておくことができます。

### ローカルでIPFSを実行する

1. IPFSを実行します。

   ```bash
   wget https://dist.ipfs.tech/kubo/v0.31.0/kubo_v0.31.0_linux-amd64.tar.gz
   tar -xvzf kubo_v0.31.0_linux-amd64.tar.gz
   cd kubo
   sudo ./install.sh
   ipfs init --profile=lowpower
   ipfs daemon
   ```

2. IPFSノードIDを確認し、オプションでリモートピアを共有して追加します。

   ```bash
   ipfs id
   ```

### 開始

```bash
sunrise-data optimism
```
