# Withdraw Reserve Rate

Total amount of deposit consists of three components.

$$
  \text{TotalAmount} = \text{BondingAmount} + \text{UnbondingAmount} + \text{WithdrawReserve}
$$

Withdraw reserve rate means

$$
  \text{WithdrawReserve} = \text{TotalAmount} \times \text{WithdrawReserveRate}
$$

Withdraw reserve will be used for withdrawal with zero unbonding time.

Of course, if many people request withdrawal at the same time, withdraw reserve will be insufficient to respond to all withdrawal with zero unbonding time.

To tackle this problem, we prepared a formula to calculate withdraw fee.

$$
  \text{ReserveMaintenanceRate} = \frac{\max(0, \text{WithdrawReserve} - \text{AmountToWithdraw})}{\text{WithdrawReserve} + \text{UnbondingAmount}}
$$

$$
  \text{WithdrawFeeRate} = \exp{\left( -10 * \text{ReserveMaintenanceRate} \right)}
$$

$$
  \text{WithdrawFee} = \text{WithdrawFeeRate} \times \text{AmountToWithdraw}
$$
