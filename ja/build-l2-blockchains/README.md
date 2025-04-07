# サポートされるL2 SDK

## Sunriseドキュメント

- [Rollkit](./rollkit/README.md)
  - [Sunrise Data](./rollkit/sunrise-data.md)
  - [Rollkit L2チェーン](./rollkit/rollkit.md)
- [Optimism OP Stack](./optimism/README.md)
  - [Sunrise Data](./optimism/sunrise-data.md)
  - [OP Stack L2チェーン](./optimism/op-stack.md)

## L2の作成方法

外部RPCに依存せず、完全なコンセンサスノードをローカルで実行することが推奨されます。

[Sunriseコンセンサスノードドキュメント](../../../node/types/consensus/README.md)

### Rollkit

`sunrise-data`と`rollkit`を実行する必要があります。

### OP Stack

`sunrise-data`、`optimism`および`op-geth`を実行する必要があります。

ローカルのEVM L1チェーンは、OP Stackの要件を満たすためだけに使用されます。実際のデータ（メタデータ）はSunriseに保存されます。

ローカルL1チェーンとしてGanache、Hardhat、Anvilなどを使用してください。

## 要件

| タイプ                    | CPU    | アーキテクチャ | メモリ | ディスク   | 帯域幅    |
| ------------------------- | ------ | -------------- | ------ | ---------- | --------- |
| Rollkit + Sunrise Data    | 4コア   | x86_64         | 16 GB  | 1 TB SSD   | 1 Gbps    |
| OP Stack + Sunrise Data   | 6コア   | x86_64         | 32 GB  | 1 TB SSD   | 1 Gbps    |

## 公式ドキュメント

- [Rollkit](https://rollkit.dev/learn/intro)
  - [BeaconKit (オプション)](https://rollkit.dev/tutorials/execution/beaconkit): BeaconKitとRollkitを組み合わせることで、EVM互換のL2ブロックチェーンの開発が可能になります。
- [OP Stack](https://docs.optimism.io/stack/getting-started)