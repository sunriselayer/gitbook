# Strategy contracts interface on External EVM chain

Strategy contracts satisfies the specific interface described below.

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
