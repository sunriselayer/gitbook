# クライアント

Sunriseクライアントライブラリを使用すると、カスタムのprotobufツーリングを実行したり、Tendermint JSON-RPCコールを手作業で作成したりすることなく、アプリケーションからチェーンの**クエリ**、**BLOBの送信**、**トランザクションの署名/ブロードキャスト**を行うことができます。

## 利用可能なSDK

* **JavaScript / TypeScript** - npmで利用可能なプライマリSDK
* **Rust** - Buf/Prostを使用したgRPC + protobuf型生成
* **Go**および**Python**バインディング - 近日公開予定（貢献を歓迎します）

## JavaScript / TypeScript SDK

[Sunriseクライアント](https://github.com/sunriselayer/sunrise-client-js)

### インストール

```bash
npm install @sunriselayer/client @cosmjs/proto-signing @cosmjs/stargate
# または
pnpm add @sunriselayer/client @cosmjs/proto-signing @cosmjs/stargate
# または
yarn add @sunriselayer/client @cosmjs/proto-signing @cosmjs/stargate
```

### 基本的な使用法

このクライアントは、Cosmos SDKチェーンと対話するための標準ライブラリである[CosmJS](https://cosmos.github.io/cosmjs/)と共に使用するように設計されています。

以下は、集中流動性ポジションを作成する方法の例です。

```typescript
import {
  createEncodeObject,
  sunriseTypesRegistry,
} from "@sunriselayer/client";
// すべてのモジュールのスキーマと型はクライアントからエクスポートされます。
// ここでは、`MsgCreatePosition`メッセージのスキーマをインポートします。
import { MsgCreatePositionSchema } from "@sunriselayer/client/types/liquiditypool";
import { DirectSecp256k1HdWallet } from "@cosmjs/proto-signing";
import { SigningStargateClient, coin } from "@cosmjs/stargate";

const RPC = "https://goldberg-rpc.sunrise.node"; // ノードに置き換えてください
const SENDER_MNEMONIC = process.env.MNEMONIC!;   // 秘密鍵は絶対にコミットしないでください

// これは簡略化された例です。実際のアプリケーションでは、クエリクライアントから
// プールの詳細を取得し、ユーザーが提供した価格からティックを計算します。
const MOCK_POOL_ID = 1n; // 注：uint64フィールドにはBigIntを使用してください
const MOCK_LOWER_TICK = -20000n;
const MOCK_UPPER_TICK = 20000n;

async function main() {
  // 1. ニーモニックからウォレットと署名者を作成します
  const signer = await DirectSecp256k1HdWallet.fromMnemonic(SENDER_MNEMONIC, {
    prefix: "sunrise", // SunriseのBech32アドレスプレフィックス
  });
  const [account] = await signer.getAccounts();
  const senderAddress = account.address;
  console.log("送信者アドレス:", senderAddress);

  // 2. 署名者と型レジストリを使用して署名クライアントを作成します
  const client = await SigningStargateClient.connectWithSigner(RPC, signer, {
    registry: sunriseTypesRegistry, // Sunriseメッセージのカスタム型レジストリ
  });
  console.log("正常に接続しました:", RPC);

  // 3. 「Create Position」トランザクションメッセージを準備します
  // すべてのメッセージフィールドは完全に型付けされ、検証されます。
  const msg = createEncodeObject(MsgCreatePositionSchema, {
    sender: senderAddress,
    poolId: MOCK_POOL_ID,
    lowerTick: MOCK_LOWER_TICK,
    upperTick: MOCK_UPPER_TICK,
    // @cosmjs/stargateの`coin`ヘルパーを使用してCoinオブジェクトを作成します
    tokenBase: coin("1000000", "urise"), // 1 RISE
    tokenQuote: coin("5000000", "uusdc"), // 5 USDC（例）
    minAmountBase: "0", // スリッページ保護
    minAmountQuote: "0", // スリッページ保護
  });

  // 4. 手数料を定義し、トランザクションに署名してブロードキャストします
  const fee = {
    amount: [coin("10000", "uusdrise")],
    gas: "400000", // ガス制限
  };
  const memo = "Created position via @sunriselayer/client";

  console.log("トランザクションをブロードキャストしています...");
  const { transactionHash } = await client.signAndBroadcast(
    senderAddress,
    [msg],
    fee,
    memo
  );

  console.log("正常にポジションを作成しました！");
  console.log("トランザクションハッシュ:", transactionHash);
}

main().catch(console.error);
```

TypeScriptを使用する場合、すべてのメソッドは完全に型付けされます。

## Rust SDK（近日公開）

Rust SDKは現在、protobuf生成を通じて実装されています。セットアップ方法は次のとおりです。

### プロジェクト構造

```
my-sunrise-client/
├── src/
│   └── main.rs
├── buf.yaml
└── buf.gen.yaml
```

### 設定ファイル

1. `buf.yaml`:

```yaml
version: v2
deps:
  - buf.build/cosmos/cosmos-sdk
  - buf.build/cosmos/cosmos-proto
  - buf.build/cosmos/gogo-proto
  - buf.build/protocolbuffers/wellknowntypes
```

2. `buf.gen.yaml`:

```yaml
version: v2
managed:
  enabled: true

plugins:
  - remote: buf.build/community/neoeinstein-prost:v0.4.0
    out: src
    opt:
      - compile_well_known_types
      - extern_path=.google.protobuf=::pbjson_types
  - remote: buf.build/community/neoeinstein-prost-serde:v0.3.1
    out: src
  - remote: buf.build/community/neoeinstein-tonic:v0.4.1
    out: src
    opt:
      - compile_well_known_types
      - extern_path=.google.protobuf=::pbjson_types

inputs:
  - git_repo: https://github.com/sunriselayer/sunrise.git
    branch: main
    subdir: proto
```

### セットアップと生成

```bash
# 必要な依存関係を追加します
cargo add tonic tonic-build pbjson-types

# 依存関係を更新し、コードを生成します
buf dep update
buf generate
```

### 使用例

```rust
use tonic::transport::Channel;
use sunriselayer::sunrise::da::v1::query_client::QueryClient;
use sunriselayer::sunrise::da::v1::ParamsRequest;

#[tokio::main]
async fn main() -> anyhow::Result<()> {
    let mut client = QueryClient::connect("http://localhost:9090").await?;
    let resp = client.params(ParamsRequest {}).await?;
    println!("DA params: {:?}", resp.into_inner());
    Ok(())
}
```

## 追加リソース

* [完全なJavaScriptメソッドリファレンス](https://github.com/SunriseLayer/gitbook/blob/main/build/client/reference/README.md)
* [ロールアップ統合の例](l2-blockchains/)
* [データ可用性の証明](validators/)

## トラブルシューティング

| 問題 | 解決策 |
| --- | --- |
| 接続が拒否されました | RPC URLを確認し、DAノードが実行されていることを確認してください |
| 認証エラー | アカウントに十分な資金があることを確認してください |
| Rustのビルド失敗 | Rust 1.74+に更新し、`cargo clean && buf generate`を実行してください |
