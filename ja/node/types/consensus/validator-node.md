# バリデーターノード

バリデーターノードを使用すると、Sunriseネットワークのコンセンサスに参加できます。

## ハードウェア要件

バリデーターノードを実行するために、以下の最低ハードウェア要件が推奨されます。

- メモリ：8 GB RAM（最小）
- CPU：6コア
- ディスク：500 GB SSDストレージ
- 帯域幅：ダウンロード1 Gbps / アップロード1 Gbps

## ノードの実行

まず、[フルコンセンサスノードの設定](full-consensus-node.md)に関する指示に従ってください。

### オプション：作業ディレクトリのリセット

過去にsunrisedの作業ディレクトリを初期化したことがある場合は、新しいディレクトリを再初期化する前にクリーンアップする必要があります。次のコマンドを実行することでクリーンアップできます。

```bash
sunrised tendermint unsafe-reset-all
```

### 作業ディレクトリの初期化

次のコマンドを実行します。

```bash
CHAIN_ID=sunrise-1 # メインネットの場合
MONIKER="validator-name"
sunrised init "$MONIKER" --chain-id $CHAIN_ID
```

[Github](https://github.com/sunriselayer/network)で現在のchain-idを確認してください。

### 新しいキーの作成

```bash
VALIDATOR_WALLET="validator"
sunrised keys add $VALIDATOR_WALLET --keyring-backend test
```

### バリデーターの公開鍵

バリデーターを初期化する前に最後に必要なのは、ノードを最初に初期化したときに作成されたバリデーターの公開鍵を取得することです。バリデーターの公開鍵を取得するには、次のようにします。

```bash
sunrised tendermint show-validator
{"@type":"/cosmos.crypto.ed25519.PubKey","key":"ZQweivhEkT/akg5RT6RWkElt43rr5cf+qu/QQ5jOpmQ="}
```

### バリデーターの作成

バリデーターを作成するには、最低1 vRISEが必要です。vRISEは譲渡不可能なため、アカウントに残高がない場合は、流動性プールにポジションを作成してvRISEを獲得してください。

まず、バリデーター設定ファイル[~/.sunrise/config/validator.json]を作成します。

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

次に、次のコマンドを実行します。

```bash
sunrised tx staking create-validator [path/to/validator.json] \
    --chain-id=$CHAIN_ID \
    --from=$VALIDATOR_WALLET \
    --keyring-backend=test \
    --gas-prices=0.025uusdrise --gas-adjustment 1.2 \
    --gas=auto \
    -y
```

## バックアップ

何らかの理由でバリデーターが損傷したり失われたりした場合に復元できるように、特定のファイルをバックアップする必要があります。`~/.sunrise/config/`にある以下のファイルを安全にバックアップしてください。

- `priv_validator_key.json`
- `node_key.json`

これらのファイルのバックアップは暗号化することをお勧めします。

## バリデーターへの追加インセンティブ

コアチームは、以下のサービスを提供するバリデーターにRISEを委任します。

- IBCリレーヤー
  - チャネルごとに`100RISE`の委任
- ノードスナップショット
  - `10000RISE`の委任
- REST APIエンドポイント
  - `10000RISE`の委任

参加を希望する場合は、Discordまたはその他の方法でチームに連絡してください。
