# バリデーターになる方法

このドキュメントでは、Sunriseチェーンでバリデーターになるための手順を説明します。

## 前提条件

バリデーターを運用する前に、[フルコンセンサスノード](../../run-a-sunrise-node/types/consensus/full-consensus-node.md)を設定し、ネットワークと完全に同期している必要があります。

## データ可用性の検証

{% hint style="warning" %}
Sunriseネットワークのバリデーターは、データ可用性（DA）レイヤーのデータを検証する必要があります。これは重要な責任です。設定方法については、[データ可用性レイヤーの証明](data-availability-proof.md)ガイドを参照してください。
{% endhint %}

## Cosmovisorの設定

メインネットでは、ノードの実行にCosmovisorを使用することを強くお勧めします。Cosmovisorを使用すると、最小限のダウンタイムでチェーンのアップグレードをスムーズに実行できます。

詳細については、[Cosmovisor設定チュートリアル](../../run-a-sunrise-node/types/consensus/setup-cosmovisor.md)に従ってください。

自動アップグレードを有効にするには、次の環境変数を設定することをお勧めします。

```bash
export DAEMON_ALLOW_DOWNLOAD_BINARIES=true
```

## バイナリとジェネシスファイル

バリデーターを設定する際には、正しいバージョンのバイナリと`genesis.json`を使用することが重要です。

* **バイナリ:** 最新のバイナリは[GitHubリリース](https://github.com/sunriselayer/sunrise/releases/tag/v1.0.0)からダウンロードできます。
* **ジェネシスファイル:** `genesis.json`ファイルは[ネットワークリポジトリ](https://github.com/sunriselayer/network/tree/main/sunrise-1)にあります。

## バリデーターの作成

バリデーターを作成するには、ジェネシスで参加する方法と、チェーンが開始した後に参加する方法の2つがあります。

### ジェネシスバリデーターとして参加する（Gentx）

ネットワークが開始する前にバリデーターとして参加する（ジェネシスバリデーターとして）には、`gentx`（ジェネシストランザクション）を生成して送信する必要があります。

詳細な手順については、[sunriselayer/networkリポジトリのREADME](https://github.com/sunriselayer/network/blob/main/sunrise-1/gentx/README.md)を参照してください。

### チェーン開始後にバリデーターとして参加する

チェーンがすでに実行されている場合は、次の方法でバリデーターを作成できます。

#### `tx staking create-validator`

これは標準のCosmos SDKメソッドで、`validator.json`ファイルを使用してバリデーターを作成します。このメソッドでは、自己委任のために`vRISE`が必要です。

1. **バリデーターの公開鍵を取得する**

    `sunrised tendermint show-validator`コマンドを実行して、バリデーターの公開鍵（pubkey）を取得します。

    ```bash
    sunrised tendermint show-validator
    ```

2. **`validator.json`ファイルを作成する**

    次の内容で`validator.json`ファイルを作成します。上記で取得した値で`pubkey`を設定します。

    ```json
    {
        "pubkey": {"@type":"/cosmos.crypto.ed25519.PubKey","key":"oWg2ISpLF405Jcm2vXV+2v4fnjodh6aafuIdeoW+rUw="},
        "amount": "1000000uvrise",
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

    * `amount`は`uvrise`で指定します。
    * `min-self-delegation`も`vRISE`の量です。
3. **`create-validator`トランザクションを送信する**

    ```bash
    sunrised tx staking create-validator path/to/validator.json --from <keyname> --chain-id <chain-id> --gas="auto" --gas-prices=<gas-prices> -y
    ```

    **使用法:**

    ```bash
    sunrised tx staking create-validator [path/to/validator.json] [flags]
    ```

## バックアップ

キーファイルのバックアップは、バリデーターの運用にとって重要です。次のファイルを安全な場所にバックアップしてください。

* `~/.sunrise/config/priv_validator_key.json`
* `~/.sunrise/config/node_key.json`

これらのバックアップファイルを暗号化することを強くお勧めします。
