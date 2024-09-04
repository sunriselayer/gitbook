# **Liquidity Pool（流動性プール）**

`x/liquiditypool`モジュールは、集中流動性 AMM（自動マーケットメーカー）メカニズムを持つ流動性プール用です。

## **Pool（プール）**

各プールには以下のパラメータがあります：

- `denom_base`: 基準通貨
- `denom_quote`: 相手通貨
- `fee_rate`: 手数料率
- `tick_params`: ティックパラメータ

## **Tick（ティック）**

各プールには 2 つのパラメータがあります：

- `price_ratio`: 通常は`1.0001`
- `base_offset`: 通常は`0`、それ以外の場合は`[0, 1)`の範囲

ティックと価格の変換式は以下の通りです：
price(tick) = price_ratio^(tick - base_offset)

典型的なケースでは、
price(tick) = 1.0001^tick
となり、これは Uniswap V3 と同じです。

## **Position（ポジション）**

各ポジションには以下の情報があります：

- `lower_tick`: ポジションの範囲の最小価格を一意に決定します
- `upper_tick`: ポジションの範囲の最大価格を一意に決定します

## **MsgCollectFees**

ユーザーは流動性提供の報酬として手数料を請求できます。

- `position_ids`: 手数料を回収するポジション ID のリスト

## **MsgCollectIncentives**

ユーザーは流動性提供のインセンティブとして$vRISE トークンを請求できます。

- `position_ids`: インセンティブを回収するポジション ID のリスト

## **Swap（スワップ）**

トークンをスワップするためのトランザクションを送信するには、`x/swap`モジュールのメッセージを使用します。
