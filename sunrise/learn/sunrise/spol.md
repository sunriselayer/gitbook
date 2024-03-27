# Sovereign Proof of Liquidity

As we described before, we integrates some unique features in Sunrise as a DA layer. One of them is Sovereign Proof of Liquidity (SPoL).

In general, crypto-asset projects must reward to the participants of the community who did:

- Participating in the governance
- Providing liquidity

It is difficult to reward these participants at the same time with conventional methods.
SPoL is a mechanism that can reward both participants at the same time.

By using SPoL mechanism, Sovereign rollup can utilize LP token `LP-XXX/BondedSR` that is issued via [Liquidity Pool module](./liquidity-pool.md) and easily swap their native token with the rich liquidity seemlessly through IBC interoperability with Gluon.

In this mechanism, the participants can stake `LP-XXX/BondedSR` to the Sovereign rollup XXX. Sovereign rollup projects can reward the stakers of `LP-XXX/BondedSR` with $XXX and $BondedSR at the same time, and make their token liquidity.
