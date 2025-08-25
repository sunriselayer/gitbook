# 🚀 クイックスタート

> ローカルのSunrise DAノード、最小限のRollkitベースのソブリンロールアップ、
> およびサンプルdAppを**20分以内**に実行します。

> **注**: Sunriseでの構築のすべての側面をカバーする包括的なガイド（詳細なモジュールリファレンス、高度な統合パターンなど）については、[Sunrise Builders Kit](https://cauchye.notion.site/Sunrise-Builders-Kit-1e02cd22bc1680f3bebcd4f02f2fbc18?pvs=4)をご覧ください。

このガイドでは、Sunrise Layerで構築するための完全な開発環境を設定する方法を説明します。次のことを学びます。

- ローカルのSunriseデータ可用性（DA）ノードを設定する
- Rollkitを使用して最小限のソブリンロールアップを作成する
- Sunriseクライアントを使用してネットワークと対話する
- 主要な機能を示すサンプルdAppを実行する

Sunriseでの構築のすべての側面をカバーする包括的なガイドについては、[Sunrise Builders Kit](https://cauchye.notion.site/Sunrise-Builders-Kit-1e02cd22bc1680f3bebcd4f02f2fbc18?pvs=4)をご覧ください。

---

## 前提条件

開始する前に、次のツールがインストールされていることを確認してください。

| ツール | バージョン | 目的 |
| --- | --- | --- |
| **Go** | `>=1.22` | Sunriseバイナリとコアコンポーネントをビルドする |
| **Rust + Cargo** | stable | Rollkitデモチェーンとスマートコントラクトをビルドする |
| **Node.js** | `>=20` | JSクライアント、スクリプト、Webアプリケーションを実行する |
| **Docker + Docker Compose** | latest | コンテナ化されたサービスと開発スタックを実行する |
| （オプション）**direnv** | any | シェルで環境変数を自動的にロードする |

```bash
# macOS（brew）の例
brew install go rustup node docker direnv
rustup default stable
```

## 1. リポジトリをクローンする

3つの主要コンポーネントで開発プレイグラウンドを作成します。

```bash
mkdir sunrise-playground && cd $_
git clone https://github.com/sunriselayer/network     sunrise-da
git clone https://github.com/rollkit/rollkit          rollkit
git clone https://github.com/sunriselayer/examples    examples
```

- `sunrise-da`: コアのSunriseネットワーク実装
- `rollkit`: ソブリンロールアップを構築するためのフレームワーク
- `examples`: サンプルアプリケーションと統合の例

## 2. ローカルのSunrise DAノードを起動する

Sunrise DAノードはネットワークの基盤であり、ロールアップにデータ可用性サービスを提供します。

```bash
cd sunrise-da
make install             # 'sunrised'をビルドします
sunrised init dev --chain-id goldberg-local
sunrised start
```

> ヒント：代わりにDockerで実行したいですか？
>
> ```bash
> docker compose -f docker/local-da.yml up --build
> ```

### ポート

| サービス | ポート | 目的 |
| --- | --- | --- |
| Tendermint RPC | 26657 | トランザクションとクエリのメインRPCエンドポイント |
| gRPC | 9090 | 高度な操作のためのプロトコルバッファインターフェース |

## 3. アカウントに資金を供給する（フォーセット）

ネットワークと対話するためにテストアカウントを作成し、資金を供給します。

```bash
sunrised keys add alice --keyring-backend test
sunrised tx bank mint $(sunrised keys show alice -a) 1000000000urise \
  --from alice --keyring-backend test --yes
```

これにより、「alice」という名前の新しいアカウントが作成され、テスト用に10億マイクロRISEトークン（`urise`）がミントされます。

## 4. 最小限のRollkitソブリンロールアップを起動する

Rollkitは、データ可用性のためにSunriseを使用できるソブリンロールアップを構築するためのフレームワークです。

```bash
cd ../rollkit
make demo                # デモバイナリ'demo-rollup'をビルドします

# BLOBをSunrise DAに保存するようにRollkitを設定します
cat <<EOF > rollup.config.toml
[da]
rpc_address = "http://localhost:26657"
fee_denom   = "uusdrise"
gas_price   = "0.025"
[rollup]
chain_id = "demo-rollup-1"
EOF

./demo-rollup start --config rollup.config.toml
```

ロールアップは、ブロックデータを自動的にSunriseに公開し、DA証明を取得します。

## 5. @sunriselayer/clientでBLOBを投稿して検証する

Sunriseクライアントは、Sunriseネットワークと対話するためのJavaScript/TypeScriptライブラリです。使用方法は次のとおりです。

```bash
# ルートのプレイグラウンドディレクトリ内
npm create vite@latest js-client-demo -- --template vanilla
cd js-client-demo && npm i @sunriselayer/client

cat <<'JS' > src/index.js
import { SunriseClient } from "@sunriselayer/client";

const rpc = "http://localhost:26657";
const main = async () => {
  const client = await SunriseClient.connect(rpc);

  const { transactionHash } = await client.da.submitBlob(
    "Hello Sunrise!",
    { gasLimit: 200_000, feeDenom: "uusdrise", gasPrice: "0.025" }
  );
  console.log("Blob tx:", transactionHash);

  const proof = await client.da.getBlobProof(transactionHash);
  console.log("Inclusion proof:", proof);
};
main();
JS
node src/index.js
```

この例では、次のことを示します。

- Sunriseノードへの接続
- データBLOBの送信
- 包含のマークル証明の取得

## 6. サンプルdAppを実行する（トークンスワップ）

サンプルdAppは、Sunriseの流動性プールモジュールを使用したトークンスワップを示します。

```bash
cd ../../examples/swap-demo
npm i
npm run dev        # http://localhost:5173を開きます
```

デモUI：

- @sunriselayer/clientに接続します
- ロールアップのx/swapモジュールを介してテストトークンをスワップします
- Sunrise DAから取得したライブ残高を表示します

## 7. 次のステップ

| 内容 | 場所 | 説明 |
| --- | --- | --- |
| 完全なクライアントリファレンス | [クライアントドキュメント](/build/client/README.md) | @sunriselayer/clientの完全なAPIドキュメント |
| 本番用Rollkitチェーンの構築 | [Rollkitガイド](/build/l2-blockchains/rollkit/README.md) | 本番用ロールアップのデプロイガイド |
| バリデーターとDA証明 | [バリデーターガイド](/build/validators/README.md) | バリデーターのセットアップとDA証明の生成について学ぶ |
| 概念的な詳細 | [学習セクション](/learn/sunrise/README.md) | Sunriseのコアコンセプトを理解する |

## トラブルシューティング

| 症状 | 修正 | 説明 |
| --- | --- | --- |
| ポート26657でECONNREFUSED | `sunrised start`が実行されていないか、RPC URLが間違っている | Sunriseノードが実行され、アクセス可能であることを確認してください |
| RollkitがBLOBを投稿できない | `~/.sunrise/config/app.toml`で`min-gas-prices`を確認してください | ガス価格の設定がネットワーク要件と一致していることを確認してください |
| BLOB txがメモリプールでスタックしている | ガス価格が低い → `--gas-prices 0.025urise`を使用してください | トランザクション処理を確実にするためにガス価格を上げてください |

## クリーンアップ

```bash
pkill sunrised demo-rollup || true
docker compose -f docker/local-da.yml down -v || true
rm -rf ~/sunrise-playground
```

ハッピーハッキング！🎉
