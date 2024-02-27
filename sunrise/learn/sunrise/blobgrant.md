# BlobGrant

Sunrise accepts any token for Data Availability (DA) fee. This feature is called BlobGrant.

## How it works

Gluon, a Sovereign rollup Layer 2 of Sunrise serves a functionality to stake any token via IBC interoperability. By submitting the proof via IBC from Gluon to Sunrise that the token is correctly locked in Gluon, Sunrise will permit the L2 operator to post Blob Tx until consuming a certain amount of gas.

The locked funds in Gluon will be finally released for Sunrise validators as an IBC bridged token after the vesting period.
