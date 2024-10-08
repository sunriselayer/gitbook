# リソース

## Ports

### Consensus

| Port  | Protocol | Detail | Default Value           | Location                        |
| ----- | -------- | ------ | ----------------------- | ------------------------------- |
| 9090  | TCP      | gRPC   | `localhost:9090`        | `~/.sunrise/config/app.toml`    |
| 1317  | TCP      | REST   | `tcp://localhost:1317`  | `~/.sunrise/config/app.toml`    |
| 26657 | TCP      | RPC    | `tcp://127.0.0.1:26657` | `~/.sunrise/config/config.toml` |

{% hint style='info' %}
cosmos-sdk v0.50.0 以降、デフォルトでは内部接続のみが許可されています。公開するには、必ず以下のように書き換えてください：
`0.0.0.0:9090`, `tcp://0.0.0.0:1317`, `tcp://0.0.0.0:26657`
{% endhint %}

### Data Availability

| Port  | Protocol | Detail       | Enabled by Default | Flag                    |
| ----- | -------- | ------------ | ------------------ | ----------------------- |
| 2121  | TCP/UDP  | P2P          | true               | N/A                     |
| 26658 | HTTP     | RPC          | true               | `--rpc.port string`     |
| 26659 | HTTP     | REST Gateway | false              | `--gateway.port string` |
