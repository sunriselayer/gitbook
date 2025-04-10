# バリデータ

- [バリデータノード](../../node/types/consensus/validator-node.md)
- [データ可用性の証明](./data-availability-proof.md)
- [セルフデリゲーション](./self-delegation.md)

まず、バリデータノードを作成します。バリデータノードが起動されると、ブロックの検証と生成が行われます。

Sunriseでは、バリデータはブロック生成に加えて、データ可用性層のデータを検証する責任も負っています。
sunrise-dataにはこのプロセスを自動化するコードが含まれており、バリデータが検証作業を実行できるようになっています。

したがって、バリデータノードは以下の3つのデーモンを実行する必要があります

1. sunrised (cosmovisorと連携することを推奨)
1. sunrise-data validator
1. IPFS Daemon