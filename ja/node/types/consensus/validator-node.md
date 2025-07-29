# バリデータノード

バリデータノードを使用すると、Sunriseネットワークのコンセンサスに参加することができます。

## ハードウェア要件

バリデータノードを実行するために推奨される最小限のハードウェア要件は以下の通りです：

- メモリ：8 GB RAM（最小）
- CPU：6コア
- ディスク：500 GB SSDストレージ
- 帯域幅：ダウンロード1 Gbps / アップロード1 Gbps

## ノードの実行

まず、[フルコンセンサスノードの設定手順](full-consensus-node.md)に従ってください。

### オプション: 作業ディレクトリのリセット

過去に`sunrised`の作業ディレクトリをすでに初期化している場合、新しいディレクトリを再初期化する前にクリーンアップする必要があります。以下のコマンドを実行することでクリーンアップができます。

```bash
sunrised tendermint unsafe-reset-all
```

### 作業ディレクトリの初期化

次のコマンドを実行してください。

```bash
CHAIN_ID=sunrise-1 # メインネットの場合
MONIKER="validator-name"
sunrised init "$MONIKER" --chain-id $CHAIN_ID
```

現在のchain-idを知るには、[私たちのGithub](https://github.com/sunriselayer/network)を確認してください。

### 新しいキーの作成

```bash
VALIDATOR_WALLET="validator"
sunrised keys add $VALIDATOR_WALLET --keyring-backend test
```

### バリデータ公開鍵

バリデータを初期化する前に最後に必要なのは、最初にノードを初期化したときに作成されたバリデータ公開鍵を取得することです。バリデータ公開鍵を取得するには：

```bash
sunrised tendermint show-validator
{"@type":"/cosmos.crypto.ed25519.PubKey","key":"ZQweivhEkT/akg5RT6RWkElt43rr5cf+qu/QQ5jOpmQ="}
```

### バリデータの作成

バリデータを作成するには、最低1 vRISEが必要です。vRISEは譲渡不可能なため、アカウントに残高がない場合は、流動性プールにポジションを作成してvRISEを獲得してください。

まず、バリデータ設定ファイル[~/.sunrise/config/validator.json]を作成します。

```json
{
  "pubkey": {"@type":"/cosmos.crypto.ed25519.PubKey","key":"ZQweivhEkT/akg5RT6RWkElt43rr5cf+qu/QQ5jOpmQ="},
  "amount": "1000000uvrise",
  "moniker": "your_validator's_name",
  "identity": "optional identity signature (ex. UPort or Keybase)",
  "website": "validator's (optional) website",
  "security": "validator's (optional) security contact email",
  "details": "validator's (optional) details",
  "commission-rate": "0.1",
  "commission-max-rate": "0.2",
  "commission-max-change-rate": "0.01",
  "min-self-delegation": "1"
}
```

次に、以下のコマンドを実行します

```bash
sunrised tx staking create-validator [path/to/validator.json] \
    --chain-id=$CHAIN_ID \
    --from=$VALIDATOR_WALLET \
    --keyring-backend=test \
    --fees=10000uusdrise \
    --gas=auto
```

## バックアップ

何らかの理由でバリデータが損傷したり失われたりした場合に復元できるよう、特定のファイルをバックアップする必要があります。`~/.sunrise/config/`にある以下のファイルを安全にバックアップしてください。

- `priv_validator_key.json`
- `node_key.json`

これらのファイルのバックアップは暗号化することをお勧めします。

## バリデータへの追加のインセンティブ

コアチームは、以下のサービスを提供するバリデータに対してRISEをデリゲートします。

- IBCリレーヤー
  - `100000000microRISE` delegation per channel
- ノードスナップショット
  - `10000000000microRISE` delegation
- REST APIエンドポイント
  - `10000000000microRISE` delegation