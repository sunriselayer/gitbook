# Gluon Full Node

フルノードは、ネットワークのジェネシス後に Gluon メインネットに参加するための一般的な手順です。

## Chain upgrades（チェーンアップグレード）

チェーンのアップグレードを効率化し、ダウンタイムを最小限に抑えるために、[Cosmovisor](https://docs.cosmos.network/main/build/tooling/cosmovisor)を設定してノードを管理することをお勧めします。

[Cosmovisor のチュートリアル](https://docs.sunriselayer.io/run-a-sunrise-node/types/consensus/setup-cosmovisor)に従ってください。

オンチェーンアップグレードを自動化するには、次のオプションを設定してください。

```yml
DAEMON_ALLOW_DOWNLOAD_BINARIES=true
```

## Backups（バックアップ）

最近のバージョンの Cosmovisor を使用している場合、デフォルトの設定では、アップグレードを適用する前に状態のバックアップが作成されます。これを無効にするには、環境フラグを使用してください。

## Alerting and monitoring（アラートとモニタリング）

アラートと監視も望ましいため、ソリューションを検討し、自分の環境に合ったものを見つけることをお勧めします。Prometheus は標準で利用可能で、さまざまなオープンソースツールがあります。

## Hardware requirements（ハードウェア要件）

バリデータノードを実行するために、以下の最低ハードウェア要件が推奨されます：

- Memory: 32 GB RAM (もしくは同等のスワップファイルの設定が必要です)
- CPU: 8 cores (4 physical core) x86_64
- Disk: 1 TB SSD Storage (詳細は下記を参照してください)
- Bandwidth: 1 Gbps for Download/1 Gbps for Upload

アーカイブノード（`pruning = "nothing"`）には、少なくとも 64GB の専用メモリが必要です。

- アーカイブノード（`pruning = "nothing"`）は、毎月約 100GB のペースで成長します。現在の総ディスク使用量は 6TB であるため、より大容量のディスクが必要です。
- フルプルーニングノード（`pruning = "everything"`）は、毎月約 5GB のペースで成長します。
- デフォルトプルーニングノード（`pruning = "default"`）は、毎月約 25GB のペースで成長します。

## Dependencies（依存関係）

チュートリアルは Ubuntu 22.04 (LTS)で行われています。[環境設定のチュートリアル](https://github.com/SunriseLayer/gitbook/blob/main/node/resources/enviromant.md)に従ってください。

## Run the node（ノードを実行する）

### Install（インストール）

```bash
git clone https://github.com/UnUniFi/chain.git
cd chain
git checkout $TAG
make install
```

### Initialize（初期化）

`chain-id` と `moniker` を設定してください。`moniker` はノードの名前として使用されます。

```bash
CHAIN_ID=gluon-1
MONIKER="node-name"
gluond init "$MONIKER" --chain-id $CHAIN_ID
```

これにより、`~/.gluon/config/` に以下のファイルが生成されます。

- `genesis.json`
- `node_key.json`
- `priv_validator_key.json`

## Download the genesis file（ジェネシスファイルをダウンロードする）

For mainnet:

```bash
rm ~/.gluon/config/genesis.json
curl -L https://raw.githubusercontent.com/UnUniFi/network/main/launch/ununifi-beta-v1/genesis.json -o ~/.gluon/config/genesis.json
```

For testnet:

```bash
rm ~/.gluon/config/genesis.json
curl -L https://raw.githubusercontent.com/UnUniFi/network/main/launch/ununifi-test-v1/genesis.json -o ~/.gluon/config/genesis.json
```

## Option: Set persistent peers（永続的ピアを設定する）

Persistent peers（永続的ピア）は、あなたのノードが他のノードと接続し、ネットワークに参加するために必要です。選択した `chain-id`: に対応するピアを取得するには、以下の手順を実行してください。

```Bash
# Set the base repo URL for mainnet & retrieve peers
echo "export PEERS=\"fa38d2a851de43d34d9602956cd907eb3942ae89@a.ununifi.cauchye.net:26656,404ea79bd31b1734caacced7a057d78ae5b60348@b.ununifi.cauchye.net:26656,1357ac5cd92b215b05253b25d78cf485dd899d55@[2600:1f1c:534:8f02:7bf:6b31:3702:2265]:26656,25006d6b85daeac2234bcb94dafaa73861b43ee3@[2600:1f1c:534:8f02:a407:b1c6:e8f5:94b]:26656,caf792ed396dd7e737574a030ae8eabe19ecdf5c@[2600:1f1c:534:8f02:b0a4:dbf6:e50b:d64e]:26656,796c62bb2af411c140cf24ddc409dff76d9d61cf@[2600:1f1c:534:8f02:ca0e:14e9:8e60:989e]:26656,cea8d05b6e01188cf6481c55b7d1bc2f31de0eed@[2600:1f1c:534:8f02:ba43:1f69:e23a:df6b]:26656\"" >> ~/.bash_profile
source .bash_profile
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$PEERS\"/" ~/.gluon/config/config.toml
```

### Set minimum gas prices（最低ガス価格を設定する）

RPC ノードおよびバリデータノードについて、以下の最低ガス価格の設定を推奨します。私たちはパーミッションレスの WASM チェーンであるため、この設定はコントラクトスパムや潜在的な WASM コントラクトの攻撃ベクターから保護するのに役立ちます。

`$HOME/.gluon/config/app.toml` にて、最低ガス価格を設定してください：

```Bash
sed -i.bak -e "s/^minimum-gas-prices *=.*/minimum-gas-prices = \"0.0025uglu\"/" $HOME/.gluon/config/app.toml
```

### Option: Additional settings（追加設定）

必要に応じて、`~/.gluon/config/app.toml`の設定ファイルを編集してください。

- `enable`は、API サーバーを有効にするかどうかを定義します。

```bash
sed -i '/\[api\]/,+3 s/enable = false/enable = true/' ~/.gluon/config/app.toml;
```

- `EnableUnsafeCORS` は、CORS を有効にするかどうかを定義します（安全ではないため、使用は自己責任で行ってください）。

```bash
sed -i 's/enabled-unsafe-cors = false/enabled-unsafe-cors = true/' ~/.gluon/config/app.toml;
```

#### Accessing historical state（過去のステートへのアクセス）

過去のステートを照会したい場合、たとえば、過去の特定のブロック高でのウォレットの残高を知りたい場合は、`app.toml` で `pruning = "nothing"` に設定したアーカイブノードを実行する必要があります。この設定はリソースを多く消費し、かなりのストレージが必要になることに注意してください。

```toml
pruning = "nothing"
```

ストレージの要件を節約したい場合は、`app.toml` で `pruning = "everything"` を設定して、すべてをプルーニングすることを検討してください。

```toml
pruning = "everything"
```

### Create (or restore) a local key pair（ローカルキーペアを作成する）

Either create a new key pair or restore an existing wallet for your validator:

```Bash
# Create new keypair
gluond keys add <your-key>
# Restore existing gluon wallet with mnemonic seed phrase.
# You will be prompted to enter mnemonic seed.
gluond keys add <your-key> --recover
# Query the keystore for your public address
gluond keys show <your-key> -a
```

### Get some GLU tokens（GLU トークンを取得する）

バリデーターとの結合には GLU トークンが必要です。アクティブセットに入るには、十分なトークンが必要です。

### Start the consensus node（コンセンサスノードの起動）

Cosmovisor の設定手順に従い、ノードを起動してください。

{% hint style='tip' %}
Cosmovisor の使用は完全に任意です。Cosmovisor を使用しない場合は、バリデータがダウンタイムに陥ったり、ジャイルされたりしないように、ネットワークのアップグレードに必ず対応する必要があります
{% endhint %}

Cosmovisor を使用しない場合は、次のコマンドを実行してください。

```bash
gluond start
```

### Syncing the node（ノードの同期）

`gluond` デーモンを起動すると、チェーンがネットワークと同期し始めます。ネットワークとの同期時間は、環境やブロックチェーンの現在のサイズによって異なりますが、非常に長い時間がかかる可能性があります。ノードのステータスを照会するには、次のコマンドを実行してください。

```Bash
# Query via the RPC (default port: 26657)
curl http://localhost:26657/status | jq .result.sync_info.catching_up
```

このコマンドが `true` を返す場合、ノードはまだ同期中であることを意味します。それ以外の場合、ノードはネットワークの最新ブロックに追いついており、バリデータノードへのアップグレードを安全に進めることができます。

最新のブロックに追いつく時間を短縮したい場合は、他のノードからスナップショットを使用することを検討してください。

- [NodeStake](https://nodestake.top/ununifi)
- [NodeJumper](https://app.nodejumper.io/ununifi/sync)
- [Nodeist](https://nodeist.net/Ununifi/)
- [genznodes](https://genznodes.dev/services/)

ブロック高 0 から追いつきたい場合、各アップグレードのブロック高で `gluond` をアップグレードする必要があります。
