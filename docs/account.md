---
id: accounts
title: Accounts
---

An `Account` on Binance Chain consists of:

| Key             | Description                                            |
| --------------- | ------------------------------------------------------ |
| Public key      | Derived from user's private key / seed phrase          |
| Address         |                                                        |
| Account Number  | A unique number for each account                       |
| Sequence Number | For replay proection. Similar to _nonce_ in ethereum   |
| Asset balances  | Consists of `available`, `locked`, and `frozen` assets |

- _Locked_ assets are in an outstanding order. Once the order terminates (filled, cancelled, expired), the assets will be unlocked.

- _Frozen_ assets are frozen via [freeze transactions]().

## Create an Account

You can also create a new key and you will get a new mnemonic with `bnbcli` or `tbnbcli`.

<!--DOCUSAURUS_CODE_TABS-->
<!--Mainnet-->

```bash
$ ./bnbcli keys add new_key
```

<!--Testnet-->

```bash
$ ./tbnbcli keys add new_key
```

<!--END_DOCUSAURUS_CODE_TABS-->

> Remember to save your mnemonic in a safe place!

This should guide you through an interactive prompt to create your account.

```
Enter a passphrase for your key:
Repeat the passphrase:
NAME:	TYPE:	ADDRESS:						PUBKEY:
new_key	local	bnb1c5dxrdn9xuw0njwcyevzyjrza550z5au8v0hyz	bnbp1addwnpepqwdsud63f5rq2wkgrezlvzdauf4x7wp3defzvhrzkwdzl7p0n6uk666ghpa
**Important** write this seed phrase in a safe place.
It is the only way to recover your account if you ever forget your password.

napkin degree boring custom differ smart bundle ball length lyrics auto forest jeans awake entry vocal there repeat rule churn picnic promote screen skull
```

## Restoring an Account

You can restore your account using your seed phrase mnemonic.

<!--DOCUSAURUS_CODE_TABS-->
<!--Mainnet-->

```bash
$ ./bnbcli keys add test --recover
```

<!--Testnet-->

```bash
$ ./tbnbcli keys add test --recover
```

<!--END_DOCUSAURUS_CODE_TABS-->

This should guide you through an interactive prompt to restore your account.

```
Enter a passphrase for your key:
Repeat the passphrase:
> Enter your recovery seed phrase:
more advice achieve mass clap nose bike bird busy section rigid model doll exchange guard theme catalog junior patrol valley depart decade convince master
NAME:	TYPE:	ADDRESS:						PUBKEY:
test	local	tbnb14m2gcdjq7aqkdtu2m9qrqrl8eevzpqfj9xc0uu	bnbp1addwnpepqt7nf2dwgfxv6kmzgwhzlp556yhdfeakfdejc6lp8xcddsv83kq552m63s9
```

## Query Account Balance

You can query the account info with the following command on mainnet:

<!--DOCUSAURUS_CODE_TABS-->
<!--Mainnet-->

```bash
$ bnbcli account <your-address>
    --chain-id Binance-Chain-Tigris # mainnet
    --node https://dataseed5.defibit.io:443
    --indent
    --trust-node  # skips querying proofs (i.e. faster)
```

<!--Testnet-->

```bash
$ tbnbcli account <your-address>
    --chain-id Binance-Chain-Nile # testnet
    --node data-seed-pre-2-s1.binance.org:80
    --indent
    --trust-node  # skips querying proofs (i.e. faster)
```

<!--END_DOCUSAURUS_CODE_TABS-->

> Note: amounts in Binance Chain are unsigned integers, shifted by **10^8** to represent decimals

A `json` of the following structure will be returned.

```json
{
  "type": "bnbchain/Account",
  "value": {
    "base": {
      "address": "tbnb1sylyjw032eajr9cyllp26n04300qzzre38qyv5",
      "coins": [
        { "denom": "000-0E1", "amount": "10530" },
        { "denom": "BNB", "amount": "247349863800" },
        { "denom": "BTC.B-918", "amount": "113218800" },
        { "denom": "COSMOS-587", "amount": "50000101983748977" },
        { "denom": "EDU-DD0", "amount": "139885964" },
        { "denom": "MFH-9B5", "amount": "1258976083286" },
        { "denom": "NASC-137", "amount": "0" },
        { "denom": "PPC-00A", "amount": "205150260" },
        { "denom": "TGT-9FC", "amount": "33251102828" },
        { "denom": "UCX-CC8", "amount": "1398859649" },
        { "denom": "USDT.B-B7C", "amount": "140456966268" },
        { "denom": "YLC-D8B", "amount": "210572645" },
        { "denom": "ZZZ-21E", "amount": "13988596" }
      ],
      "public_key": {
        "type": "tendermint/PubKeySecp256k1",
        "value": "AhOb3ZXecsIqwqKw+HhTscyi6K35xYpKaJx10yYwE0Qa"
      },
      "account_number": "406226",
      "sequence": "29"
    },
    "name": "",
    "frozen": null,
    "locked": [{ "denom": "KOGE48-35D", "amount": "10000000000" }]
  }
}
```

### Account Number

The `Account Number` is an internal identifier for the account. It is unique to each account.

### Sequence Number

The `Sequence Number` allows Binance Chain to prevent [replay attacks](https://en.wikipedia.org/wiki/Replay_attack). Every new transaction, when broadcast, should include an increment over the current `Sequence Number`. Once the transaction is recorded on the blockchain, the account's `Sequence Number` is incremented to the latest transaction's.

> This is similar to Cosmos' implementation of the Sequence Number, or Ethereum's [nonce](https://ethereum.stackexchange.com/questions/27432/what-is-nonce-in-ethereum-how-does-it-prevent-double-spending)

This logic forces the client to be aware of the current `Sequence Number`, either by reading from the
blockchain via API, or keep the counting locally by themselves. The recommended way is to keep
counting locally and re-synchronize from the blockchain periodically.
