# Liquidity Restaking

Sunrise chain supports minting LP tokens of `XXX/BondedSR` for any token `XXX` (includes LST of some tokens), and that LP token can be used for staking in Sunrise Proof of Stake.

By using this solution, Sunrise Proof of Stake can be enhanced its security with external tokens.

## Security enhancement

Just staking external tokens to Sunrise is also theoretically possible, but as we researched the security model of Data Availability layers, restaking external tokens to DA layers will lead to the disincentive not to do malicious behaviors in the Layer 2 chains that uses the DA.
Simply saying, Proof of Stake mechanism has an element of preventing malicious behaviors by giving network participants an expectation of token price downfalling when the malicious behavior is observed and the credibility or brand of the DA layer get damaged.
However, for example, EigenDA only depends on restaked ETH tokens to determine the voting powers and trivially the price of LSTs of ETH are not affected by the credibility or the brand of EigenDA, whereas the price of TIA can be considered to be affected by the credibility or the brand of Celestia. After our research, we concluded that the weight of the dependency to the external token in staking system should be kept optimal as the disincentive not to have malicious behavior doesn't occur.

This Liquidity restaking mechanism force stakers of `XXX/BondedSR` to get impermanent losses when the credibility or the brand of Sunrise get damaged.
This mechanism enhance the security of Sunrise DA layer at the same time to enhance the liquidity of `BondedSR` and decreasing the circulation supply of `SR` token.
