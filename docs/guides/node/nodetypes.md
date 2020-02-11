---
id: nodetypes
title: Types of Nodes
---

## Node Roles

### What is a Validator Node?

Validators are a group/IT infrastructure that take the responsibility to maintain the Binance
Chain/DEX data and validate all the transactions. They join the consensus procedure and
vote to produce blocks. The fees are collected and distributed among all validators.
You can consider Validator as "miner" in Bitcoin and Ethereum and similar concepts exist in dPoS
blockchain as EOS or dBFT in NEO. The initial validators are selected from trusted members of the
Binance community, and will eventually expand to more members as the Binance blockchain and
ecosystem matures, this responsibility will be distributed. The decentralized governance procedure
will be introduced and executed. More qualified organization/individual can become Validators.

### What is a Witness Node?

Witness nodes represent the majority of nodes in a Binance Chain deployment. Although they do not join the consensus process
and produce blocks, they take care of:

- The witness consensus process.
- They serve as data replicas and help to propagate the chain state around the network.
- They receive transactions and broadcast them to all other nodes including Validator nodes.

### What is an Accelerated Node?

Please check [here](faq.md#what-is-the-accelerated-node).

For testnet, there are 2 accelerated nodes setup as below. API users should try to use them directly.

- `testnet-dex-atlantic.binance.org`
- `testnet-dex-asiapacific.binance.org`

For mainnet, there are more accelerated nodes.

- `dex-atlantic.binance.org`
- `dex-asiapacific.binance.org`
- `dex-european.binance.org`

### Full Nodes

### Light Nodes
