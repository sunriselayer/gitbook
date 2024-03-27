# Interoperability

Sovereign rollup is a new type of Layer 2 solution that is different from conventional Smart contract rollup.

In the conventional Smart contract rollup, there is an "enshrined bridge" that enables users to bridge their tokens between L1 settlement layer and L2 execution layer. The role of verifying the validity of the bridge is played by the rollup contract. So this bridge is called "enshrined."

On the other hand, Sovereign rollup has no enshrined bridge. The sovereign rollup side plays a role in verifying the validity of the bridge. With this architecture, Sovereign rollup has a flexible space to design the bridges or interoperability. In concrete, Sovereign rollup can support IBC (Inter Blockchain Communication) interoperability.

At this moment, these SDKs are known to support the IBC of Sovereign rollup:

* Rollkit
* Sovereign SDK
