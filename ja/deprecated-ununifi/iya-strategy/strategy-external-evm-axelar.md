# 外部EVMチェーン上の戦略コントラクトインターフェース

戦略コントラクトは、以下に説明する特定のインターフェースを満たします。

```solidity
interface IStrategy {
    function stake(uint256 amount) external;
    function unstake(uint256 amount) external;
    function epoch() external;
}
```

## Axelar

```solidity
contract MyStrategy is IStrategy, AxelarExecutable {
    // TODO
}
```
