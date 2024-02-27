# App chain thesis

In the IBC (Inter Blockchain Communication) ecosystem, the concept of "app chain thesis" has been proposed.
The core idea is that by building a Layer 1 blockchain for each dApp and then connecting them by using IBC interoperability, we can achieve a scalable and secure blockchain ecosystem.

Let's rename this "Monolithic app chain thesis".

However, there is one weakness in the app chain thesis.
Because it requires to gather the validators set for each app chain, the load of the core team of the app chain is heavy.
This is called "validator bootstrapping problem".

Due to this weakness, IBC ecosystem has grown but hasn't reached the level IBC ecosystem predicted.

Now, there is a modular blockchain paradigm that can solve the validator bootstrapping problem when we build an app specific blockchain.

By using Sovereign rollup technology, we can build a blockchain that is compatible with the IBC ecosystem and can solve the validator bootstrapping problem at the same time.

We call this "Modular app chain thesis".

## Smart contract is not the only way to build a dApp

We think that we can express a metaphor of ways of building dApps:

|||
|---|---|
| Smart contract | Shared server |
| Modular app specific chain | Virtual private server |
| Monolithic app specific chain | Dedicated server |

Smart contracts are often affected with the traffic of other dApps. This is like a shared server.
On the other hand, monolithic app specific chains are like dedicated servers. They are not affected with the traffic of other dApps, but they are expensive to bootstrap validators.

Modular app specific chains are like virtual private servers. They are almost not affected with the traffic of other dApps, and they are not expensive to bootstrap validators.

As VPS grew to IaaS, Raas (Rollup as a Service) will grow and allow us to build a scalable and secure blockchain ecosystem as easy as deploying smart contracts.
