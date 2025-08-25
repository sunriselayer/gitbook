# 便利なCLIコマンド

`ununifi`デーモンから標準のデバッグ情報を取得します。

```bash
ununifid status
```

ノードが追いついているかどうかを確認します。

```bash
# RPC経由でクエリ（デフォルトポート：26657）
curl http://localhost:26657/status | jq .result.sync_info.catching_up
```

ノードIDを取得します。

```bash
ununifid tendermint show-node-id
```

{% hint style="info" %}
ピアアドレスは、これにホストとポートを加えたものになります。つまり、デフォルトポートを使用している場合は`<id>@<host>:26656`です。
{% endhint %}

ジェイルされているか、トゥームストーンになっているかを確認します。

```bash
ununifid query slashing signing-info $(ununifid tendermint show-validator)
```

`valoper`アドレスを取得します。

```bash
ununifid keys show <your-key-name> -a --bech val
```

現在のボックスのキーを表示します。

```bash
ununifid keys list
```

ニーモニックからキーをインポートします。

```bash
ununifid keys add <new-key-name> --recover
```

秘密鍵をエクスポートします（警告：何をしているか理解していない限り、これを行わないでください！）

```bash
ununifid keys export <your-key-name> --unsafe --unarmored-hex
```

報酬（バリデータ手数料を含む）を引き出します。`ununifivaloper1...`はバリデータアドレスです。

```bash
ununifid tx distribution withdraw-rewards <ununifivaloper1...> --from <your-key>  --commission
```

ステーク：

```bash
ununifid tx staking delegate <ununifivaloper1...> <AMOUNT>uununifi --from <your-key>
```

`--generate-only`を使用して、コマンドのJSONがどうなるかを確認します。

```bash
ununifid tx bank send $(ununifid keys show <your-key-name> -a) <recipient addr> <AMOUNT>uununifi --generate-only
```

CLI経由でバリデータセット（およびジェイルステータス）をクエリします。

```bash
ununifid query staking validators --limit 1000 -o json | jq -r '.validators[] | [.operator_address, (.tokens|tonumber / pow(10; 6)), .description.moniker, .jail, .status] | @csv' | column -t -s"," | sort -k2 -n -r | nl
```

コントラクトの状態を取得します。

```bash
ununifid q wasm contract-state all <contract-address>
```
