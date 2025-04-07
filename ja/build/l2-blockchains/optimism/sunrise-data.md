# OP Stack向けSunrise Data

[Sunrise Data](https://github.com/sunriselayer/sunrise-data)は、L2チェーンをSunrise DAレイヤーに接続するリレーサーバーとして機能します。

## Sunriseコンセンサスノード

動作にはネットワーク接続されたSunriseノードが必要です。Sunrise v0.3.0以上を実行している[ネットワーク](../../networks/README.md)はデータ可用性レイヤーをサポートしています。

コンセンサスノードの作成方法については[ノードガイド](../consensus/README.md)をご参照ください。

### sunrise-dataのセットアップ方法

1. `sunrised`の実行
設定に関しては[コンセンサスノード](../../node/types/consensus/full-consensus-node.md)をご参照ください。

1. sunrise-dataレポジトリのクローン

   ```bash
   cd ~
   git clone https://github.com/sunriselayer/sunrise-data.git
   cd sunrise-data
   make install
   ```

1. `config.toml`の作成と編集

   ```bash
   cp config.default.toml config.toml
   nano config.toml
   ```

   ローカルのIPFSデーモンに接続するには、`ipfs_api_url`フィールドを空のままにしておきます

   `home_path`を.sunriseディレクトリに、`publisher_account`をsunrisedキーの名前に変更します

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
   publish_fees="10000urise"

   [optimism]
   listen_address="127.0.0.1"
   port=3100
   data_shard_count=10
   parity_shard_count=10
   ```

   その他のフィールドはそのままにしておくことができます。

### ローカルでIPFSを実行する

1. IPFSの実行

   ```bash
   wget https://dist.ipfs.tech/kubo/v0.31.0/kubo_v0.31.0_linux-amd64.tar.gz
   tar -xvzf kubo_v0.31.0_linux-amd64.tar.gz
   cd kubo
   sudo ./install.sh
   ipfs init --profile=lowpower
   ipfs daemon
   ```

1. IPFSノードIDを確認し、必要に応じてリモートピアを共有および追加する

   ```bash
   ipfs id
   ```

### 起動

```bash
sunrise-data optimism
```