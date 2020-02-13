---
id: install
title: Install CLI
---

Our Quickstart will be using the Command Line Interface to interact with Binance Chain. Here's how to install it to your system.

## Installer Script

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
