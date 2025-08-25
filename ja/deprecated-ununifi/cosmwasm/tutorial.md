# チュートリアル

## wasm CLIの使い方

まず、wasm CLIと[Rust](https://www.rust-lang.org/tools/install)を使用するために`ununifid`をインストールします。`ununifid`のインストール方法については、[こちら](../cli-introduction/)をご覧ください。

wasm CLIの使い方は2通りあります。

```bash
ununifid tx wasm --help
ununifid query wasm --help
```

## コントラクトのコンパイルとテスト

[CosmWasmドキュメント](https://docs.cosmwasm.com/docs/getting-started/compile-contract)より引用

```bash
# リポジトリをダウンロードする
git clone https://github.com/CosmWasm/cw-plus
cd cw-plus
git checkout main
cd contracts/cw20-ics20

# 安定したツールチェーンでwasmコントラクトをコンパイルする
rustup default stable
cargo wasm
```

### 単体テスト

[CosmWasmドキュメント](https://docs.cosmwasm.com/docs/getting-started/compile-contract)より引用

```bash
RUST_BACKTRACE=1 cargo unit-test
```

### オプティマイザを使用したビルド

[CosmWasmドキュメント](https://docs.cosmwasm.com/docs/getting-started/compile-contract)より引用

```bash
docker run --rm -v "$(pwd)":/code \
  --mount type=volume,source="$(basename "$(pwd)")_cache",target=/code/target \
  --mount type=volume,source=registry_cache,target=/usr/local/cargo/registry \
  cosmwasm/rust-optimizer:0.12.11
```

### デプロイとインタラクション

[CosmWasmドキュメント](https://docs.cosmwasm.com/docs/getting-started/compile-contract)より引用

ビルドしたwasmスマートコントラクトをデプロイするには、`ununifid tx wasm store`コマンドを使用します。

```bash
ununifid tx wasm store --help
```

Solidityスマートコントラクトとは対照的に、CosmWasmにはスマートコントラクトを有効にするための2つの段階があります。それはデプロイとインスタンス化です。したがって、wasmスマートコントラクトをデプロイした後、`ununifid tx wasm instantiate`コマンドを使用します。

```bash
ununifid tx wasm instantiate --help
```
