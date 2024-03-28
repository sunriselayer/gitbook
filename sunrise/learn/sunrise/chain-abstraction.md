# Chain Abstraction

By using `abstractaccount` module that realizes the account abstraction and is integrated into Sunrise, and Interchain Account technology, Sunrise will serve the novel mechanism of chain abstraction. With this mechanism, any Layer 2 solutions can serve a better UX than ever like using a single blockchain with other blockchains to end users.

## What is Account Abstraction?

Account Abstraction is the method to release the restriction of validating the permission of accounts in the blockchain. Conventionally, transactions on the blockchain can be emitted only by EOA that is linked to the specific private key and public key with digital signature technology. However, by introducing account abstraction, transactions can be emitted by any contract accounts or module accounts that are linked to specific credentials.

Credentials can be anything. The zero-knowledge proof of something, credentials of Google / Apple / Microsoft account signing in, and so on.

## What is Interchain Account?

Interchain Account is the technology to operate the account of the external blockchain remotely by using IBC (inter blockchain communication) interoperability. Any blockchains that support IBC (not only Cosmos SDK blockchains but also Ethereum L2s supported by Polymer or EVM chains that integrate IBC Solidity) can be the host chain of Interchain Account with the Interchain Account controller on Sunrise. It is not restricted only to Sovereign rollups on Sunrise.

## The combination of Account abstraction and Interchain Account

Sunrise integrates Account Abstraction and Sunrise can be Interchain Account controller for any blockchains that support IBC. It means that accounts on any blockchains that support IBC can be operated by using customized authentication methods with specific credential that is not only digital signature verification.

If the issuers of the credential need to post that credential into Blob space on Sunrise, they can do so. Sunrise DA is also a hub of chain abstraction with a customized authentication method.

Projects in the modular ecosystem like Celestia and Avail are trying to make the deployment of chains as easy as deploying smart contracts. By using Chain Abstraction technology of Sunrise, we will make the usage of modular chains as easy as using monolithic blockchain and web2 applications from the point of view of users.
