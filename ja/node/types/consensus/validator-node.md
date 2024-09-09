# Validator Node

バリデータノードを使用すると、Sunrise ネットワークのコンセンサスに参加することができます。

## Hardware requirements（ハードウェア要件）

バリデータノードを実行するために推奨される最小限のハードウェア要件は以下の通りです：

- Memory: 8 GB RAM (最小)
- CPU: 6 cores
- Disk: 500 GB SSD Storage
- Bandwidth: 1 Gbps for Download/1 Gbps for Upload

## Run the Node（ノードの実行）

まず、[フルコンセンサスノードの設定手順](https://docs.sunriselayer.io/run-a-sunrise-node/types/consensus/full-consensus-node)に従ってください。

### Optional: Reset working directory（作業ディレクトリのリセット）

過去に `sunrised` の作業ディレクトリをすでに初期化している場合、新しいディレクトリを再初期化する前にクリーンアップする必要があります。以下のコマンドを実行することでクリーンアップができます。

```bash
sunrised tendermint unsafe-reset-all
```

### Initialize a working directory（作業ディレクトリの初期化）

次のコマンドを実行してください。

```bash
CHAIN_ID=sunrise-1
MONIKER="validator-name"
sunrised init "$MONIKER" --chain-id $CHAIN_ID
```

### Create a new key（新しいキーの作成）

```bash
VALIDATOR_WALLET="validator"
sunrised keys add $VALIDATOR_WALLET --keyring-backend test
```

### Create Validator（バリデータの作成）

```bash
sunrised tx staking create-validator [path/to/validator.json] \
    --chain-id=$CHAIN_ID \
    --from=$VALIDATOR_WALLET \
    --keyring-backend=test \
    --fees=21000urise \
    --gas=220000
```

```json
{
  "pubkey": {
    "@type": "/cosmos.crypto.ed25519.PubKey",
    "key": "oWg2ISpLF405Jcm2vXV+2v4fnjodh6aafuIdeoW+rUw="
  },
  "amount": "1000000urise",
  "moniker": "myvalidator",
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

次に、`~/.sunrise/config/config.toml` を編集します。

## Backup（バックアップ）

何らかの理由でバリデータが損傷したり失われたりした場合に復元できるよう、特定のファイルをバックアップする必要があります。`~/.sunrise/config/` にある以下のファイルを安全にバックアップしてください。

- `priv_validator_key.json`
- `node_key.json`

これらのファイルのバックアップは暗号化することをお勧めします。

## Additional incentives for validators（バリデータへの追加のインセンティブ）

コアチームは、以下のサービスを提供するバリデータに対して RISE をデリゲートします。

- IBC relayer
  - `100000000microRISE` delegation per channel
- Node snapshot
  - `10000000000microRISE` delegation
- REST API endpoints
  - `10000000000microRISE` delegation