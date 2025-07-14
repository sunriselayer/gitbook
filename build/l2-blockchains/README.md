# Supported L2 SDKs

## Sunrise Documents

- [Rollkit](./rollkit/README.md)
  - [Sunrise Data](./rollkit/sunrise-data.md) - Configure and run the Sunrise DA relay
  - [Rollkit L2 Chain](./rollkit/rollkit.md) - Build and deploy a Rollkit-based L2
- [Optimism OP Stack](./optimism/README.md)
  - [Sunrise Data](./optimism/sunrise-data.md) - Set up Sunrise DA for OP Stack
  - [OP Stack L2 Chain](./optimism/op-stack.md) - Deploy an OP Stack L2 with Sunrise

## How to create L2

It is recommended to run the full consensus node locally, without relying on an external RPC. This ensures better reliability and control over your L2 deployment.

[Sunrise Consensus Node Document](../../../node/types/consensus/README.md)

### Rollkit

`sunrise-data`, and `rollkit` need to be run. The integration provides:

- Native data availability through Sunrise
- Sovereign rollup capabilities
- Customizable execution environment
- Simple configuration and deployment

### OP Stack

`sunrise-data`, `optimism` and `op-geth` need to be run. Key points:

- The local EVM L1 chain is only used to meet OP Stack requirements
- The actual data (metadata) is stored in Sunrise
- Use Ganache, Hardhat, Anvil or similar for local L1 chain
- Sunrise handles the actual data availability

## Requirements

| Type                    | CPU    | Architecture | Mem   | Disk     | Bandwidth | Purpose |
| ----------------------- | ------ | ------------ | ----- | -------- | --------- | ------- |
| Rollkit + Sunrise Data  | 4 Core | x86_64       | 16 GB | 1 TB SSD | 1 Gbps    | Development and testing |
| OP Stack + Sunrise Data | 6 Core | x86_64       | 32 GB | 1 TB SSD | 1 Gbps    | Production deployment |

Additional considerations:

- SSD should be enterprise-grade for production
- Bandwidth requirements increase with transaction volume
- Memory requirements scale with state size

## Official Document

- [Rollkit](https://rollkit.dev/learn/intro)
  - [BeaconKit (option)](https://rollkit.dev/tutorials/execution/beaconkit): By combining BeaconKit and Rollkit, EVM compatible L2 blockchain is possible to develop.
  - Provides full EVM compatibility while maintaining Sunrise DA benefits
- [OP Stack](https://docs.optimism.io/stack/getting-started)
  - Comprehensive documentation for OP Stack deployment
  - Integration guides for various components

## Integration Architecture

```
┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐
│                 │     │                 │     │                 │
│  L2 Blockchain  │────▶│  Sunrise DA     │────▶│  Validator      │
│                 │     │  Layer          │     │  Network        │
└─────────────────┘     └─────────────────┘     └─────────────────┘
        │                       │                       ▲
        │                       │                       │
        ▼                       ▼                       │
┌─────────────────┐     ┌─────────────────┐             │
│                 │     │                 │             │
│  User           │     │  DA Proof       │─────────────┘
│  Applications   │     │  Verification   │
└─────────────────┘     └─────────────────┘
```

## Common Integration Steps

1. **Setup Sunrise DA Node**
   - Deploy a Sunrise node or connect to the testnet
   - Configure network parameters
   - Set up validator if needed
   - Verify node synchronization

2. **Configure L2 Framework**
   - Install required dependencies
   - Set up configuration files
   - Connect to Sunrise DA layer
   - Configure network parameters

3. **Implement DA Integration**
   - Configure blob submission
   - Set up proof verification
   - Implement fee handling
   - Set up monitoring

4. **Testing and Deployment**
   - Test on testnet
   - Verify DA proofs
   - Deploy to production
   - Monitor performance

## Configuration Examples

### Rollkit Configuration

```yaml
[da]
rpc_address = "http://localhost:26657"
fee_denom   = "uusdrise"
gas_price   = "0.025"

[rollup]
chain_id = "my-rollup-1"
```

### OP Stack Configuration

```bash
# Environment variables
DA_SERVER=http://localhost:8547
BLOB_RPC=http://localhost:26657
```

## Best Practices

1. **Security**
   - Always verify DA proofs
   - Use secure RPC endpoints
   - Implement proper error handling
   - Regular security audits

2. **Performance**
   - Optimize blob sizes
   - Implement proper caching
   - Monitor gas costs
   - Regular performance testing

3. **Reliability**
   - Implement retry mechanisms
   - Monitor DA proof status
   - Set up proper logging
   - Regular backups

## Troubleshooting

| Issue | Solution | Prevention |
|-------|----------|------------|
| DA proofs not verifying | Check RPC connection and proof format | Regular connection testing |
| High gas costs | Optimize blob size and frequency | Monitor and adjust gas settings |
| Connection issues | Verify network configuration and firewall settings | Regular network monitoring |

## Additional Resources

- [Rollkit Documentation](rollkit/README.md)
- [OP Stack Integration](optimism/README.md)
- [Data Availability Proofs](/build/validators/data-availability-proof.md)
- [Fee Abstraction](/learn/sunrise/fee-abstraction.md)
