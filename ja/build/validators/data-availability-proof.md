# データ可用性層の証明

Sunriseのデータ可用性層はバリデータによって検証されます。バリデータは有効でない可能性のあるデータを検証し、その証明をチェーンに送信する必要があります。

このセクションでは、バリデータがどのようにデータを証明するかについて説明します。

## 証明

証明が必要なデータは、MsgSubmitInvalidityが送信され、ステータスが`CHALLENGING`に変更されたものだけです。

`CHALLENGING`の閾値は、全シャードの33%（ジェネシスのデフォルト）に対してMsgSubmitInvalidityが送信された場合です。

その後、バリデータが検証されます。一定数以上のシャードが証明された場合、ステータスは通常通り`VERIFIED`に変更されます。そうでない場合、ステータスは`REJECTED`に変更されます。

データ可用性層におけるステータスとデータの証明については、[データ可用性](../../learn/sunrise/data-availability.md)を参照してください。

## バリデータのためのsunrise-data

sunrise-dataは、バリデータに`CHALLENGING`になったデータをモニタリングし証明する機能を提供します。

### バリデータの証明代理を登録する

バリデータは自身でトランザクションを送信してデータを証明することもできますが、鍵の漏洩を防ぐために代理アドレスを使用することをお勧めします。

```bash
sunrised tx da register-proof-deputy [deputy_address] \
   --from [your_validator_key] \
   --chain-id=$CHAIN_ID \
   --fees=21000urise \
   --gas=220000
```

登録するには、`sunrised`でバリデータキーを使用してトランザクションを一度だけ送信する必要があります。
`sunrise-data`で使用する代理のアドレスを登録します。

### セットアップ方法

1. バリデータとして`sunrised`を実行する
セットアップについては[バリデータノード](../../node/types/consensus/validator-node.md)を参照してください。

1. sunrise-dataリポジトリをクローンする

   ```bash
   cd ~
   git clone https://github.com/sunriselayer/sunrise-data.git
   cd sunrise-data
   make install
   ```

1. `config.toml`を作成して編集する

   ```bash
   cp config.default.toml config.toml
   vi config.toml
   ```

   ローカルのIPFSデーモンに接続するには、`ipfs_api_url`フィールドを空のままにしておきます

   `home_path`を.sunriseディレクトリに、`proof_deputy_account`をsunrisedキーの名前に、`validator_address`をバリデータアドレスに変更します。

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
    proof_fees="10000urise"
    proof_interval=5
   ```

### ローカルでIPFSを実行する

1. IPFSを実行する

   ```bash
   wget https://dist.ipfs.tech/kubo/v0.31.0/kubo_v0.31.0_linux-amd64.tar.gz
   tar -xvzf kubo_v0.31.0_linux-amd64.tar.gz
   cd kubo
   sudo ./install.sh
   ipfs init --profile=lowpower
   ipfs daemon
   ```

1. IPFSノードIDを確認し、必要に応じてリモートピアを共有して追加する

   ```bash
   ipfs id
   ```

### データの証明を開始する

sunrise-dataディレクトリで、

```bash
sunrise-data validator
```

またはサービスとして登録する

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

セットアップが成功すると、表示は次のようになります

```bash
$ sunrise-data validator
{"level":"info","time":"2025-02-19T18:32:52+09:00","message":"Starting validator task"}
{"level":"info","time":"2025-02-19T18:32:52+09:00","message":"validator: sunrisevaloper1a8jcsmla6heu99ldtazc27dna4qcd4jyv75vcz deputy: sunrise155u042u8wk3al32h3vzxu989jj76k4zcc6d03n"}
{"level":"info","time":"2025-02-19T18:32:52+09:00","message":"On-chain data is checked every 5 sec"}
```