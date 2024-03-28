# Liquidity Restaking

Sunrise chain supports minting LP tokens of `XXX/BondedSR` for any token `XXX` (includes LST of some tokens), and that LP token can be used for staking in Sunrise Proof of Stake.

By using this solution, Sunrise Proof of Stake can enhance its security with external tokens.

## Security enhancement

Just staking external tokens to Sunrise is also theoretically possible, but as we researched the security model of Data Availability layers, restaking external tokens to DA layers will lead to the disincentive not doing malicious behaviors in the Layer 2 chains that use the DA. Simply put, Proof of Stake mechanism has an element of preventing malicious behaviors by giving network participants an expectation of token price downfalling when the malicious behavior is observed and the credibility or brand of the DA layer gets damaged. However, for example, EigenDA only depends on restaked ETH tokens to determine the voting powers and trivially the price of LSTs of ETH are not affected by the credibility or the brand of EigenDA, whereas the price of TIA can be considered to be affected by the credibility or the brand of Celestia. After our research, we concluded that the weight of the dependency on the external token in the staking system should be kept optimal as the disincentive not to have malicious behavior doesn't occur.

This Liquidity restaking mechanism forces stakers of `XXX/BondedSR` to get impermanent losses when the credibility or the brand of Sunrise gets damaged. This mechanism enhances the security of the Sunrise DA layer and at the same time enhances the liquidity of `BondedSR` and decreases the circulation supply of `SR` tokens.
