# Architecture of NFT Backed Loan

## Extendibility

`nftbackedloan` modules serves an original algorithm that is different from simple Peer-to-Peer lending. It solves the problem of simple Peer-to-Peer lending that it takes a long time to find a lender who is willing to lend the exact amount of money that the borrower wants to borrow, while the merit of Peer-to-Peer lending is preserved. For example, we don't need to depend on any oracles.

However, thanks to the algorithm, the module can integrate the element of Peer-to-Pool lending.
Though Peer-to-Pool lending depends on oracles, it can reduce the user operations.

By combining the two elements, the module can provide a new type of lending service.

For developers, see [here](../../../develop/nft-lending-pool.md).

## Generality of the architecture

It can be said that the architecture of `nftbackedloan` module is the most generalized architecture among the oracle less lending services, includes fungible token backed lending services.
To clarify this, we will show one example.

Imagine the following situation.

- There is an NFT that realizes "Token Bound Account"
- There is a Lending Pool contract that evaluates the value of fungible tokens in the account bound by that NFT

In this situation, the lending with that NFT as collateral can be regarded as a special case of the lending with fungible tokens as collateral.
In other words, the architecture of `nftbackedloan` module is a generalized one that contains special case of the lending with FTs as collateral.

This is why UnUniFi is a sector specific chain, not a single application chain.
It can be extended to any usecases in the sector like fungible token lending.

### Perspective of option trading

The architecture of `nftbackedloan` module can be also expressed in the perspective of option trading.
We can say that, in this architecture, the lender sells a put option to the borrower.
To understand this, looking similar architecture like liquidation less lending [Myso](https://www.myso.finance/) would be helpful.
In the Myso's architecture, the borrower sells their collateral at first, then the lender sells call options to borrowers to buy back the collateral.
The pay off of this architecture is equivalent to the case that the lender lends assets and sells a put option to the borrower.

So ultimately, the architecture of UnUniFi's `nftbackedloan` module contains the liquidation-less FT lendings as a special case.
