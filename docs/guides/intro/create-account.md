---
id: create-account
title: Create an Account
---

The first thing you’ll need to do anything on the Binance Chain is an `Account`. An `Account` on Binance Chain consists of:

| Key             | Description                                                       |
| --------------- | ----------------------------------------------------------------- |
| Public key      | Derived from user's private key / seed phrase                     |
| Public Address  | 20 byte address prefixed with `bnb` (mainnet) or `tbnb` (testnet) |
| Account Number  | A unique number for each account                                  |
| Sequence Number | For replay protection. Similar to _nonce_ in ethereum             |
| Asset balances  | Consists of `available`, `locked`, and `frozen` assets            |

- _Locked_ assets are in an outstanding order. Once the order terminates (filled, cancelled, expired), the assets will be unlocked.

- _Frozen_ assets are frozen via [freeze transactions]().

## Create Account

You can generate a new key and mnemonic with `bnbcli` (`tbnbcli` for testnet). You will be asked to give the key a `name` which is used to refer to it locally.

For this quickstart, we will be creating a key named `quickstart_key`.

<!--DOCUSAURUS_CODE_TABS-->
<!--Mainnet CLI-->

```bash
$ bnbcli keys add quickstart_key
```

This should guide you through an interactive prompt to create your account.

```
Enter a passphrase for your key:
Repeat the passphrase:
NAME:	        TYPE:	ADDRESS:						            PUBKEY:
quickstart_key	local	bnb1c5dxrdn9xuw0njwcyevzyjrza550z5au8v0hyz	bnbp1addwnpepqwdsud63f5rq2wkgrezlvzdauf4x7wp3defzvhrzkwdzl7p0n6uk666ghpa
**Important** write this seed phrase in a safe place.
It is the only way to recover your account if you ever forget your password.

napkin degree boring custom differ smart bundle ball length lyrics auto forest jeans awake entry vocal there repeat rule churn picnic promote screen skull
```

<!--Testnet CLI-->

```bash
$ tbnbcli keys add quickstart_key
```

This should guide you through an interactive prompt to create your account. Note that testnet addresses have a prefix of `tbnb`.

```
Enter a passphrase for your key:
Repeat the passphrase:
NAME:	        TYPE:	ADDRESS:						            PUBKEY:
quickstart_key	local	bnb1c5dxrdn9xuw0njwcyevzyjrza550z5au8v0hyz	tbnbp1addwnpepqwdsud63f5rq2wkgrezlvzdauf4x7wp3defzvhrzkwdzl7p0n6uk666ghpa
**Important** write this seed phrase in a safe place.
It is the only way to recover your account if you ever forget your password.

napkin degree boring custom differ smart bundle ball length lyrics auto forest jeans awake entry vocal there repeat rule churn picnic promote screen skull
```

<!--END_DOCUSAURUS_CODE_TABS-->

> Remember to save your mnemonic in a safe place!

### Restoring Account

You can restore your account from just your seed phrase mnemonic.

<!--DOCUSAURUS_CODE_TABS-->
<!--Mainnet-->

```bash
$ bnbcli keys add recovery_test --recover
```

<!--Testnet-->

```bash
$ tbnbcli keys add recovery_test --recover
```

<!--END_DOCUSAURUS_CODE_TABS-->

This should guide you through an interactive prompt to restore your account.

```
Enter a passphrase for your key:
Repeat the passphrase:
> Enter your recovery seed phrase:
more advice achieve mass clap nose bike bird busy section rigid model doll exchange guard theme catalog junior patrol valley depart decade convince master
NAME:	        TYPE:	ADDRESS:						            PUBKEY:
recovery_test	local	bnb1c5dxrdn9xuw0njwcyevzyjrza550z5au8v0hyz tbnbp1addwnpepqwdsud63f5rq2wkgrezlvzdauf4x7wp3defzvhrzkwdzl7p0n6uk666ghpa
```

### Seeing list of Accounts

You can see the keys that are available to your local CLI using the following command:

<!--DOCUSAURUS_CODE_TABS-->
<!--Mainnet-->

```bash
$ bnbcli keys list
```

```shell
NAME:	        TYPE:	ADDRESS:						            PUBKEY:
quickstart_key	local	bnb1c5dxrdn9xuw0njwcyevzyjrza550z5au8v0hyz	bnbp1addwnpepqwdsud63f5rq2wkgrezlvzdauf4x7wp3defzvhrzkwdzl7p0n6uk666ghpa
recovery_test	local	bnb1c5dxrdn9xuw0njwcyevzyjrza550z5au8v0hyz tbnbp1addwnpepqwdsud63f5rq2wkgrezlvzdauf4x7wp3defzvhrzkwdzl7p0n6uk666ghpa
```

