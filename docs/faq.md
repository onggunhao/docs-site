---
id: faq
title: FAQ
---

# Binance Chain FAQ v0.5

- [Binance Chain FAQ v0.5](#binance-chain-faq-v05)
  - [What is Binance Chain, or Binance DEX?](#what-is-binance-chain-or-binance-dex)
  - [What is the design principle of Binance Chain?](#what-is-the-design-principle-of-binance-chain)
  - [What can you do on Binance Chain?](#what-can-you-do-on-binance-chain)
  - [Will Binance Chain introduce more features and transaction types in the future?](#will-binance-chain-introduce-more-features-and-transaction-types-in-the-future)
  - [What is the native coin on Binance Chain?](#what-is-the-native-coin-on-binance-chain)
  - [How can I register on Binance Chain/DEX and start trading?](#how-can-i-register-on-binance-chaindex-and-start-trading)
  - [How can I send orders on Binance DEX?](#how-can-i-send-orders-on-binance-dex)
    - [Order](#order)
    - [What is `Immediate Or Cancel order`?](#what-is-immediate-or-cancel-order)
    - [Match](#match)
    - [Trade](#trade)
    - [What is `Order Expire`?](#what-is-order-expire)
    - [Where can I see my assets and trades?](#where-can-i-see-my-assets-and-trades)
    - [When can I see my order on the blockchain after I send it?](#when-can-i-see-my-order-on-the-blockchain-after-i-send-it)
    - [What is the Fee Structure?](#what-is-the-fee-structure)
  - [Can I see orders/balances of others or can other people see my orders/balances?](#can-i-see-ordersbalances-of-others-or-can-other-people-see-my-ordersbalances)
  - [Information provided through API and their usage](#information-provided-through-api-and-their-usage)
    - [Is there any limit to using the API to send orders or check market data?](#is-there-any-limit-to-using-the-api-to-send-orders-or-check-market-data)
    - [What does Wallet and API cost to use?](#what-does-wallet-and-api-cost-to-use)
    - [What Market Data can I get?](#what-market-data-can-i-get)
    - [What are the tick size and lot size? Are they fixed?](#what-are-the-tick-size-and-lot-size-are-they-fixed)
    - [Are there limits on notional value of an order?](#are-there-limits-on-notional-value-of-an-order)
    - [What is the decimal precision for prices and quantities on Binance Chain/DEX?](#what-is-the-decimal-precision-for-prices-and-quantities-on-binance-chaindex)
  - [I forgot the private key for my address, how can I get it back?](#i-forgot-the-private-key-for-my-address-how-can-i-get-it-back)
  - [My private key got stolen by hackers, how can I recover my assets?](#my-private-key-got-stolen-by-hackers-how-can-i-recover-my-assets)
  - [What is the Accelerated Node?](#what-is-the-accelerated-node)
  - [How can I issue an asset?](#how-can-i-issue-an-asset)
  - [What is the consensus algorithm used on Binance Chain?](#what-is-the-consensus-algorithm-used-on-binance-chain)
  - [Can I run a full node for Binance Chain?](#can-i-run-a-full-node-for-binance-chain)
  - [Does Binance Chain support Smart Contracts?](#does-binance-chain-support-smart-contracts)
  - [How can I transfer tokens, such as Bitcoin, from other block chains onto Binance Chain?](#how-can-i-transfer-tokens-such-as-bitcoin-from-other-block-chains-onto-binance-chain)
  - [How is a trading pair created on Binance DEX?](#how-is-a-trading-pair-created-on-binance-dex)
  - [How would a third-party integrate with Binance Chain and Binance DEX?](#how-would-a-third-party-integrate-with-binance-chain-and-binance-dex)

## What is Binance Chain, or Binance DEX?

Binance Chain is the blockchain initially developed by Binance and community. Binance DEX is the
decentralized exchange module developed on top of the Binance Chain blockchain.

## What is the design principle of Binance Chain?

The main focuses for the design of Binance Chain are:

- No custody of funds: traders maintain control of their private keys and funds.
- High performance: low latency, high throughput for a large user base, and high liquidity trading.
  We target to achieve 1 second block times, with 1 confirmation finality.
- Low cost: in both fees and liquidity cost.
- Easy user experience: as friendly as Binance.com.
- Fair trading: minimize front-running, to the extent possible.
- Evolvable: able to develop with forever-improving technology stack, architecture, and ideas.

## What can you do on Binance Chain?

You can:

- Send and receive BNB
- Issue new tokens
- Send, receive, burn/mint and freeze/unfreeze tokens
- Propose to create trading pairs between two different tokens
- Send orders to buy or sell assets through trading pairs created on the chain

## Will Binance Chain introduce more features and transaction types in the future?

Yes, Binance Chain team and community would cherish the technology advancements and recommended trends and strive to make circulation of assets and value easier and easier.

## What is the native coin on Binance Chain?

The Binance Coin, BNB, is the native asset on Binance Chain. There are 200MM BNB coins in total.
There will be no mining. The existing coin burns and freezes will still be in effect on the new
Binance Chain blockchain.

The exact number of BNB coins will be destroyed based on the same number of BNB ERC20 tokens
that have already been destroyed.

Since Binance Chain is live, all BNB ERC20 tokens will be swapped for Binance Chain coins. All
users who hold BNB ERC20 tokens can deposit them to Binance.com, and upon withdrawal, the new
Binance Chain native coins will be sent to their new wallets.

## How can I register on Binance Chain/DEX and start trading?

There is no need to register. All you need is a Binance Chain address, which can be generated with
any [wallet](./wallets.md) that supports Binance Chain. Then you can trade BNB or other assets stored on that address.

## How can I send orders on Binance DEX?

### Order

On Binance DEX, you can send "new order" messages to buy or sell certain assets. You can also
send "cancel" messages to cancel existing open orders.

You can use a wallet to send new orders and cancels. Binance DEX also provides API for automated trading.

In Binance DEX v1.0, the order message contains:

- Symbol: trading pair on the chain
- Side: buy or sell
- Price: only limit price orders are supported in Binance Chain v1.0
- Amount
- Time In Force: Binance DEX supports `Immediate Or Cancel` (IOC) and `Good Till Expiry` (GTE)
  orders. GTE orders can quote on the exchange until they are filled by the opposite orders satisfying
  the limit price, or canceled by client themselves, or expire after 72 hours after 00:00 (UTC).
  Check the "What is `Order Expire`" section of the FAQ for more information.

Network nodes examine orders to ensure they are valid. Once the orders are accepted, they are
booked on the next block, and get matched accordingly.

### What is `Immediate Or Cancel order`?

Immediate Or Cancel is a special order type. Once the order is accepted into a block, Immediate Or
Cancel orders only exist in this block round. The order may get filled to zero, or partially or fully
filled by other orders, and then will become expired and removed from the order book right away.
As a result, it will not be tradable in the next round of matching. A small fee will be charged
for the network usage, if there is no fill at all for the order (deemed as no intention to trade).

### Match

Binance DEX does all of its matching on the blockchain, i.e. all nodes perform the matches and
expect the same result. This is to ensure the maximum transparency and to mitigate the chance
for front-running, even from the block producers. The matching infrastructure is expected to
evolve and grow in capacity as time progresses.

Binance DEX doesn't do continuous matching as most centralized exchanges do. Instead, it matches
using periodic auction matching for all the existing open orders received in the past and the
latest blocks. The match logic is explained in more detail later.

### Trade

Once the orders are filled, the corresponding assets will be automatically moved into buyers'
addresses. The confirmation is instant and no need to wait for further blocks (i.e. T+0 block).
Buyers can use the bought asset right away, either send it to another address or trade it again.

### What is `Order Expire`?

Orders accepted by Binance DEX will either get filled with other orders or remain in the order book,
but they will not stay on the order book forever. These orders will expire and be removed from the
order book after the 1st midnight (UTC) after 72 hours once the order gets accepted. A small fee
will be charged for the network usage, if there is no fill at all for the order (deemed as no intention to trade).

### Where can I see my assets and trades?

You can always use wallets that support Binance Chain to check your asset balances, open orders,
and (optionally) order/trade history. Binance Chain Explorer is another tool to check balances
and transactions.

### When can I see my order on the blockchain after I send it?

It depends. Normally, if you connect to one of the Accelerated Nodes, your orders should get
accepted and booked into a block in 1-3 seconds. If the order price is marketable, the order
will be filled and trades will come back in about similar time. If you send the order from far-way
(self-setup full node), or there is heavy network traffic, the order may take longer to reach
a Validator (block producer).

### What is the Fee Structure?

Fees are charged and shared among the block producers (i.e. Validators) to run the network,
in order to pay for the network usage and prevent abuse and attack. Since all user transactions,
include transfer, new order, cancel etc, they are all recorded in blocks and chain state, the fee will be
shared among different transactions. New orders are exempt from fees to encourage usage and larger
trades will be charged more for their benefits from the liquidity provided in the network.
Order Expire and Cancel are also charged with a fee if they fail to provide any liquidity. The current fee table is [here](./trading-spec.md)

Besides the fees, **no other gas will be charged.**

Fees can be paid in any asset, but the network will charge BNB first and apply a discount if the
address has BNB balance.

The fee is subject to periodical review and adjustment, after agreement from validators, via a
proposal-vote procedure. See a fee-change proposal [here](https://explorer.binance.org/tx/B1E78D8275598CB0538C716997EEDD2F1198B82F4D73959C5BF69CBAF4281240)

- Trade fee is calculated based on trade notional value, while fees for other transactions are fixed.
- It is free to send a new GET order, cancel a partially filled order, or expire a partially filled order.
- Non-Trade related transactions will be charged with a fee when the transactions happen, and can
  only be paid in BNB. The transaction will be rejected if the address does not have enough BNB.
- Trade-related transactions will be charged with a fee when an order is filled, or
  canceled/expired/IOC-expired with no fills. If there is enough BNB to pay, BNB fee structure will
  be used, otherwise, non-BNB fee structure will be used instead.
- If the whole order value and free balance for the receiving asset are not enough to pay the fee,
  all the receiving asset and its residual balance will be charged.

## Can I see orders/balances of others or can other people see my orders/balances?

Yes, anyone can see anyone's orders and balances if they know the corresponding addresses.
Binance Chain is 100% transparent for transactions and balances.

## Information provided through API and their usage

### Is there any limit to using the API to send orders or check market data?

Yes, there are rate limits to ensure there is no waste or abuse of the network infrastructure.<br/>
Please check the API documentation.

### What does Wallet and API cost to use?

No fee or commission at all (free to use).

### What Market Data can I get?

The market data provided via Wallet and API are similar to Binance.com, including ticker data, order book,
trade and Kline. They can be seen in the Wallet and read from REST or WebSocket API.<br/>
Please check the API documentation for details.

### What are the tick size and lot size? Are they fixed?

Tick size is the minimum unit to increase or decrease for the price (in quote asset) of an order,
while lot size is the minimum unit to increase or decrease for the quantity (in base asset) of an order.<br/>
They are not the same as on Binance.com. They can be queried from API or checked from Wallet UI.

Tick Size and lot size are not fixed. Binance Chain will automatically/periodically review the values to make
sure proper order size and notional is applied.

### Are there limits on notional value of an order?

The smallest order you can send for a trading pair is 1 lot size quantity at 1 tick size price. No other limits.

### What is the decimal precision for prices and quantities on Binance Chain/DEX?

Amounts are represented as integers, and all coins have a fixed scale of 8.<br/>
This means that if a balance of 100000000 were to be exposed to a wallet integrator, this will represent a balance of 1 coin.

## I forgot the private key for my address, how can I get it back?

Sorry, you cannot. Owner of the address takes full responsibility for the private key protection.
Binance Chain and official wallets do not have your private key.

## My private key got stolen by hackers, how can I recover my assets?

Sorry, you take full responsibility of your private key ownership and protection. Binance Chain
and official wallets will not record, or transfer out your private key.

## What is the Accelerated Node?

While users can submit transactions and most of the queries via normal, self-run full nodes.<br/>
Accelerated Node provides more secure and faster lines to access Binance Chain.

Accelerated Node is special infrastructure built around Validator to facilitate accelerated transaction
routing and provide richer, faster user interfaces. There are always several Accelerated Nodes running
at the same time around the world (owned by different organizations) and you are encouraged to choose
one of them to use, or allow your Wallet choose one randomly.<br/>
For rapid API access, you'd better stay with one Accelerated Node to get better performance.

## How can I issue an asset?

Anyone can pay a fee and issue an asset as Token on Binance Chain, as long as they provide
proper information for the fields below, and then execute the command through the command line or http interfaces.

- Name: a description string of less than 21 characters
- Symbol: an identifier string less than 9 characters, which must be composed of [0-9A-Z]
- Total Supply: a positive number less than or equal to 90 billions
- Mint-able: whether the token can increase Total Supply in later time or not

## What is the consensus algorithm used on Binance Chain?

Binance Chain uses BFT and PoS (upcoming) based consensus mechanism to produce blocks among
a series of qualified Validators. This is similar to the architectures of several existing
popular blockchain platforms such as EOS and NEO.
The process for setting up validators among different entities on Binance Chain is currently being defined. More details will be shared at a later date.

## Can I run a full node for Binance Chain?

Yes, you can. A full node contains all the information and application logic for Binance Chain.
It can receive and broadcast blocks and transactions with other full nodes and even validators.
The only exception is it will not participate in the consensus if the full node is not a Validator.

## Does Binance Chain support Smart Contracts?

No. This was an intentional design decision to improve the performance of the system and eliminate
having to support unnecessary features.

If you have certain must-have feature-s, it might be added as a native implementation instead of using smart contract.<br/>
Feel free to talk to Binance community.

## How can I transfer tokens, such as Bitcoin, from other block chains onto Binance Chain?

Right now, there are 2 ways to transfer tokens cross-chain:

1. via interoperability among different chains. After the latest “Archimedes” upgrade, [BEP3](https://github.com/binance-chain/BEPs/blob/master/BEP3.md) was introduced and it defines native transactions to support [Hash Timelock Contract (HTLC)](https://en.bitcoin.it/wiki/Hash_Time_Locked_Contracts) on Binance Chain and it also to defines the infrastructure standard and procedure to use HTLC for inter-chain [atomic swap](https://www.binance.vision/blockchain/atomic-swaps-explained) to easily swap tokens on different chains. Binance Chain development community has finished implementing its solution for BEP3 with BEP2 and ERC20 tokens and decided to open-source all of the key components, including：

- [smart-contract solution](https://github.com/binance-chain/bep3-smartcontracts) that supports Atomic Peg Swap (APS) for Ethereum. Please note that this solution is already audited by 3rd party.
- [deputy process](https://github.com/binance-chain/bep3-deputy) written in GoLang that handles swap activities

Any developer is welcome to test the solutions in testnet and then use them in mainnet.

2. via Binance.com. [Binance](binance.com),the largest cryptocurrency exchange, has issued a number of crypto-pegged tokens on Binance Chain (BEP2 token format): [BEP2 Bitcoin](https://explorer.binance.org/asset/BTCB-1DE), [BEP2 BCH](https://explorer.binance.org/asset/BCH-1FD),[BEP2 XRP](https://explorer.binance.org/asset/XRP-BF2), [BEP2 LTC](https://explorer.binance.org/asset/LTC-F07). Pegged tokens such as [BEP2 Bitcoin](https://explorer.binance.org/asset/BTCB-1DE), are 100% backed by the native coin in [reserve](https://btc.com/3LYJfcfHPXYJreMsASk2jkn69LWEYKzexb). The reserve addresses are published for anyone to audit. Read this [blog](https://www.binance.com/en/blog/347360878904684544/Introducing-BitcoinPegged-Token-on-Binance-Chain) to learn about the reserved address. Users are free to convert between native and BEP2 Bitcoin via deposit/withdrawal. This has a higher degree of ease-of-use for most traders. More swap channels will be provided on partner wallets soon.

Atomic swap and this centralized approach are not exclusive to other decentralized approaches, which can also be implemented in parallel. There are many cross-chain solutions being developed and we are very interested in them.

Please do **NOT** try to transfer anything on existing network to Binance Chain testnet, you may experience loss by doing so, because testnet doesn't run with real coins.

## How is a trading pair created on Binance DEX?

The design philosophy of Binance DEX adheres to the idea that the most efficient and low cost way to perform trading and
price-discovery is still to use single order book. This single order book is managed and replicated across all
full nodes with the same, deterministic matching logic.

Simply allowing trading between two assets seems easy enough, however it is expensive for not only the network
but also its users in long term (and liquidity costs can be much larger). In order to efficiently use the
network, Binance Chain only list assets against BNB and other widely accepted market quote assets.

After an asset is issued, which costs a small fee,
anyone can "propose" to all validators to list it against particular quote assets.
Validators then vote to accept the proposal.
A deposit is taken to prevent network abuse.
Once the proposal is accepted, the owner of the base asset can list the trading pair.

For more information about this process please check the [listing guide](list.md).

## How would a third-party integrate with Binance Chain and Binance DEX?

A wallet provider may choose to only support the feature set of Binance Chain, which would just
cover wallets, addresses, balances and transfers.<br/>
To improve their implementation further, they could choose to integrate Binance DEX which would add trading (order placement and cancellation), historical order and trade views, charts, etc.
