# データ可用性の証明

Sunriseのデータ可用性レイヤーはバリデーターによって検証されます。バリデーターは、無効である可能性のあるデータを検証し、その証明をチェーンに送信する必要があります。

このセクションでは、バリデーターがデータを証明する方法について説明します。

## 証明

証明が必要なデータは、MsgSubmitInvalidityが送信され、ステータスが`CHALLENGING`に変更されたものだけです。

`CHALLENGING`のしきい値は、全シャードの33%（ジェネシスのデフォルト）に対してMsgSubmitInvalidityが送信された場合です。

その後、バリデーターは検証されます。一定数以上のシャードが証明された場合、ステータスは通常通り`VERIFIED`に変わります。そうでない場合、ステータスは`REJECTED`に変わります。

データ可用性レイヤーのステータスとデータの証明については、[データ可用性](../../learn/sunrise/data-availability.md)を参照してください。

## バリデーターのためのSunrise-Data

sunrise-dataは、`CHALLENGING`になったデータを監視し、証明する機能をバリデーターに提供します。

### バリデーターの証明代理人を登録する

バリデーターは自分でtxを送信して証明データを送信できますが、キーの漏洩を防ぐために代理人アドレスを使用することをお勧めします。

まず、代理人として機能する新しいアカウントを作成します。

```bash
sunrised keys add your_deputy_account --keyring-backend=test
```

次に、`tx bank send`コマンドを使用して、このアカウントにいくらかの`uusdrise`を送信します。これは、`SubmitValidityProof`トランザクションを送信する際のガス料金の支払いに使用されます。

```bash
DEPUTY_ADDRESS=$(sunrised keys show your_deputy_account -a --keyring-backend=test)
sunrised tx bank send [your_validator_key] $DEPUTY_ADDRESS 1000000uusdrise \
    --chain-id=$CHAIN_ID \
    --gas-prices=0.025uusdrise --gas-adjustment 1.2 \
    --gas=auto \
    -y
```

最後に、バリデーターに代理人アドレスを登録します。このトランザクションは、バリデーターのアカウントから送信する必要があり、一度だけ実行すれば十分です。

```bash
sunrised tx da register-proof-deputy $DEPUTY_ADDRESS \
   --from [your_validator_key] \
   --chain-id=$CHAIN_ID \
   --gas-prices=0.025uusdrise --gas-adjustment 1.2 \
   --gas=auto \
   -y
```

`sunrise-data`で使用する代理人のアドレスを登録します。

### 設定方法

1. バリデーターとして`sunrised`を実行します。設定については、[バリデーターノード](../../run-a-sunrise-node/types/consensus/validator-node.md)を参照してください。
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
   vi config.toml
   ```

   ローカルのIPFSデーモンに接続するには、`ipfs_api_url`フィールドを空のままにします。

   `home_path`を`.sunrise`ディレクトリに、`proof_deputy_account`をsunrisedキーの名前に、`validator_address`をバリデーターアドレスに変更します。

   ```toml
   [api]
   port = 8000
   ipfs_api_url = ""
   ipfs_address_info = ""

   [chain]
   address_prefix="sunrise"
   home_path="/home/ubuntu/.sunrise"
   keyring_backend="test"
   sunrised_rpc="http://localhost:26657"

   [validator]
    proof_deputy_account="your_deputy_account"
    validator_address="sunrisevaloper1a8jcsmla6heu99ldtazc27dna4qcd4jyv75vcz"
    proof_fees="10000uusdrise"
    proof_interval=5
   ```

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

### データの証明を開始する

sunrise-dataディレクトリで、

```bash
sunrise-data validator
```

またはサービスとして登録します。

```bash
vi /etc/systemd/system/sunrise-data.service
systemctl enable sunrise-data
systemctl start sunrise-data
```

```service
[Unit]
Description = sunrise-data validator daemon
After=network-online.target

[Service]
User=ubuntu
WorkingDirectory=/home/ubuntu/sunrise-data
ExecStart = /home/ubuntu/go/bin/sunrise-data validator
Restart=on-failure
RestartSec=3
LimitNOFILE=1400000

[Install]
WantedBy = multi-user.target
```

セットアップが成功すると、表示は次のようになります。

```bash
$ sunrise-data validator
{"level":"info","time":"2025-02-19T18:32:52+09:00","message":"Starting validator task"}
{"level":"info","time":"2025-02-19T18:32:52+09:00","message":"validator: sunrisevaloper1a8jcsmla6heu99ldtazc27dna4qcd4jyv75vcz deputy: sunrise155u042u8wk3al32h3vzxu989jj76k4zcc6d03n"}
{"level":"info","time":"2025-02-19T18:32:52+09:00","message":"On-chain data is checked every 5 sec"}
```