<!--Testnet-->

```bash
$ tbnbcli keys list
```

```shell
NAME:	          TYPE:	ADDRESS:						           PUBKEY:
quickstart_key	local	tbnb1c5dxrdn9xuw0njwcyevzyjrza550z5au8v0hyz	bnbp1addwnpepqwdsud63f5rq2wkgrezlvzdauf4x7wp3defzvhrzkwdzl7p0n6uk666ghpa
recovery_test	local	tbnb1c5dxrdn9xuw0njwcyevzyjrza550z5au8v0hyz bnbp1addwnpepqwdsud63f5rq2wkgrezlvzdauf4x7wp3defzvhrzkwdzl7p0n6uk666ghpa
```

<!--END_DOCUSAURUS_CODE_TABS-->

### Initial State

Your freshly created account has no transactions involved in it yet, and thus has not been stored in Binance Chain's state.

We can check this by querying the account with the following command:

<!--DOCUSAURUS_CODE_TABS-->
<!--Mainnet-->

```bash
$ bnbcli account <your-address>
    --chain-id Binance-Chain-Tigris # mainnet
    --node https://dataseed5.defibit.io:443
    --indent      # formatting
    --trust-node  # skips querying proofs (i.e. faster)
```

<!--Testnet-->

```bash
$ tbnbcli account <your-address>
    --chain-id Binance-Chain-Nile # testnet
    --node data-seed-pre-2-s1.binance.org:80
    --indent      # formatting
    --trust-node  # skips querying proofs (i.e. faster)
```

<!--END_DOCUSAURUS_CODE_TABS-->

This should give the following result.

```shell
ERROR: No account with address bnb1yg3egrrzzsck46mj0wtstm9f6209pr0yej0t08 was found in the state.
Are you sure there has been a transaction involving it?
```

## Funding the account

To initialize your account, you need to send a transaction to it. We'll send some BNB to the account to cover the transaction fees for the rest of the Quickstart.

<!--DOCUSAURUS_CODE_TABS-->
<!--Mainnet-->

#### Obtaining BNB

- You can buy BNB at [Binance.com](https://www.binance.com/en/buy-sell-crypto/channel-list/buy/USD/BNB/10)
- This will be deposited to your Binance.com exchange account

#### Sending to Account

- Withdraw the BNB to the address you generated earlier
- A [withdrawal guide](https://www.binance.vision/tutorials/how-to-withdraw) is available on Binance Academy

<!--Testnet-->

#### Obtaining tBNB

- You can obtain free Testnet BNB at our [testnet faucet](https://www.binance.com/en/dex/testnet/address)
- Enter the address you generated earlier
- A [testnet faucet guide](https://www.binance.vision/tutorials/binance-dex-funding-your-testnet-account) is available on Binance Academy

<!--END_DOCUSAURUS_CODE_TABS-->

## Re-querying Account Balance

Let's run the query balance CLI command again.

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

This time, a `json` representing key account details will be returned.

> Note: amounts in Binance Chain are unsigned integers, shifted by **10^8** to represent decimals

```json
{
  "type": "bnbchain/Account",
  "value": {
    "base": {
      "address": "bnb1mz79n4t309drf4745zvt5ncuymq8u7xnutg0xn",
      "coins": [
        {
          "denom": "BNB",
          "amount": "20000000000"
        }
      ],
      "public_key": null,
      "account_number": "698680",
      "sequence": "0"
    },
    "name": "",
    "frozen": null,
    "locked": null,
    "flags": "0"
  }
}
```

## Account Data Structure

### Account Number

The `Account Number` is an internal identifier for the account. It is unique to each account.

### Sequence Number

The `Sequence Number` allows Binance Chain to prevent [replay attacks](https://en.wikipedia.org/wiki/Replay_attack). Every new transaction, when broadcast, should include an increment over the current `Sequence Number`. Once the transaction is recorded on the blockchain, the account's `Sequence Number` is incremented to the latest transaction's.

> Sequence Numbers are similar to Cosmos' implementation, or Ethereum's [nonce](https://ethereum.stackexchange.com/questions/27432/what-is-nonce-in-ethereum-how-does-it-prevent-double-spending)
