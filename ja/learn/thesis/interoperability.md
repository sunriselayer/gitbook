# Interoperability（インターオペラビリティ）

Sovereign Rollup（ソブリン・ロールアップ） は、従来のスマートコントラクトロールアップとは異なる新しいタイプの Layer 2 ソリューションです。

従来のスマートコントラクトロールアップでは、ユーザーが L1 Settlement layer（決済層）と L2 Execution layer（実行層）の間でトークンをブリッジできるようにする "Enshrined Bridge" （「組み込みブリッジ」）が存在します。このブリッジの有効性を検証する役割は、ロールアップコントラクトが担っています。そのため、このブリッジは「組み込み」と呼ばれます。

一方、Sovereign rollup には組み込みブリッジがありません。Sovereign Rollup 側がブリッジの有効性を検証する役割を果たします。この構造により、Sovereign rollup はブリッジやインターオペラビリティを設計する柔軟な余地を持っています。具体的には、Sovereign Rollup は IBC（Inter Blockchain Communication）インターオペラビリティをサポートできます。

現時点で、Sovereign rollup の IBC をサポートすることが知られている SDK は以下の通りです：

- Rollkit
- Sovereign SDK
