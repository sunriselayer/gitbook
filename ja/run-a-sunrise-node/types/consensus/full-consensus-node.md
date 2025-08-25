# フルコンセンサスノード

フルコンセンサスノードを使用すると、Sunriseコンセンサスレイヤーでブロックチェーンの履歴を同期できます。

## チェーンのアップグレード

チェーンのアップグレードを効率化し、ダウンタイムを最小限に抑えるために、[Cosmovisor](https://docs.cosmos.network/main/build/tooling/cosmovisor)を設定してノードを管理することをお勧めします。

[Cosmovisorチュートリアル](setup-cosmovisor.md)に従ってください。

オンチェーンアップグレードを自動化するには、次のオプションを設定します。

```yml
DAEMON_ALLOW_DOWNLOAD_BINARIES=true
```

## バックアップ

最近のバージョンのCosmovisorを使用している場合、デフォルトの設定では、アップグレードを適用する前に状態のバックアップが作成されます。これは[環境フラグ](https://docs.cosmos.network/main/build/tooling/cosmovisor#command-line-arguments-and-environment-variables)を使用してオフにすることができます。

## アラートと監視

アラートと監視も望ましいため、ソリューションを検討し、自分の設定に合ったものを見つけることをお勧めします。Prometheusは標準で利用可能で、さまざまなオープンソースツールがあります。

## ハードウェア要件

バリデーターノードを実行するために、以下の最低ハードウェア要件が推奨されます。

- メモリ：8 GB RAM（最小）
- CPU：4コア
- ディスク：250 GB SSDストレージ
- 帯域幅：ダウンロード1 Gbps / アップロード1 Gbps

プルーニングを使用しない場合は、アーカイブノードを実行しており、500 GBのSSDストレージを推奨します。

## 依存関係

チュートリアルはUbuntu 22.04（LTS）で行われています。[環境チュートリアル](../../resources/environment.md)に従ってください。

## フルコンセンサスノードの実行

### インストール

[Go](https://go.dev/doc/install) 1.24.2をインストールします。

```bash
git clone https://github.com/sunriselayer/sunrise.git
cd sunrise
git checkout $TAG
make install
```

{% hint style="info" %}
ジェネシスから同期する場合は、ジェネシス時点のバイナリバージョンを使用してください。
スナップショットを使用している場合は、スナップショットの高さを確認し、その高さのバイナリを使用する必要があります。

詳細は[アップグレードドキュメント](../../resources/upgrade.md)を参照してください。
{% endhint %}

### 初期化

`chain-id`と`moniker`を設定します。`moniker`はノードの名前です。

```bash
CHAIN_ID=sunrise-1 // mainnet
MONIKER="node-name"
sunrised init "$MONIKER" --chain-id $CHAIN_ID
```

これにより、`~/.sunrise/config/`に以下のファイルが生成されます。

- `genesis.json`
- `node_key.json`
- `priv_validator_key.json`

## ジェネシスファイルのダウンロード

[Github](https://github.com/sunriselayer/network)で現在実行中のネットワークの`genesis.json`を確認してください。

例：メインネットの場合：

```bash
rm ~/.sunrise/config/genesis.json
curl -L https://raw.githubusercontent.com/sunriselayer/network/main/sunrise-1/genesis.json -o ~/.sunrise/config/genesis.json
```

### 最低ガス価格の設定

RPCノードおよびバリデーターノードについて、以下の最低ガス価格の設定を推奨します。私たちはパーミッションレスのWasmチェーンであるため、この設定はコントラクトスパムや潜在的なWasmコントラクトの攻撃ベクターから保護するのに役立ちます。

`$HOME/.sunrise/config/app.toml`で、最低ガス価格を設定してください。

```Bash
sed -i.bak -e "s/^minimum-gas-prices *=.*/minimum-gas-prices = \"0.025uusdrise\"/" $HOME/.sunrise/config/app.toml
```

{% hint style="warning" %}
ガス価格を高く設定しすぎないでください。バリデーターの場合、提案したブロックにトランザクションが含まれなくなります。これにより、ネットワーク全体が処理できるトランザクションの数が減少します。
{% endhint %}

### オプション：シードと永続的ピアの設定

- シード

「シード」は、新しく参加するバリデーターが最初に接続すべき他のバリデーターのリストを提供します。
バリデーターがネットワークに接続すると、主に`persistent_peers`に接続を依存するため、`seeds`の重要性は低下します。

```bash
SEEDS=$(curl -sL https://raw.githubusercontent.com/sunriselayer/network/main/sunrise-1/seeds.txt | tr '\n' ',')
echo $SEEDS
sed -i.bak -e "s/^seeds *=.*/seeds = \"$SEEDS\"/" $HOME/.sunrise/config/config.toml
```

- 永続的ピア

「永続的ピア」は、バリデーターが常に接続を維持すべき信頼できるバリデーターのリストです。
`persistent_peers`にリストされているバリデーターへの接続は、ネットワークの安定性を維持するために優先されます。

```bash
PERSISTENT_PEERS=$(curl -sL https://raw.githubusercontent.com/sunriselayer/network/main/sunrise-1/peers.txt | tr '\n' ',')
echo $PERSISTENT_PEERS
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$PERSISTENT_PEERS\"/" $HOME/.sunrise/config/config.toml
```

### オプション：追加設定

必要に応じて、`$HOME/.sunrise/config/app.toml`の設定ファイルを編集してください。

- `enable`は、APIサーバーを有効にするかどうかを定義します。

```bash
sed -i '/\[api\]/,+3 s/enable = false/enable = true/' $HOME/.sunrise/config/app.toml;
```

- `EnableUnsafeCORS`は、CORSを有効にするかどうかを定義します（安全ではないため、自己責任で使用してください）。

```bash
sed -i 's/enabled-unsafe-cors = false/enabled-unsafe-cors = true/' $HOME/.sunrise/config/app.toml;
```

- デフォルトでは、RPCとRESTは公開されていないため、公開ノードにしたい場合は、次のように設定してください。

```bash
sed -i 's/address = "localhost:9090"/address = "0.0.0.0:9090"/' $HOME/.sunrise/config/app.toml;
sed -i 's#address = "tcp://localhost:1317"#address = "tcp://0.0.0.0:1317"#' $HOME/.sunrise/config/app.toml;
sed -i 's#laddr = "tcp://127.0.0.1:26657"#laddr = "tcp://0.0.0.0:26657"#' $HOME/.sunrise/config/config.toml;
```

### ストレージとプルーニングの設定

コンセンサスノードをsunrise-nodeブリッジノードに接続する場合は、トランザクションインデックスを有効にし、すべてのブロックデータを保持する必要があります。これは、`config.toml`で次の設定を行うことで実現できます。

#### トランザクションインデックスの有効化

```toml
indexer = "kv"
```

#### すべてのブロックデータの保持

そして、`app.toml`では、`min-retain-blocks`はデフォルト設定のままである必要があります。

```toml
min-retain-blocks = 0
```

#### 過去のステートへのアクセス

過去の特定の高さでのウォレットの残高などを照会したい場合は、`app.toml`で`pruning = "nothing"`に設定したアーカイブノードを実行する必要があります。この設定はリソースを多く消費し、かなりのストレージが必要になることに注意してください。

```toml
pruning = "nothing"
```

ストレージの要件を節約したい場合は、`app.toml`で`pruning = "everything"`を使用してすべてをプルーニングすることを検討してください。

```toml
pruning = "everything"
```

### ローカルキーペアを作成（または復元）する

バリデーター用に新しいキーペアを作成するか、既存のウォレットを復元します。

```Bash
# 新しいキーペアを作成
sunrised keys add <your-key>
# ニーモニックシードフレーズで既存のsunriseウォレットを復元します。
# ニーモニックシードを入力するように求められます。
sunrised keys add <your-key> --recover
# キーストアで公開アドレスをクエリします
sunrised keys show <your-key> -a
```

`<your-key>`を任意のキー名に置き換えてください。

### RISEトークンを取得する

バリデーターにボンドするためにいくつかのvRISEトークンが必要になります（手数料のためにいくつかのRISEトークンも必要です）。アクティブセットに入るには、十分なトークンが必要です。

### コンセンサスノードの起動

Cosmovisorを設定し、ノードを起動するための手順に従ってください。
[Cosmovisorチュートリアル](setup-cosmovisor.md)を参照してください。

{% hint style="info" %}
Cosmovisorの使用は完全に任意です。Cosmovisorを使用しない場合は、バリデーターがダウンタイムに陥ったり、ジェイルされたりしないように、ネットワークのアップグレードに必ず対応する必要があります。
{% endhint %}

Cosmovisorを使用しない場合は、次のコマンドを実行してください。

```bash
sunrised start
```

### ノードの同期

`sunrised`デーモンを起動すると、チェーンがネットワークと同期し始めます。ネットワークとの同期時間は、設定やブロックチェーンの現在のサイズによって異なりますが、非常に長い時間がかかる可能性があります。ノードのステータスを照会するには、次のようにします。

```Bash
# RPC経由でクエリ（デフォルトポート：26657）
curl http://localhost:26657/status | jq .result.sync_info.catching_up
```

このコマンドが`true`を返す場合、ノードはまだ同期中であることを意味します。それ以外の場合、ノードはネットワークの最新ブロックに追いついており、バリデーターノードへのアップグレードを安全に進めることができます。

最新のブロックに追いつく時間を短縮したい場合は、他のノードのスナップショットを使用することを検討してください。

### オプション：スナップショットを使用する

最新のブロックに追いつく時間を短縮したい場合は、スナップショットの使用を検討してください。スナップショットを使用すると、特定の高さからノードをブートストラップできるため、ジェネシスから同期する必要がなくなります。

パートナーの[Polkachu](https://www.polkachu.com/tendermint_snapshots/sunrise)は、Sunriseネットワークの毎日のスナップショットを提供しています。最新のスナップショットURLを取得するには、彼らのWebサイトにアクセスしてください。
