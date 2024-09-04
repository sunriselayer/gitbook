# **App chain thesis（アプリケーションチェーン**のテーゼ**）**

IBC（Inter Blockchain Communication）エコシステムでは、「アプリケーションチェーンのテーゼ」という概念が提案されています。その核心的なアイデアは、各 dApp のために Layer 1 ブロックチェーンを構築し、それらを IBC の Interoperability（相互運用性）を利用して接続することで、スケーラブルでセキュアなブロックチェーンエコシステムを実現することができるというものです。

この「Monolithic app chain thesis」（モノリシック・アプリケーションチェーンチェーンのテーゼ）を改名しましょう。

しかし、アプリケーションチェーンチェーンのテーゼには 1 つの弱点があります。各アプリチェーンのバリデータセットを集める必要があるため、アプリチェーンのコアチームの負荷が重くなります。これを「Validator Bootstrapping Problem」（バリデータブートストラッピングの問題）と呼びます。

この弱点のため、IBC エコシステムは成長してきましたが、IBC エコシステムが予測したレベルには達していません。

現在、アプリケーション固有のブロックチェーンを構築する際にバリデータブートストラッピングの問題を解決できるモジュラーブロックチェーンのパラダイムがあります。

Sovereign Rollup 技術を使用することで、IBC エコシステムと互換性のあるブロックチェーンを構築し、同時にバリデータブートストラッピングの問題を解決することができます。

これを「Modular app chain thesis」（モジュラーアプリチェーンのテーゼ）と呼びます。

スマートコントラクトは dApp を構築する唯一の方法ではありません。

dApp を構築する方法のメタファーを表現できると考えています：

|                               |                        |
| ----------------------------- | ---------------------- |
| Smart contract                | Shared server          |
| Modular app specific chain    | Virtual private server |
| Monolithic app specific chain | Dedicated server       |

スマートコントラクトは他の dApp のトラフィックの影響を受けやすいです。これは共有サーバーのようなものです。一方、モノリシック・アプリケーションの固有チェーンは専用サーバーのようなものです。他の dApp のトラフィックの影響を受けませんが、バリデータのブートストラッピングが高コストです。

モジュラー・アプリケーションの固有チェーンは仮想プライベートサーバーのようなものです。他の dApp のトラフィックの影響をほとんど受けず、バリデータのブートストラッピングも高価ではありません。

VPS が IaaS に成長するように、RaaS（Rollup as a Service）も成長し、スマートコントラクトを展開するのと同じくらい簡単にスケーラブルでセキュアなブロックチェーンエコシステムを構築することができるようになります。