# バリデータノード（ジェネシス）

バリデータノードを使用すると、Sunriseネットワークのコンセンサスに参加することができます。

{% hint style="info" %}
この方法でバリデータとして参加できるのは、ネットワークが開始される前（ジェネシス時）のみです。ネットワークがすでに開始されている場合は、[このチュートリアル](validator-node.md)をご覧ください。
{% endhint %}

## ハードウェア要件

バリデータノードを実行するために推奨される最小限のハードウェア要件は以下の通りです。

- メモリ：8 GB RAM（最小）
- CPU：6コア
- ディスク：500 GB SSDストレージ
- 帯域幅：ダウンロード1 Gbps / アップロード1 Gbps

## ノードの実行

まず、[フルコンセンサスノード](full-consensus-node.md)の設定手順に従ってください。

### オプション: 作業ディレクトリのリセット

過去に`sunrised`の作業ディレクトリをすでに初期化している場合、新しいディレクトリを再初期化する前にクリーンアップする必要があります。以下のコマンドを実行することでクリーンアップができます。

```bash
sunrised tendermint unsafe-reset-all
```

### 作業ディレクトリの初期化

次のコマンドを実行してください。

```bash
CHAIN_ID=sunrise-1
MONIKER="validator-name"
sunrised init "$MONIKER" --chain-id $CHAIN_ID
```

現在のchain-idを知るには、[私たちのGithub](https://github.com/sunriselayer/network)を確認してください。

### 新しいキーの作成

```bash
VALIDATOR_WALLET="validator"
sunrised keys add $VALIDATOR_WALLET --keyring-backend test
```

### 新しいチェーンのためのジェネシストランザクションを作成する

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

`$HOME/.sunrised/config/gentx/gentx-*.json`の中に生成されたgentx JSONファイルが見つかります。

### gentxの登録のためのプルリクエストの作成

GitHubでプルリクエストを作成するために、以下のコマンドを実行してgentxを登録してください。

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