# Gluon Validator Node

バリデータノードは、Gluon ネットワークでコンセンサスに参加することを可能にします。Gluon は、Sunrise のソブリンロールアップ上で動作しています。

## ノードを実行する

まず、[フルノードの設定手順](https://docs.sunriselayer.io/run-a-gluon-node/nodes)に従ってください。

```bash
MONIKER="your_moniker"
VALIDATOR_WALLET="validator"

gluond tx staking create-validator [path/to/validator.json] \
    --chain-id=$CHAIN_ID \
    --from=$VALIDATOR_WALLET \
    --keyring-backend=test \
    --fees=21000uglu \
    --gas=220000
```

```json
{
  "pubkey": {
    "@type": "/cosmos.crypto.ed25519.PubKey",
    "key": "oWg2ISpLF405Jcm2vXV+2v4fnjodh6aafuIdeoW+rUw="
  },
  "amount": "1000000uglu",
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

次に、`~/.gluon/config/config.toml` を編集してください。

## バックアップ

何らかの理由でバリデータが損傷したり、失われたりした場合に復元できるように、以下のファイルをバックアップしておく必要があります。`~/.gluon/config/` にある以下のファイルを安全にバックアップしてください：

- `priv_validator_key.json`
- `node_key.json`

これらのファイルのバックアップは、暗号化することをお勧めします。
