# Gluonフルノード

フルノードは、ネットワークジェネシス後にGluonメインネットに参加するための一般的な手順です。

## チェーンのアップグレード

チェーンのアップグレードを効率化し、ダウンタイムを最小限に抑えるために、[Cosmovisor](https://docs.cosmos.network/main/build/tooling/cosmovisor)を使用してノードを管理することをお勧めします。

[Cosmovisorチュートリアル](../../node/types/consensus/setup-cosmovisor.md)に従ってください。

オンチェーンアップグレードを自動化するには、次のオプションを設定します。

```yml
DAEMON_ALLOW_DOWNLOAD_BINARIES=true
```

## バックアップ

Cosmovisorの最近のバージョンを使用している場合、デフォルト設定ではアップグレードが適用される前に状態のバックアップが作成されます。これは[環境フラグ](https://docs.cosmos.network/main/build/tooling/cosmovisor#command-line-arguments-and-environment-variables)を使用してオフにすることができます。

## アラートと監視

アラートと監視も望ましいです。解決策を検討し、自分の設定に合ったものを見つけることをお勧めします。Prometheusはすぐに利用でき、さまざまなオープンソースツールがあります。

## ハードウェア要件

バリデータノードを実行するために、以下の最低ハードウェア要件が推奨されます。

- メモリ：32 GB RAM（または同等のスワップファイル設定）
- CPU：8コア（4物理コア）x86_64
- ディスク：1 TB SSDストレージ（詳細は下記参照）
- 帯域幅：ダウンロード1 Gbps / アップロード1 Gbps

アーカイブノード（pruning = "nothing"）は、少なくとも64GBの専用メモリが必要です。

- アーカイブノード（pruning = "nothing"）は、月あたり約100 GBの割合で増加します。現在の合計ディスク使用量は6TBなので、より大きなディスクが必要になります。
- フルプルーニングノード（pruning = "everything"）は、月あたり約5 GBの割合で増加します。
- デフォルトのプルーニングノード（pruning = "default"）は、月あたり約25 GBの割合で増加します。

## 依存関係

このチュートリアルはUbuntu 22.04（LTS）で実行されます。
[環境チュートリアル](../../node/resources/environment.md)に従ってください。

## ノードの実行

### インストール

```bash
git clone https://github.com/UnUniFi/chain.git
cd chain
git checkout $TAG
make install
```

### 初期化

`chain-id`と`moniker`を設定します。`moniker`はノードの名前です。

```bash
CHAIN_ID=gluon-1
MONIKER="node-name"
gluond init "$MONIKER" --chain-id $CHAIN_ID
```

これにより、`~/.gluon/config/`に次のファイルが生成されます。

- `genesis.json`
- `node_key.json`
- `priv_validator_key.json`

## ジェネシスファイルのダウンロード

メインネットの場合：

```bash
rm ~/.gluon/config/genesis.json
curl -L https://raw.githubusercontent.com/UnUniFi/network/main/launch/ununifi-beta-v1/genesis.json -o ~/.gluon/config/genesis.json
```

テストネットの場合：

```bash
rm ~/.gluon/config/genesis.json
curl -L https://raw.githubusercontent.com/UnUniFi/network/main/launch/ununifi-test-v1/genesis.json -o ~/.gluon/config/genesis.json
```

## オプション：永続ピアの設定

永続ピアは、ノードが他のノードに接続してネットワークに参加する場所をノードに指示するために必要です。選択した`chain-id`のピアを取得するには：

```Bash
# メインネットのベースリポジトリURLを設定し、ピアを取得します
echo "export PEERS=\"fa38d2a851de43d34d9602956cd907eb3942ae89@a.ununifi.cauchye.net:26656,404ea79bd31b1734caacced7a057d78ae5b60348@b.ununifi.cauchye.net:26656,1357ac5cd92b215b05253b25d78cf485dd899d55@[2600:1f1c:534:8f02:7bf:6b31:3702:2265]:26656,25006d6b85daeac2234bcb94dafaa73861b43ee3@[2600:1f1c:534:8f02:a407:b1c6:e8f5:94b]:26656,caf792ed396dd7e737574a030ae8eabe19ecdf5c@[2600:1f1c:534:8f02:b0a4:dbf6:e50b:d64e]:26656,796c62bb2af411c140cf24ddc409dff76d9d61cf@[2600:1f1c:534:8f02:ca0e:14e9:8e60:989e]:26656,cea8d05b6e01188cf6481c55b7d1bc2f31de0eed@[2600:1f1c:534:8f02:ba43:1f69:e23a:df6b]:26656\"" >> ~/.bash_profile
source .bash_profile
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$PEERS\"/" ~/.gluon/config/config.toml
```

### 最低ガス価格の設定

RPCノードとバリデータノードには、次の`minimum-gas-prices`を設定することをお勧めします。私たちはパーミッションレスのwasmチェーンであるため、この設定は契約スパムや潜在的なwasm契約の攻撃ベクトルから保護するのに役立ちます。

`$HOME/.gluon/config/app.toml`で、最低ガス価格を設定します。

```Bash
sed -i.bak -e "s/^minimum-gas-prices *=.*/minimum-gas-prices = \"0.0025uglu\"/" $HOME/.gluon/config/app.toml
```

### オプション：追加設定

必要に応じて、設定ファイル`~/.gluon/config/app.toml`を編集します。

- APIサーバーを有効にするかどうかを定義します。

```bash
sed -i '/\[api\]/,+3 s/enable = false/enable = true/' ~/.gluon/config/app.toml;
```

- EnableUnsafeCORSは、CORSを有効にするかどうかを定義します（安全でないため、自己責任で使用してください）。

```bash
sed -i 's/enabled-unsafe-cors = false/enabled-unsafe-cors = true/' ~/.gluon/config/app.toml;
```

#### 履歴状態へのアクセス

履歴状態を照会したい場合（たとえば、過去の特定の高さでのウォレットの残高を知りたい場合）、`app.toml`で`pruning = "nothing"`を設定したアーカイブノードを実行する必要があります。この設定はリソースを大量に消費し、かなりのストレージが必要になることに注意してください。

```toml
pruning = "nothing"
```

ストレージ要件を節約したい場合は、`app.toml`で`pruning = "everything"`を使用してすべてをプルーニングすることを検討してください。

```toml
pruning = "everything"
```

### ローカルキーペアの作成（または復元）

バリデータ用に新しいキーペアを作成するか、既存のウォレットを復元します。

```Bash
# 新しいキーペアを作成する
gluond keys add <your-key>
# ニーモニックシードフレーズで既存のgluonウォレットを復元する
# ニーモニックシードの入力を求められます
gluond keys add <your-key> --recover
# キーストアで公開アドレスを照会する
gluond keys show <your-key> -a
```

### GLUトークンを入手する

バリデータにボンドするために、いくつかのGLUトークンが必要になります。アクティブセットに入るには、十分なトークンが必要です。

### コンセンサスノードの起動

指示に従ってCosmovisorをセットアップし、ノードを起動します。

{% hint style='tip' %}
cosmovisorの使用は完全にオプションです。cosmovisorを使用しないことを選択した場合は、バリデータがダウンタイムを経験してジェイルされないように、ネットワークのアップグレードに必ず参加する必要があります。
{% endhint %}

Cosmovisorを使用しない場合は、次を実行します。

```bash
gluond start
```

### ノードの同期

`gluond`デーモンを起動した後、チェーンはネットワークへの同期を開始します。ネットワークへの同期にかかる時間は、設定とブロックチェーンの現在のサイズによって異なりますが、非常に長い時間がかかる場合があります。ノードのステータスを照会するには：

```Bash
# RPC経由で照会する（デフォルトポート：26657）
curl http://localhost:26657/status | jq .result.sync_info.catching_up
```

このコマンドが`true`を返す場合、ノードはまだ追いついていないことを意味します。それ以外の場合、ノードはネットワークの現在のブロックに追いついており、バリデータノードへのアップグレードに進んでも安全です。

最新のブロックに追いつくまでの時間を短縮したい場合は、他のノードのスナップショットを使用することを検討してください。

- [NodeStake](https://nodestake.top/ununifi)
- [NodeJumper](https://app.nodejumper.io/ununifi/sync)
- [Nodeist](https://nodeist.net/Ununifi/)
- [genznodes](https://genznodes.dev/services/)

高さ0から追いつきたい場合は、アップグレードの高さごとに`gluond`をアップグレードする必要があります。
