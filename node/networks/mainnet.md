# Sunrise Mainnet

The main network of Sunrise. Use tokens with real value.

{% hint style="warning" %}
**IMPORTANT**: This network is currently in the process of being launched.
{% endhint %}

## Mainnet Details

[sunrise-1 Network Details](https://github.com/sunriselayer/network/tree/main/sunrise-1)

| Detail | Value                                        |
| ------ | -------------------------------------------- |
| RPC    | Coming soon                        |
| REST   | Coming soon                         |

## Frontend

| Name                | URL                                           |
| ------------------- | --------------------------------------------- |
| APP (Tx Portal)     | Coming soon                           |
| Risescan (Explorer) | Coming soon                      |

## Mainnet Software

Please check our proposals and community. See [sunrise-1](https://github.com/sunriselayer/network/tree/main/sunrise-1) for setup.
The genesis binary is `v1.0.0`.

[Released Binary](https://github.com/sunriselayer/sunrise/releases)

## IBC Config

| Dst Chain  | Dst Port   | Dst Channel   | Src Chain           | Src Port   | Src Channel |
| ---------- | ---------- | ------------- | ------------------- | ---------- | ----------- |
| `cosmoshub-4` | `transfer` | | `sunrise-1` | `transfer` | |
| `noble-1`  | `transfer` |  | `sunrise-1` | `transfer` |  |
