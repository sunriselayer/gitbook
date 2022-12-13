# How to use UnUniFi Plugin

If you are not knowledgeable about Cosmos blockchain transactions, please use the UnUniFi Application Plugin.

UnUniFi Plugin is a single-function plugin that only creates messages for UnUniFi transactions.

Two additional plugins are required to send transactions.

- Cosmos SDK Tx Basis Plugin
- Keplr Plugin

## How to install

Open your App source page and select `Plugins` in the sidebar.
Install the latest plugin `UnUniFi (not Application)`, `Cosmos SDK Tx Basis` & `Keplr`.

**Please uninstall UnUniFi Application Plugin. These cannot be used together.**

## Settings

First, Add Plugin's Element to your App and set some parameters.

Second, in Keplr Element, enter information about the chain to be connected.

![keplr-param](https://user-images.githubusercontent.com/29295263/207234030-2b091324-5bdc-456a-beef-a8b0cfee0156.png)

Next, in Cosmos Tx Basis Element, enter same infomation as Keplr and Keplr Element's `public_key` & `address`. Also, set any `log_level`.

![basis-param](https://user-images.githubusercontent.com/29295263/207233991-fffabe9f-2895-400f-9c3f-42a80b49ece2.png)

The Elment that creates Msgs sets only Keplr Plugin's `address`.

![element-param](https://user-images.githubusercontent.com/29295263/207234557-fbcdeaa1-a76d-4673-8b98-0d5580528831.png)

Set the Element containing the Msg you wish to use. Msgs supported by each Element are show in later chapters.

## Workflow

After setting, set up `Workflow` for transaction submission.

First, trigger the button, etc., up to the creation of Msg by UnUniFi Plugin. Set `login` by Keplr & `create_msg_xxx` by UnUniFi Plugin.

![workflow](https://user-images.githubusercontent.com/29295263/207235735-485a9eda-46f1-4ff6-9123-78dc70643ae1.png)

Second, Set up two actions when `msg_xxx_created` event, `set_msg` & `create_tx` by Cosmos SDK Tx Basis Plugin.
In `set_msg`, `type_url` & `value` are needed to set. Set from UnUniFi Plugin Element.

![workflow-msg](https://user-images.githubusercontent.com/29295263/207236967-1c375802-770c-48f0-a9ca-42b476eaf6ac.png)

Third, add signature in Keplr. set `sign` by Keplr when `tx_created` event. Set `authInfoHex`, `accountNumString` & `bodyHex` from Cosmos SDK Tx Basis Element.

![workflow-keplr](https://user-images.githubusercontent.com/29295263/207237537-24d216e0-1018-41d5-9d32-d47d4e1ce924.png)

Finally, broadcast transaction. use `broadcast_tx` by Cosmos SDK Tx Basis when `sined` event. Set `signed_body_hex`, `signed_auth_info_hex` & `signature` from Keplr Element.

![workflow-broadcast](https://user-images.githubusercontent.com/29295263/207237640-ebb0d582-3a30-4ce1-9714-462af5d2c99a.png)

If it works like this, you are done.
A Keplr window will open and ask you to sign it.
The Tx Hash can be obtained from the Cosmos SDK Tx Basis Plugin.

![page](https://user-images.githubusercontent.com/29295263/207239127-f2569950-49af-4880-bf59-1a7e4c3b734c.png)

## Plugins for Msg creation

A dedicated Plugin is used to create Msg for each transaction.
Each plugin also includes a REST API for GET as an `API Call`.

### UnUniFi

#### UnUniFi Marketplace Element

- MsgListNft
- MsgCancelNftListing
- MsgEndNftListing
- MsgExpandListingPeriod
- MsgPlaceBid
- MsgCancelBid
- MsgPayFullBid
- MsgBorrow
- MsgRepay
- MsgLiquidate
- MsgMintStableCoin
- MsgBurnStableCoin
- MsgSellingDecision

#### UnUniFi NFT mint Element

- MsgCreateClass
- MsgMintNFT
- MsgBurnNFT
- MsgSendClassOwnership
- MsgUpdateBaseTokenUri
- MsgUpdateTokenSupplyCap

### Cosmos SDK Bank

Cosmos SDK Standard Msgs can be used as well as the UnUniFi Plugin.

- MsgSend

### Cosmos SDK Staking

- MsgDelegate
- MsgRedelegate
- MsUndelegate

### Cosmos SDK Distribution

- MsgWithdrawDelegatorReward
- MsgWithdrawValidatorCommission

### Cosmos SDK Gov

- MsgVote
- MsgDeposit
