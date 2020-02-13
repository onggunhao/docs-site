---
id: access
title: Accessing Binance Chain
---

We can access Binance Chain through a few methods:

> For this quickstart, we will be using the [Command Line](../../api-reference/cli) to interact with Binance Chain.

## Access Methods

|                                                           | Description                                                                               | Method           |
| --------------------------------------------------------- | ----------------------------------------------------------------------------------------- | ---------------- |
| [Command Line](../../api-reference/cli)                   | Easy-to-use CLI that calls Web API and Node RPCs                                          | `bnbcli`         |
| [Accelerated Node API](../../api-reference/dex-api/paths) | API calls to our `accelerated node` infrastrcture. This is recommended for most use cases | REST, Websockets |
| [Node RPC](../../api-reference/node-rpc)                  | RPC calls to public seed nodes or to a [full node](../node/fullnode) you run              | RPC Calls        |

## SDKs

Additionally, Binance Chain offers language-specific SDKs that wrap the lower-level RPC calls.

### Official SDKs

| Language   | Link                                                      | Docs                                                         |
| ---------- | --------------------------------------------------------- | ------------------------------------------------------------ |
| Go         | [Github](https://github.com/binance-chain/go-sdk)         | [Docs](https://github.com/binance-chain/go-sdk/wiki)         |
| Java       | [Github](https://github.com/binance-chain/java-sdk)       | [Docs](https://github.com/binance-chain/java-sdk/wiki)       |
| Javascript | [Github](https://github.com/binance-chain/javascript-sdk) | [Docs](https://github.com/binance-chain/javascript-sdk/wiki) |

### Community SDKs

| Language | Link                                                     | Docs                                                                                                   |
| -------- | -------------------------------------------------------- | ------------------------------------------------------------------------------------------------------ |
| C++      | [Github](https://github.com/binance-chain/cplusplus-sdk) | [Docs](https://github.com/binance-chain/cplusplus-sdk/wiki)                                            |
| C#       | [Github](ht;tps://github.com/binance-chain/csharp-sdk)   | [Docs](https://github.com/binance-chain/csharp-sdk)                                                    |
| Python   | [Github](https://github.com/binance-chain/python-sdk)    | [Docs](https://python-binance-chain.readthedocs.io/en/latest/binance-chain.html#module-binance_chain)) |
| Swift    | [Github](https://github.com/binance-chain/swift-sdk)     | [Docs](https://github.com/binance-chain/swift-sdk/blob/master/README.md)                               |

If you are interested in developing new SDKs in other languages (e.g. Rust, Haskell), please contact us directly.

> We will be installing the [Command Line](../../api-reference/cli) in the next step of the Quickstart
