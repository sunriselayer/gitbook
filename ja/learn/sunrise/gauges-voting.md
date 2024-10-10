# Gauges Voting（ゲージ 投票）

## Gauge（ゲージ）とは何か？

Gauge（ゲージ）とは、vRISE を発行する当社のプロダクトを指します。
Sunrise における Gauge の最初のプロダクトは、流動性プールです。

vRISE 保有者は、vRISE を使って投票し、どの Gauge にどれだけの vRISE を割り当てるかを決定します。
より多くの Voting Power（投票力）を集めた Gauge にリンクされた流動性プールに、より多くの新規発行 vRISE が割り当てられます。

## 投票方法

### Epoch（エポック）

Gauge の重み付け投票は、パラメータによって決定された各ブロックで実施されます。
次のエポックが始まると、その時点で存在する票が集計されます。

### 資格

Gauge に投票するには、まず vRISE を獲得する必要があります。vRISE は主に流動性プールに流動性を供給することで獲得できます。

エポック開始時の有効な vRISE 残高が投票に使用されます。ロックされた vRISE は反映されません。

{% hint style="info" %}
vRISE を保有していなくても投票は可能です。エポック開始時の vRISE 残高が反映されます。
{% endhint %}

### 現在の投票結果

ガバナンスタブの「現在の Gauge 投票を表示」に移動してください。

- Current Votes（現在の投票）

  - エポックブロック
    エポックが更新されるブロック数。オンチェーンガバナンスによって決定されます。
  - ステーキング報酬比率
    元々ステーキングに発行された vRISE のうち、Gauge に割り当てられる割合。オンチェーンガバナンスによって決定されます。
  - 投票数
    何人が投票しているか。

- Current Epoch（現在のエポック）

  - Total Votes（総投票数）
  - Start（開始）
  - End（終了）
  - Previous Epoch（前回のエポック）

下部には、すべての投票 Gauge の完全なリストがあります。
「投票」には、各 Gauge の投票力と総投票数に対する割合が表示されます。

{% hint style="warning" %}
チェーン上に存在するエポックは「現在」と「前回」の 2 つだけです。それ以前のエポックは削除されるため、情報を参照することはできません。
{% endhint %}

### 投票する Gauge の追加

Gauge に投票するには、`My Votes`をクリックします。
「プールを選択」をクリックし、ポップアップから任意のプールを選択します。

すでに Gauge に投票している場合は、現在の投票状況が自動的に入力されます。
Gauge への投票を停止するには、削除ボタンをクリックします。

### 各 Gauge に vRISE の何%を投票するかを選択

Gauge を追加したら、各 Gauge に vRISE の何%を割り当てるかを選択できます。

- vRISE 残高は変動します。ロック、インセンティブ付与など。各エポック開始時の投票者の残高は不明なため、割合を指定する必要があります。
- 今後のすべてのエポックで再投票するのは面倒です。そのため、Gauge 投票は、新しい投票を行うまで、あなたの投票決定をすべての今後のエポックにわたって引き継ぐように設計されています。

「投票のプレビュー」には、現在の残高に基づいた各 Gauge の投票数が表示されます。

決定を確認したら、`Vote`をクリックしてトランザクションを送信します。

### 投票の更新

投票を提出すると、「My Gauge Votes」に投票が更新されているのが確認できます。
投票はいつでも更新でき、エポック開始時に最新の投票が適用されます。

投票の決定を更新するには、再度`Vote`をクリックしてトランザクションを送信します。