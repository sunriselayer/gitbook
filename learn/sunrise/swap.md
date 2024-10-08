# Swap

The module `x/swap` serves the functionalities to swap tokens with the liquidity in `x/liquiditypool` module.

### Interface Provider Fee Rewards

Any frontend application that is built on top of the swap module has the ability to earn fees. How is this done?

---

There are 2 important parameters to note:

- <strong>interface_fee_rate:</strong> A fee, denoted in percentage, that is taken from the total amount of the swap.

- <strong>interface_provider:</strong> An address that specifies where the fee will be sent. If no address is provided, no interface fee will be taken.

See [Github](https://github.com/sunriselayer/sunrise/tree/main/x/swap) for details.
