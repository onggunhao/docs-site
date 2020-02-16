---
id: access
title: Accessing Binance Chain
---

Binance Chain can be accessed by interacting with a node in the distributed network. This can be to a self-run node, or to a public node provider.

> For this quickstart, we will be using the beginner-friendly [Command Line](../../api-reference/cli) to interact with Binance Chain.

## Access Methods

### Direct Node Access

This is the most basic way to interact with a node. You can choose to run your own [full node](../node/fullnode) or leverage on public nodes provided by the Accelerated Node network.

> The Accelerated Node network consists of several accelerated nodes run by different organizations around the world, and offer accelerated transaction routing

|                                                               | Description                                                                                | Method                           |
| ------------------------------------------------------------- | ------------------------------------------------------------------------------------------ | -------------------------------- |
| [Accelerated Node Network](../../api-reference/dex-api/paths) | API calls to our `accelerated node` infrastructure. This is recommended for most use cases | REST, Websockets                 |
| [Node RPC](../../api-reference/node-rpc)                      | RPC calls to public seed nodes or to a [full node](../node/fullnode) you run               | RPC Calls, Websocket, API Server |

### CLI and SDKs

We provide CLI and SDKs that wrap lower-level API calls to the Accelerated Node API and Node RPC. This allows developers to work at a higher level of abstraction.

|                                         | Description                                                        | Method            |
| --------------------------------------- | ------------------------------------------------------------------ | ----------------- |
| [Command Line](../../api-reference/cli) | CLI that calls Web API and Node RPCs                               | `bnbcli`          |
| [SDKs](../../api-reference/node-rpc)    | Language-specific wrappers for Accelerated Node APIs and Node RPCs | Language-specific |

## Install CLI

### Installer Script

We have a community-maintained installer script (`install.sh`) that helps to install and configure your access to Binance Chain. This installs:

- `bnbcli`: CLI to access Binance Chain

In addition to the CLI, the installer script also installs the binaries required to run a full or light node. We will not be using them in this quickstart.

- `bnbchaind`: Allows you to run a [full node](../node/fullnode)
- `lightd`: Allows you to run a [light node](../node/lightnode)

```shell
# One-line install
sh <(wget -qO- https://raw.githubusercontent.com/binance-chain/node-binary/compress/install.sh)
```

> In the future, we may release an official installer script  
> e.g. `sh <(wget -qO- https://get.binance.org)

### Manual Installation

You can obtain the Binance Chain executables directly from our [Github repo](https://github.com/binance-chain/node-binary).

#### Clone Repo

```shell
git clone https://github.com/binance-chain/node-binary.git
```

#### Find version of CLI

The repo is organized by network type, and then by version. To find the version of the CLI you want to use, `cd` into the correct directory:

```shell
cd node-binary/cli/{network}/{version}
```

#### (Optional) Copy to PATH

You can add the `bnbcli` executable to a folder your \$PATH (e.g. `/usr/local/bin` on \*nix systems)

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
