# リソース

## ポート

### コンセンサス

| ポート | プロトコル | 詳細 | デフォルト値 | 場所 |
| --- | --- | --- | --- | --- |
| 9090 | TCP | gRPC | `localhost:9090` | `~/.sunrise/config/app.toml` |
| 1317 | TCP | REST | `tcp://localhost:1317` | `~/.sunrise/config/app.toml` |
| 26657 | TCP | RPC | `tcp://127.0.0.1:26657` | `~/.sunrise/config/config.toml` |

{% hint style='info' %}
cosmos-sdk v0.50.0以降、デフォルトでは内部接続のみが許可されています。
公開するには、必ず次のように書き換えてください
`0.0.0.0:9090`, `tcp://0.0.0.0:1317`, `tcp://0.0.0.0:26657`
{% endhint %}

### データ可用性

| ポート | プロトコル | 詳細 | デフォルトで有効 | フラグ |
| --- | --- | --- | --- | --- |
| 2121 | TCP/UDP | P2P | true | N/A |
| 26658 | HTTP | RPC | true | `--rpc.port string` |
| 26659 | HTTP | RESTゲートウェイ | false | `--gateway.port string` |
