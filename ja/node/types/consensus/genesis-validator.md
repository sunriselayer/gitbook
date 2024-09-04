# Validator Node (Genesis)

バリデータノードを使用すると、Sunrise ネットワークのコンセンサスに参加することができます。

{% hint style="info" %}
この方法でバリデータとして参加できるのは、ネットワークが開始される前（ジェネシス時）のみです。ネットワークがすでに開始されている場合は、[このチュートリアル](https://docs.sunriselayer.io/run-a-sunrise-node/types/consensus/validator-node)をご覧ください。
{% endhint %}

## Hardware requirements（ハードウェア要件）

バリデータノードを実行するために推奨される最小限のハードウェア要件は以下の通りです。

- Memory: 8 GB RAM (minimum)
- CPU: 6 cores
- Disk: 500 GB SSD Storage
- Bandwidth: 1 Gbps for Download/1 Gbps for Upload

## Run the Node（ノードの実行）

まず、[フルコンセンサスノード](https://docs.sunriselayer.io/run-a-sunrise-node/types/consensus/full-consensus-node)の設定手順に従ってください。

### Optional: Reset working directory（作業ディレクトリのリセット）

過去に `sunrised` の作業ディレクトリをすでに初期化している場合、新しいディレクトリを再初期化する前にクリーンアップする必要があります。以下のコマンドを実行することでクリーンアップができます。

```bash
sunrised tendermint unsafe-reset-all
```

### Initialize a working directory（作業ディレクトリの初期化）

次のコマンドを実行してください。

```bash
CHAIN_ID=sunrise-test-1
MONIKER="validator-name"
sunrised init "$MONIKER" --chain-id $CHAIN_ID
```

### Create a new key（新しいキーの作成）

```bash
VALIDATOR_WALLET="validator"
sunrised keys add $VALIDATOR_WALLET --keyring-backend test
```

### Create the genesis transaction for new chain（新しいチェーンのためのジェネシストランザクションを作成する）

```bash
STAKING_AMOUNT=1000000urise
sunrised genesis gentx $VALIDATOR_WALLET $STAKING_AMOUNT --chain-id $CHAIN_ID \
   --pubkey=$(sunrised tendermint show-validator) \
   --moniker=$MONIKER \
   --commission-rate=0.1 \
   --commission-max-rate=0.2 \
   --commission-max-change-rate=0.01 \
   --min-self-delegation=1 \
   --keyring-backend test
```

`$HOME/.sunrised/config/gentx/gentx-\*.json` の中に生成された gentx JSON ファイルが見つかります。

### Create Pull Request to register your gentx（gentx の登録のためのプルリクエストの作成）

GitHub でプルリクエストを作成するために、以下のコマンドを実行して gentx を登録してください。

```bash
 mv $HOME/.sunrised/config/gentx/gentx-*.json $HOME/.sunrised/config/gentx/gentx-${MONIKER}.json
 git clone https://github.com/sunriselayer/public-testnet/
 cd public-testnet
 git checkout -b gentx/$MONIKER
 cp $HOME/.sunrised/config/gentx/gentx-${MONIKER}.json gentx/sunrise-testnet-1
 git add gentx/sunrise-testnet-1
 git commit -m "Add gentx: $MONIKER"
 git push origin $(git branch --show-current)
```
