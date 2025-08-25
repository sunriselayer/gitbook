# ノードのビルド

## チェーンのアップグレード

チェーンのアップグレードを効率化し、ダウンタイムを最小限に抑えるために、ノードを管理するために[cosmovisor](https://docs.cosmos.network/master/run-node/cosmovisor.html)を設定することをお勧めします。

## バックアップ

Cosmovisorの最近のバージョンを使用している場合、デフォルト設定ではアップグレードが適用される前に状態のバックアップが作成されます。これは[環境フラグ](https://docs.cosmos.network/master/run-node/cosmovisor.html#command-line-arguments-and-environment-variables)を使用してオフにすることができます。

## アラートと監視

アラートと監視も望ましいです。解決策を検討し、自分の設定に合ったものを見つけることをお勧めします。Prometheusはすぐに利用でき、さまざまなオープンソースツールがあります。推奨される読み物：

## DDOS攻撃の回避

> サーバーの運用に慣れている場合は、DDOS攻撃から保護するために[セントリーノードアーキテクチャ](https://docs.tendermint.com/master/nodes/validators.html)のバリデータを構築することをお勧めします。

現在のメインネットノードを実行するためのベストプラクティスは、セントリーノードアーキテクチャです。[こちら](https://medium.com/@kidinamoto/tech-choices-for-cosmos-validators-27c7242061ea)で詳しく説明されているように、さまざまなアプローチがあります。一部のバリデータは、Dockerまたは他の仮想化ツールを使用して、単一のボックス上の仮想パーティションに3つのノードすべてを同じ場所に配置することを提唱しています。ただし、疑問がある場合は、各ノードを別のサーバーで実行してください。

[こちら](https://hub.cosmos.network/main/hub-tutorials/join-mainnet.html#pruning-of-state)で概説されているように、セントリーでプルーニングを有効にできることに注意してください。バリデータノード自体でプルーニングを無効にすることが望ましいですが、必須ではありません。

## ストレージの管理

> クラウドサービスプロバイダーを使用している場合は、後でデータをより大きなストレージデバイスに移動する必要がある場合があるため、`$HOME`を外部マウント可能なストレージボリュームにマウントすることをお勧めします。ほとんどのコマンドでホームディレクトリを指定するか、シンボリックリンクを使用できます。

ディスク容量がいっぱいになる可能性が高いため、ストレージを管理する計画を立てることが重要です。

セントリーノードを実行している場合：

- フルノード用の1TBのストレージは、多くの余裕を与えます
- プルーニングを行うセントリーごとに200GBで十分なはずです

バックアップの管理はこのドキュメントの範囲外ですが、いくつかのバリデータが公開スナップショットとバックアップを保持しています。

現在、wasmチェーンでは状態同期は機能していませんが、まもなく機能することが期待されています。

## ネットワークへの参加

ネットワークジェネシス後にUnUniFiメインネットに参加するための一般的な手順。

### シェル変数の設定

このガイドでは、シェル変数を使用します。これにより、クライアントコマンドをそのまま使用できるようになります。シェルコマンドは現在のシェルセッションに対してのみ有効であり、シェルセッションが閉じられると、シェル変数を再定義する必要があることを覚えておくことが重要です。

変数を複数のセッションで永続化させたい場合は、Go環境変数で行ったように、シェルの`.bash_profile`で明示的に設定してください。

変数のバインドをクリアするには、`unset $VARIABLE_NAME`を使用します。シェル変数はすべて大文字で名前を付ける必要があります。

### 必要なメインネットのchain-idを選択する

現在のUnUniFiネットワークの`chain-id`は`ununifi-beta-v1`です。`CHAIN_ID`を設定します。

メインネットの場合：

```bash
CHAIN_ID=ununifi-beta-v1
```

テストネットの場合：

```bash
CHAIN_ID=ununifi-test-v1
```

### サーバー名を設定する

`moniker`を選択します。これはノードの名前です。`MONIKER`を設定します。

```bash
MONIKER=<moniker>
# 例
MONIKER="yu-kimura-server-1"
```

## ノードの設定

これらの手順では、ノードを初期化し、ネットワークに同期し、ノードをバリデータにアップグレードする方法を説明します。

### チェーンの初期化

```bash
ununifid init "$MONIKER" --chain-id $CHAIN_ID
```

これにより、`~/.ununifi/config/`に次のファイルが生成されます。

- `genesis.json`
- `node_key.json`
- `priv_validator_key.json`

### ジェネシスファイルのダウンロード

メインネットの場合：

```bash
rm ~/.ununifi/config/genesis.json
curl -L https://raw.githubusercontent.com/UnUniFi/network/main/launch/ununifi-beta-v1/genesis.json -o ~/.ununifi/config/genesis.json
```

テストネットの場合：

```bash
rm ~/.ununifi/config/genesis.json
curl -L https://raw.githubusercontent.com/UnUniFi/network/main/launch/ununifi-test-v1/genesis.json -o ~/.ununifi/config/genesis.json
```

これにより、`ununifid init`コマンドで作成されたジェネシスファイル`genesis.json`が置き換えられます。

### 永続ピアの設定

永続ピアは、ノードが他のノードに接続してネットワークに参加する場所をノードに指示するために必要です。選択した`chain-id`のピアを取得するには：

メインネットの場合：

```bash
# メインネットのベースリポジトリURLを設定し、ピアを取得します
echo "export PEERS=\"fa38d2a851de43d34d9602956cd907eb3942ae89@a.ununifi.cauchye.net:26656,404ea79bd31b1734caacced7a057d78ae5b60348@b.ununifi.cauchye.net:26656,1357ac5cd92b215b05253b25d78cf485dd899d55@[2600:1f1c:534:8f02:7bf:6b31:3702:2265]:26656,25006d6b85daeac2234bcb94dafaa73861b43ee3@[2600:1f1c:534:8f02:a407:b1c6:e8f5:94b]:26656,caf792ed396dd7e737574a030ae8eabe19ecdf5c@[2600:1f1c:534:8f02:b0a4:dbf6:e50b:d64e]:26656,796c62bb2af411c140cf24ddc409dff76d9d61cf@[2600:1f1c:534:8f02:ca0e:14e9:8e60:989e]:26656,cea8d05b6e01188cf6481c55b7d1bc2f31de0eed@[2600:1f1c:534:8f02:ba43:1f69:e23a:df6b]:26656\"" >> ~/.bash_profile
source .bash_profile
```

テストネットの場合：

```bash
# メインネットのベースリポジトリURLを設定し、ピアを取得します
echo "export PEERS=\"65710949120e28f8af12f81b75efd2a509280f70@a.ununifi-test-v1.cauchye.net:26656,b20e3aad6b1bf7dc2d1635c388f578f335b13466@b.ununifi-test-v1.cauchye.net:26656,a8d5662130dd127dfcf82314e7a5b379a95d9daf@c.ununifi-test-v1.cauchye.net:26656,59361cdca33b1abbf85b46adb62bb680c6d59768@d.ununifi-test-v1.cauchye.net:26656\"" >> ~/.bash_profile
source .bash_profile
```

上記のピア変数を使用して、`~/.ununifi/config/config.toml`で`persistent_peers`を設定できます。

```bash
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$PEERS\"/" ~/.ununifi/config/config.toml
```

### 最低ガス価格の設定

RPCノードとバリデータノードには、次の`minimum-gas-prices`を設定することをお勧めします。私たちはパーミッションレスのwasmチェーンであるため、この設定は契約スパムや潜在的なwasm契約の攻撃ベクトルから保護するのに役立ちます。

`$HOME/.ununifi/config/app.toml`で、最低ガス価格を設定します。

```Bash
sed -i.bak -e "s/^minimum-gas-prices *=.*/minimum-gas-prices = \"0.0025uguu\"/" $HOME/.ununifi/config/app.toml
```

### 追加設定

必要に応じて、設定ファイル`~/.ununifi/config/app.toml`を編集します。

- `pruning`
- APIサーバーを有効にするかどうかを定義します。`enable = true`
- CORSを有効にするかどうかを定義します（安全でないため、自己責任で使用してください）。`enabled-unsafe-cors = true`

### ローカルキーペアの作成（または復元）

バリデータ用に新しいキーペアを作成するか、既存のウォレットを復元します。

```Bash
# 新しいキーペアを作成する
ununifid keys add <your-key>
# ニーモニックシードフレーズで既存のununifiウォレットを復元する
# ニーモニックシードの入力を求められます
ununifid keys add <your-key> --recover
# キーストアで公開アドレスを照会する
ununifid keys show <your-key> -a
```

`<your-key>`を任意のキー名に置き換えます。

### UnUniFiトークンを入手する

バリデータにボンドするために、いくつかのUnUniFiトークンが必要になります。アクティブセットに入るには、十分なトークンが必要です。

### cosmovisorのセットアップとノードの起動

指示に従ってcosmovisorをセットアップし、ノードを起動します。

> cosmovisorの使用は完全にオプションです。cosmovisorを使用しないことを選択した場合は、バリデータがダウンタイムを経験してジェイルされないように、ネットワークのアップグレードに必ず参加する必要があります。

Cosmovisorを使用しない場合は、ノードを起動できます：`ununifid start`

### ノードの同期

`ununifid`デーモンを起動した後、チェーンはネットワークへの同期を開始します。ネットワークへの同期にかかる時間は、設定とブロックチェーンの現在のサイズによって異なりますが、非常に長い時間がかかる場合があります。ノードのステータスを照会するには：

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

高さ0から追いつきたい場合は、アップグレードの高さごとに`ununifid`をアップグレードする必要があります。[mainnet-upgrades](mainnet-upgrades.md)を参照してください。
