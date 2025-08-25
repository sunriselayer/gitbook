# バリデーターノード（ジェネシス）

バリデーターノードを使用すると、Sunriseネットワークのコンセンサスに参加できます。

{% hint style="info" %}
この方法でバリデーターとして参加できるのは、ネットワークが開始する（ジェネシス）前のみです。ネットワークがすでに開始している場合は、[こちらのチュートリアル](validator-node.md)を参照してください。
{% endhint %}

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

[Github](https://github.com/sunriselayer/network)で現在の`chain-id`を確認し、次のコマンドを実行してください。

```bash
CHAIN_ID=sunrise-1
MONIKER="validator-name"
sunrised init "$MONIKER" --chain-id $CHAIN_ID
```

`genesis.json`をネットワークリポジトリのものに変更します。

```bash
wget https://raw.githubusercontent.com/sunriselayer/network/main/sunrise-1/gentx/genesis.json
cp genesis.json $HOME/.sunrise/config/genesis.json
```

### 新しいキーの作成

```bash
VALIDATOR_WALLET="validator"
sunrised keys add $VALIDATOR_WALLET --keyring-backend test
```

### 新しいチェーンのジェネシストランザクションの作成

```bash
STAKING_AMOUNT=1000000uvrise
sunrised genesis gentx $VALIDATOR_WALLET $STAKING_AMOUNT --chain-id $CHAIN_ID \
   --pubkey=$(sunrised tendermint show-validator) \
   --moniker=$MONIKER \
   --commission-rate=0.1 \
   --commission-max-rate=0.2 \
   --commission-max-change-rate=0.01 \
   --min-self-delegation=1 \
   --keyring-backend test
```

生成されたgentx JSONファイルは`$HOME/.sunrised/config/gentx/gentx-*.json`内にあります。

### gentxを登録するためのプルリクエストの作成

gentxを登録するには、[ネットワークリポジトリ](https://github.com/sunriselayer/network/tree/main/sunrise-1/gentx)にプルリクエストを作成してください。
