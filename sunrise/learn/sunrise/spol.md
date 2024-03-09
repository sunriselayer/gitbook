# Sovereign Proof of Liquidity

As we described before, we integrates some unique features in Sunrise as a DA layer. One of them is Sovereign Proof of Liquidity (SPoL).

In general, crypto-asset projects must reward to the participants of the community who did:

- Participating in the governance
- Providing liquidity

It is difficult to reward these participants at the same time with conventional methods.
SPoL is a mechanism that can reward both participants at the same time.

Imagine that there is a Sovereign rollup called XXX. The native token of XXX is called $XXX. The SPoL mechanism is as follows:

- Gluon supports DEX pair of $XXX and $BondedSR, the Liquid Staking Token of $SR.
  - The DEX pair is called `XXX/BondedSR`.
- Gluon supports LP token of `XXX/BondedSR`.
  - Let's call the LP token as `LP-XXX/BondedSR`.
- Sunrise and Gluon supports staking of `LP-XXX/BondedSR` for Sovereign rollups.

In this mechanism, the participants can stake `LP-XXX/BondedSR` to the Sovereign rollup XXX. Sovereign rollup projects can reward the stakers of `LP-XXX/BondedSR` with $XXX and $BondedSR at the same time, and make their token liquidity.
