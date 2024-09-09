# **Interoperability**（インターオペラビリティ）

Sovereign Rollup（ソブリン・ロールアップ）は、従来のスマートコントラクト・ロールアップとは異なる新しいレイヤー 2 のソリューションです。

従来のスマートコントラクト・ロールアップでは、「Enshrined Bridge」（埋め込まれたブリッジ）と呼ばれるものがあり、ユーザーは L1 の決済層と L2 の実行層の間でトークンをブリッジすることができます。ブリッジの有効性を検証する役割はロールアップコントラクトが果たします。そのため、このブリッジは「Enshrined Bridge」（埋め込まれたブリッジ）と呼ばれています。

一方、ソブリン・ロールアップには Enshrined Bridge はありません。ソブリン・ロールアップ側がブリッジの有効性を検証する役割を果たします。このアーキテクチャにより、ソブリン・ロールアップはブリッジや相互運用性を柔軟に設計するためのスペースを持っています。具体的には、ソブリン・ロールアップは IBC（インターブロックチェーン通信）の Interoperability（相互運用性）をサポートすることができます。

現時点では、以下の SDK がソブリン・ロールアップの IBC をサポートしていることが知られています:

- Rollkit
- Sovereign SDK