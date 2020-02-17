---
id: make-transfer
title: Make a Transfer
---

`Transfer` is the most basic transaction of Binance Chain that allows assets to move between different addresses.

Each transfer costs a certain amount in BNB fees, which must be paid first before a transaction can be executed.

## Create another Account

We'll create another account to make a transfer to. Use the same

<!--DOCUSAURUS_CODE_TABS-->
<!--Mainnet CLI-->

```bash
$ bnbcli keys add new_key         # Create new account
$ bnbcli account <your-address>   # Check initial balance
    --chain-id Binance-Chain-Tigris
    --node https://dataseed5.defibit.io:443
    --indent
```

<!--Testnet CLI-->

```bash
$ tbnbcli keys add new_key        # Create new account
$ tbnbcli account <your-address>  # Check initial balance
    --chain-id Binance-Chain-Nile
    --node data-seed-pre-2-s1.binance.org:80
    --indent
```

<!--END_DOCUSAURUS_CODE_TABS-->

## Your First Transfer

Let's make a transfer from your first account to your second account.

<!--DOCUSAURUS_CODE_TABS-->
<!--Mainnet-->

```bash
$ bnbcli send
  --from <key_name (i.e. quickstart_key)>
  --to <second account address (e.g. bnbp1dkd....)>
  --amount 1:BNB    # Smallest unit of BNB available
  --chain-id Binance-Chain-Tigris
  --node  https://dataseed5.defibit.io:443
  --json
  --memo "Test transfer"
Password to sign with 'quickstart_key':
```

This should result in a `json` of the following format being returned:

```bash
{
   "Height":"68766197",
   "TxHash":"30CBDA98F636099665F0B7AB76BAD039FF5A63C0D29BD51D097D3E36188A5957",
   "Response":{
      "log":"Msg 0: ",
      "events":[
         {
            "attributes":[
               {
                  "key":"c2VuZGVy",
                  "value":"Ym5iMW16NzluNHQzMDlkcmY0NzQ1enZ0NW5jdXltcTh1N3huajdwdHh6"
               },
               {
                  "key":"cmVjaXBpZW50",
                  "value":"Ym5iMXlnM2VncnJ6enNjazQ2bWowd3RzdG05ZjYyMDlwcjB5ZWowdDA4"
               },
               {
                  "key":"YWN0aW9u",
                  "value":"c2VuZA=="
               }
            ]
         }
      ]
   }
}
```

<!--Testnet-->

```bash
$ tbnbcli send
  --from <key name (i.e. quickstart_key)>
  --to <second account address (e.g. tbnb12id...)>
  --amount 1:BNB
  --chain-id=Binance-Chain-Nile
  --node=data-seed-pre-2-s1.binance.org:80
  --json
  --memo "Test transfer"
```

This should result in a `json` of the following format being returned:

```bash
{
   "Height":"68766197",
   "TxHash":"30CBDA98F636099665F0B7AB76BAD039FF5A63C0D29BD51D097D3E36188A5957",
   "Response":{
      "log":"Msg 0: ",
      "events":[
         {
            "attributes":[
               {
                  "key":"c2VuZGVy",
                  "value":"Ym5iMW16NzluNHQzMDlkcmY0NzQ1enZ0NW5jdXltcTh1N3huajdwdHh6"
               },
               {
                  "key":"cmVjaXBpZW50",
                  "value":"Ym5iMXlnM2VncnJ6enNjazQ2bWowd3RzdG05ZjYyMDlwcjB5ZWowdDA4"
               },
               {
                  "key":"YWN0aW9u",
                  "value":"c2VuZA=="
               }
            ]
         }
      ]
   }
}
```

<!--END_DOCUSAURUS_CODE_TABS-->

## Transfer Types

### Multi-send

There are two main types of transfers:

- Single-receipient transfers (like we did above)
- Multi-send transfers that allows you to do multiple transfers in a single transaction, with reduced BNB fees.

You can learn more about multi-send in the [Transfers](../../transfer.md) page.

### Options

You can customize your transfer with a number of parameters, which you can access in the `bnbcli` or `tbnbcli` help menu.

```text
$ bnbcli send -h
Create and sign a send tx

Usage:
  bnbcli send [flags]

Flags:
      --account-number int   AccountNumber number to sign the tx
      --amount string        Amount of coins to send
      --async                broadcast transactions asynchronously
      --chain-id string      Chain ID of Binance Chain node
      --dry-run              ignore the perform a simulation of a transaction, but don't broadcast it
      --from string          Name or address of private key with which to sign
      --generate-only        build an unsigned transaction and write it to STDOUT
  -h, --help                 help for send
      --indent               Add indent to JSON response
      --json                 return output in json format
      --ledger               Use a connected Ledger device
      --memo string          Memo to send along with transaction
      --node string          <host>:<port> to tendermint rpc interface for this chain (default "tcp://localhost:26657")
      --print-response       return tx response (only works with async = false) (default true)
      --sequence int         Sequence number to sign the tx
      --source int           Source of tx
      --to string            Address to send coins
      --trust-node           Trust connected full node (don't verify proofs for responses) (default true)

Global Flags:
  -e, --encoding string   Binary encoding (hex|b64|btc) (default "hex")
      --home string       directory for config and data (default "/root/.bnbcli")
  -o, --output string     Output format (text|json) (default "text")
      --trace             print out full stack trace on errors
```
