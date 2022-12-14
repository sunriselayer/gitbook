# UnUniFi Application Plugin

## How to use UnUniFi Application Plugin

[UnUniFi Application (Bubble plugin)](https://bubble.io/plugin/ununifi-application-1661304597546x724719328208093200)

On Bubble App, UnUniFi Application Plugin supports sending transactions and retrieving information related to NFT functions in the UnUniFi blockchain.

This is mainly composed of `API calls` and `Elements`.
`API calls` are used to retrieve information on the blockchain and `Elements` are used to send transactions.

UnUniFi Application Plugin depends on the following projects.

- [cosmos-client-ts](https://github.com/cosmos-client/cosmos-client-ts)
- [ununifi-ts](https://github.com/cosmos-client/ununifi-ts)

The usage ofCosmos SDK Application Plugin is the same; use this to implement the standard Cosmos SDK transactions.

[Cosmos SDK Application (Bubble plugin)](https://bubble.io/plugin/cosmos-sdk-application-1661304565115x325886041951305700)

## How to install

Open your App source page and select `Plugins` in the sidebar.
Install the latest plugin `UnUniFi Application`.

![plugin](https://user-images.githubusercontent.com/29295263/192484786-328707cb-dcef-42a6-9775-e81fe2794650.jpg)

## Elements

Element supports the transmission of transactions to the UnUniFi blockchain.

On `Design` in the sidebar, Add Visual elements `UnUniFi App nftmint` or `UnUniFi App marketplace`.
Set element's properties chain_id, etc. or use default value.

![element](https://user-images.githubusercontent.com/29295263/192485033-926bed7b-7d2e-4186-ba68-d5f7299ade80.jpg)

In `UnUniFi Application`, 2 Elements are available.
`UnUniFi App nftmint` & `UnUniFi App marketplace`

### UnUniFi App nftmint

This element supports the following transactions.

- Create Class
- Mint NFT
- Burn NFT
- Send Class Ownership
- Update Base Token URI
- Update Token Supply Cap

On `Workflow` in the sidebar, add Element Actions and set value: class_id, etc.
Each Element Action issues Events such as `class_created` and update the element's `tx_hash` field when the process is completed.

![element_action](https://user-images.githubusercontent.com/29295263/192485002-d437a91f-873a-460d-9b1e-682244399af9.jpg)

The specification of the transaction sending function requires that users has installed Keplr Chrome Plugin.
Please encourage users to install it.

### UnUniFi App marketplace

This element supports the following transactions.

- List NFT
- Cancel NFT Listing
- Expand Listing Period
- Place Bid
- Cancel Bid
- End NFT Listing
- Pay Full Bid
- Borrow
- Repay
- Mint Stable Coin
- Burn Stable Coin
- Liquidate

The usage is the same as nftmint.

## API calls

API calls support the getting of information from the UnUniFi blockchain.

API calls can be used simply by installing the plugin.
It can be used in the Input Box's Placeholder and other places where Insert dynamic data can be used.

Insert dynamic data > Get data from an external API > UnUniFi NFT - All Listed Classes, etc.
![api_call](https://user-images.githubusercontent.com/29295263/192485077-f7d36900-399b-4f57-b726-9a80ead91890.jpg)

API calls supports the following GET methods in the UnUniFi API.

### NFT Market Module

- All Listed Classes
- All Listed NFTs
- Bidder Bids
- CDPs List
- Listed Class
- All Loans
- Loan
- NFT Bids
- NFT Listing
- NFTmarket Params
- Address' Rewards

### NFT Mint Module

- lass IDs By Name
- Class IDs By Owner
- Class Attributes
- NFT Minter
- NFTmint Params

### Cosmos NFT Module

- Balance by Class
- Classes List
- Class Detail
- NFTs List
- NFT Detail
- Owner by NFT
- Supply by Class
- NFTs List by Owner
