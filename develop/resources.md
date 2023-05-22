# Resource

## Mainnet

Frontend Application: <https://ununifi.io>

- Explorer
  <https://ununifi.io/explorer>
  Blockchain explorer for UnUniFi
- Portal
  <https://ununifi.io/portal>
  Wallet & DeFi Application for UnUniFi

### Public LCD

UnUniFi Rest API
Download OpenAPI specification: [swagger.yaml](https://github.com/UnUniFi/chain/blob/main/docs/client/swagger.yaml)

Cosmos SDK Rest & gRPC Gateway: [v1.cosmos.network](https://v1.cosmos.network/rpc)

| Endpoint                      | Network         | Chain ID        |
| ----------------------------- | --------------- | --------------- |
| **a.lcd.ununifi.cauchye.net** | UnUniFi mainnet | ununifi-beta-v1 |
| **b.lcd.ununifi.cauchye.net** | UnUniFi mainnet | ununifi-beta-v1 |

### Available Ports

| Port                 | Function                          |
| -------------------- | --------------------------------- |
| 9090                 | gRPC server                       |
| 1317 (https: 1318)   | REST server                       |
| 26657 (https: 26658) | CometBFT RPC endpoint (websocket) |

## Testnet

There are currently 3 public testnet chains.

- Testnet
  For mainnet development
  <https://test.ununifi.io/>
- Lab
  Includes features planned for next release
  <https://lab-testnet.ununifi.io/>
- Alpha
  Includes unstable and up-to-date features
  <https://alpha-test.ununifi.io/>

All testnets have Explorer & Portal.

| Endpoint                           | Network         | chain ID           |
| ---------------------------------- | --------------- | ------------------ |
| **a.ununifi-test-v1.cauchye.net**  | UnUniFi Testnet | ununifi-test-v1    |
| **b.ununifi-test-v1.cauchye.net**  | UnUniFi Testnet | ununifi-test-v1    |
| **c.ununifi-test-v1.cauchye.net**  | UnUniFi Testnet | ununifi-test-v1    |
| **d.ununifi-test-v1.cauchye.net**  | UnUniFi Testnet | ununifi-test-v1    |
| **ununifi-beta-test.cauchye.net**  | UnUniFi Lab     | ununifi-beta       |
| **ununifi-alpha-test.cauchye.net** | UnUniFi Alpha   | ununifi-alpha-test |

### Available Ports (Testnet)

| Port                 | Function                          |
| -------------------- | --------------------------------- |
| 9090                 | gRPC server                       |
| 1317 (https: 1318)   | REST server                       |
| 26657 (https: 26658) | CometBFT RPC endpoint (websocket) |
| 8000 (https: 8001)   | Faucet for BTC                    |
| 8002 (https: 8003)   | Faucet for GUU & USDC             |
