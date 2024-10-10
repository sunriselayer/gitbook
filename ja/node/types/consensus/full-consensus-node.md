# Full Consensus Node

フルコンセンサスノードを使用すると、Sunrise のコンセンサス層でブロックチェーンの履歴を同期することができます。

## チェーンアップグレード

チェーンのアップグレードを効率化し、ダウンタイムを最小限に抑えるために、ノードの管理に Cosmovisor を設定することをお勧めします。
Cosmovisor のチュートリアルに従ってください。
オンチェーンアップグレードを自動化するには、以下のオプションを設定します。

```yml
DAEMON_ALLOW_DOWNLOAD_BINARIES=true
```

## バックアップ

新しいバージョンの Cosmovisor を使用している場合、デフォルトの設定ではアップグレードが適用される前にステートのバックアップが作成されます。この機能は[環境フラグ](https://docs.cosmos.network/main/build/tooling/cosmovisor#command-line-arguments-and-environment-variables)を使用してオフにすることができます。

## アラートとモニタリング

アラートとモニタリングも望ましいでしょう - あなたの環境に適したソリューションを探索し、見つけることをお勧めします。Prometheus はすぐに利用可能であり、さまざまなオープンソースツールが存在します。

## ハードウェア要件

バリデータノードを実行するために推奨される最小限のハードウェア要件は以下の通りです。

- Memory: 8 GB RAM (最小)
- CPU: 4 cores
- Disk: 250 GB SSD Storage
- Bandwidth: 1 Gbps for Download/1 Gbps for Upload

プルーニングを使用していない場合はアーカイブノードを運用していることになり、500 GB の SSD ストレージを用意することが推奨されます。

## 依存関係

このチュートリアルは Ubuntu 22.04（LTS）で実行されます。[環境構築](../../resources/environment.md)のチュートリアルに従ってください。

## フルコンセンサスノードの実行

### インストール

[Install Go](https://go.dev/doc/install) 1.22

```bash
git clone https://github.com/SunriseLayer/sunrise.git
cd sunrise
git checkout $TAG
make install
```

### 初期化

`chain-id` と `moniker` を設定します。`moniker` はノードの名前です。

```bash
CHAIN_ID=sunrise-1
MONIKER="node-name"
sunrised init "$MONIKER" --chain-id $CHAIN_ID
```

これにより、`~/.sunrise/config/`に以下のファイルが生成されます。

- `genesis.json`
- `node_key.json`
- `priv_validator_key.json`

## ジェネシスファイルをダウンロードする

For mainnet:

```bash
rm ~/.sunrise/config/genesis.json
curl -L https://raw.githubusercontent.com/sunrise-layer/network/main/launch/sunrise-1/genesis.json -o ~/.sunrise/config/genesis.json
```

For testnet:

```bash
rm ~/.sunrise/config/genesis.json
curl -L https://raw.githubusercontent.com/sunrise-layer/network/main/launch/sunrise-test-1/genesis.json -o ~/.sunrise/config/genesis.json
```

## オプション: Persistent Peers（永続的なピア）を設定する

```bash
PERSISTENT_PEERS=$(curl -sL https://raw.githubusercontent.com/sunrise-layer/network/main/launch/sunrise-1/peers.txt | tr '\n' ',')
echo $PERSISTENT_PEERS
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$PERSISTENT_PEERS\"/" $HOME/.sunrise/config/config.toml
```

### 最小ガス価格の設定

RPC ノードとバリデータノードについては、以下の最小ガス価格（minimum-gas-prices）を設定することをお勧めします。私たちはパーミッションレスな Wasm チェーンであるため、この設定はコントラクトのスパムや潜在的な Wasm コントラクト攻撃ベクトルからの保護に役立ちます。

`$HOME/.sunrise/config/app.toml`で最小ガス価格を設定します。

```Bash
sed -i.bak -e "s/^minimum-gas-prices *=.*/minimum-gas-prices = \"0.0025urise\"/" $HOME/.sunrise/config/app.toml
```

### オプション: 追加の設定

必要に応じて、設定ファイル `~/.sunrise/config/app.toml` を編集してください。

- Enable は、API サーバーを有効にするかどうかを定義します。

```bash
sed -i '/\[api\]/,+3 s/enable = false/enable = true/' ~/.sunrise/config/app.toml;
```

- `EnableUnsafeCORS`は、CORS を有効にするかどうかを定義します（安全ではありません - 自己責任で使用してください）。

```bash
sed -i 's/enabled-unsafe-cors = false/enabled-unsafe-cors = true/' ~/.sunrise/config/app.toml;
```

### ストレージとプルーニングの設定

コンセンサスノードが sunrise-node ブリッジノードに接続されている場合、トランザクションのインデックス作成を有効にし、すべてのブロックデータを保持する必要があります。これは `config.toml` で以下の設定を行うことで実現できます。

#### トランザクションのインデックス化を有効にする

```toml
indexer = "kv"
```

#### すべてのブロックデータを保持する

そして、`app.toml` では、`min-retain-blocks` をデフォルト設定のままにしておく必要があります。

```toml
min-retain-blocks = 0
```

#### Historical State（過去のステート）へのアクセス

Historical State（過去のステート）を照会したい場合 — 例えば、過去の特定のブロック高におけるウォレットの残高を知りたい場合など — `app.toml` で `pruning = "nothing"` を設定して、アーカイブノードを実行する必要があります。ただし、この設定はリソースを多く消費し、大量のストレージを必要とすることに注意してください。

```toml
pruning = "nothing"
```

ストレージの要件を節約したい場合は、app.toml で `pruning = "everything"` を使用して、すべてをプルーニング（剪定）することを検討してください。

```toml
pruning = "everything"
```

### ローカルキーペアの作成（または復元）

バリデーター用に新しいキーペアを作成するか、既存のウォレットを復元します。

```Bash
# Create new keypair
sunrised keys add <your-key>
# Restore existing sunrise wallet with mnemonic seed phrase.
# You will be prompted to enter mnemonic seed.
sunrised keys add <your-key> --recover
# Query the keystore for your public address
sunrised keys show <your-key> -a
```

`<your-key>`  を選んだキー名に置き換えてください。

### RISE トークンを取得する

バリデータと結合するには、RISE トークンが必要です。アクティブセットに入るには、十分なトークンが必要です。

### コンセンサスノードを起動する

Cosmovisor の設定とノードの起動については、以下の手順に従ってください。

{% hint style="info" %}
Cosmovisor の使用は完全に任意です。Cosmovisor を使用しないことを選択した場合、バリデータがダウンタイムを持たず、ジェイルされないようにするために、ネットワークのアップグレードに確実に対応する必要があります。
{% endhint %}

Cosmovisor を使用しない場合は、次のコマンドを実行してください。

```bash
sunrised start
```

### ノードの同期

`sunrised` デーモンを起動すると、チェーンはネットワークとの同期を開始します。ネットワークとの同期にかかる時間は、あなたの設定と現在のブロックチェーンのサイズによって異なりますが、非常に長い時間がかかる可能性があります。ノードのステータスを確認するには：

```Bash
# Query via the RPC (default port: 26657)
curl http://localhost:26657/status | jq .result.sync_info.catching_up
```

このコマンドが `true` を返す場合、あなたのノードはまだ追いついている途中であることを意味します。そうでない場合、あなたのノードはネットワークの現在のブロックに追いついており、バリデータノードにアップグレードしても安全です。

最新のブロックに追いつくまでの時間を短縮したい場合は、他のノードからのスナップショットの使用を検討してください。

ブロック高 0 から追いつきたい場合は、各アップグレードのブロック高で `sunrised` をアップグレードする必要があります。
