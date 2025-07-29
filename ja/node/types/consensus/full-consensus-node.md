# フルコンセンサスノード

フルコンセンサスノードを使用すると、Sunriseのコンセンサスレイヤーでブロックチェーンの履歴を同期することができます。

## チェーンアップグレード

チェーンのアップグレードを効率化し、ダウンタイムを最小限に抑えるために、ノードの管理に[Cosmovisor](https://docs.cosmos.network/main/build/tooling/cosmovisor)を設定することをお勧めします。

[Cosmovisorチュートリアル](setup-cosmovisor.md)に従ってください。

オンチェーンアップグレードを自動化するには、以下のオプションを設定します。

```yml
DAEMON_ALLOW_DOWNLOAD_BINARIES=true
```

## バックアップ

新しいバージョンのCosmovisorを使用している場合、デフォルトの設定ではアップグレードが適用される前にステートのバックアップが作成されます。この機能は[環境フラグ](https://docs.cosmos.network/main/build/tooling/cosmovisor#command-line-arguments-and-environment-variables)を使用してオフにすることができます。

## アラートとモニタリング

アラートとモニタリングも望ましいでしょう - あなたの環境に適したソリューションを探索し、見つけることをお勧めします。Prometheusはすぐに利用可能であり、さまざまなオープンソースツールが存在します。

## ハードウェア要件

バリデータノードを実行するために推奨される最小限のハードウェア要件は以下の通りです。

*   メモリ：8 GB RAM（最小）
*   CPU：4コア
*   ディスク：250 GB SSDストレージ
*   帯域幅：ダウンロード1 Gbps / アップロード1 Gbps

プルーニングを使用していない場合はアーカイブノードを運用していることになり、500 GBのSSDストレージを用意することが推奨されます。

## 依存関係

このチュートリアルはUbuntu 22.04（LTS）で実行されます。[環境構築](../../resources/environment.md)のチュートリアルに従ってください。

## フルコンセンサスノードの実行

### インストール

[Go 1.22をインストール](https://go.dev/doc/install)

```bash
git clone https://github.com/sunriselayer/sunrise.git
cd sunrise
git checkout $TAG
make install
```

{% hint style="info" %}
ジェネシスから同期する場合は、ジェネシス時点のバイナリバージョンを使用してください。
スナップショットを使用している場合は、スナップショットの高さを確認し、その高さのバイナリを使用する必要があります。

詳細は[アップグレードドキュメント](../../resources/upgrade.md)をご覧ください。
{% endhint %}

### 初期化

`chain-id`と`moniker`を設定します。`moniker`はノードの名前です。

```bash
CHAIN_ID=sunrise-1 // mainnet
MONIKER="node-name"
sunrised init "$MONIKER" --chain-id $CHAIN_ID
```

これにより、`~/.sunrise/config/`に以下のファイルが生成されます。

*   `genesis.json`
*   `node_key.json`
*   `priv_validator_key.json`

## ジェネシスファイルをダウンロードする

現在実行中のネットワークの`genesis.json`を[私たちのGithub](https://github.com/sunriselayer/network)で確認してください。

例：メインネットの場合：

```bash
rm ~/.sunrise/config/genesis.json
curl -L https://raw.githubusercontent.com/sunriselayer/network/main/sunrise-1/genesis.json -o ~/.sunrise/config/genesis.json
```

### 最小ガス価格の設定

RPCノードとバリデータノードについては、以下の最小ガス価格（minimum-gas-prices）を設定することをお勧めします。私たちはパーミッションレスなWasmチェーンであるため、この設定はコントラクトのスパムや潜在的なWasmコントラクト攻撃ベクトルからの保護に役立ちます。

`$HOME/.sunrise/config/app.toml`で最小ガス価格を設定します。

```Bash
sed -i.bak -e "s/^minimum-gas-prices *=.*/minimum-gas-prices = \"0.0025urise\"/" $HOME/.sunrise/config/app.toml
```

{% hint style="warning" %}
ガス価格を高く設定しすぎないでください。バリデーターの場合、提案したブロックにトランザクションが含まれなくなります。これにより、ネットワーク全体が処理できるトランザクションの数が減少します。
{% endhint %}

### オプション: シードと永続的なピアを設定する

- シード

「シード」は、新しく参加するバリデーターが最初に接続すべき他のバリデーターのリストを提供します。
バリデーターがネットワークに接続すると、主に`persistent_peers`に依存して接続するため、`seeds`の重要性は低下します。

```bash
SEEDS=$(curl -sL https://raw.githubusercontent.com/sunriselayer/network/main/sunrise-1/seeds.txt | tr '\n' ',')
echo $SEEDS
sed -i.bak -e "s/^seeds *=.*/seeds = \"$SEEDS\"/" $HOME/.sunrise/config/config.toml
```

- 永続的なピア

「永続的なピア」は、バリデーターが常に接続を維持すべき信頼できるバリデーターのリストです。
`persistent_peers`にリストされているバリデーターへの接続は、ネットワークの安定性を維持するために優先されます。

```bash
PERSISTENT_PEERS=$(curl -sL https://raw.githubusercontent.com/sunriselayer/network/main/sunrise-1/peers.txt | tr '\n' ',')
echo $PERSISTENT_PEERS
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$PERSISTENT_PEERS\"/" $HOME/.sunrise/config/config.toml
```

### オプション: 追加の設定

必要に応じて、設定ファイル`$HOME/.sunrise/config/app.toml`を編集してください。

*   Enableは、APIサーバーを有効にするかどうかを定義します。

```bash
sed -i '/\[api\]/,+3 s/enable = false/enable = true/' $HOME/.sunrise/config/app.toml;
```

*   EnableUnsafeCORSは、CORSを有効にするかどうかを定義します（安全ではありません - 自己責任で使用してください）。

```bash
sed -i 's/enabled-unsafe-cors = false/enabled-unsafe-cors = true/' $HOME/.sunrise/config/app.toml;
```

*   デフォルトでは、RPCとRESTは公開されていないため、公開ノードにしたい場合は、次のように設定します。

```bash
sed -i 's/address = "localhost:9090"/address = "0.0.0.0:9090"/' $HOME/.sunrise/config/app.toml;
sed -i 's#address = "tcp://localhost:1317"#address = "tcp://0.0.0.0:1317"#' $HOME/.sunrise/config/app.toml;
sed -i 's#laddr = "tcp://127.0.0.1:26657"#laddr = "tcp://0.0.0.0:26657"#' $HOME/.sunrise/config/config.toml;
```

### ストレージとプルーニングの設定

コンセンサスノードがsunrise-nodeブリッジノードに接続されている場合、トランザクションのインデックス作成を有効にし、すべてのブロックデータを保持する必要があります。これは`config.toml`で以下の設定を行うことで実現できます。

#### トランザクションのインデックス化を有効にする

```toml
indexer = "kv"
```

#### すべてのブロックデータを保持する

そして、`app.toml`では、`min-retain-blocks`をデフォルト設定のままにしておく必要があります。

```toml
min-retain-blocks = 0
```

#### 過去のステートへのアクセス

過去のステートを照会したい場合 — 例えば、過去の特定のブロック高におけるウォレットの残高を知りたい場合など — `app.toml`で`pruning = "nothing"`を設定して、アーカイブノードを実行する必要があります。ただし、この設定はリソースを多く消費し、大量のストレージを必要とすることに注意してください。

```toml
pruning = "nothing"
```

ストレージの要件を節約したい場合は、app.tomlで`pruning = "everything"`を使用して、すべてをプルーニング（剪定）することを検討してください。

```toml
pruning = "everything"
```

### ローカルキーペアの作成（または復元）

バリデーター用に新しいキーペアを作成するか、既存のウォレットを復元します。

```Bash
# 新しいキーペアを作成
sunrised keys add <your-key>
# ニーモニックシードフレーズで既存のsunriseウォレットを復元
# ニーモニックシードの入力を求められます
sunrised keys add <your-key> --recover
# キーストアから公開アドレスを照会
sunrised keys show <your-key> -a
```

`<your-key>`を選んだキー名に置き換えてください。

### RISEトークンを取得する

バリデータと結合するには、vRISEトークン（および手数料のためのRISEトークン）が必要です。アクティブセットに入るには、十分なトークンが必要です。

### コンセンサスノードを起動する

Cosmovisorの設定とノードの起動については、以下の手順に従ってください。
[Cosmovisorチュートリアル](setup-cosmovisor.md)を参照してください。

{% hint style="info" %}
Cosmovisorの使用は完全に任意です。Cosmovisorを使用しないことを選択した場合、バリデータがダウンタイムを持たず、ジェイルされないようにするために、ネットワークのアップグレードに確実に対応する必要があります。
{% endhint %}

Cosmovisorを使用しない場合は、次のコマンドを実行してください。

```bash
sunrised start
```

### ノードの同期

`sunrised`デーモンを起動すると、チェーンはネットワークとの同期を開始します。ネットワークとの同期にかかる時間は、あなたの設定と現在のブロックチェーンのサイズによって異なりますが、非常に長い時間がかかる可能性があります。ノードのステータスを確認するには：

```Bash
# RPC経由でクエリ（デフォルトポート：26657）
curl http://localhost:26657/status | jq .result.sync_info.catching_up
```

このコマンドが`true`を返す場合、あなたのノードはまだ追いついている途中であることを意味します。そうでない場合、あなたのノードはネットワークの現在のブロックに追いついており、バリデータノードにアップグレードしても安全です。

最新のブロックに追いつくまでの時間を短縮したい場合は、他のノードからのスナップショットの使用を検討してください。

ブロック高0から追いつきたい場合は、各アップグレードのブロック高で`sunrised`をアップグレードする必要があります。
Cosmovisorが実行中で自動ダウンロードオプションが有効になっている場合、アップグレードも自動的に処理されます。