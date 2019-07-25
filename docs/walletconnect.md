# <img src="./assets/walletconnect.svg" width="60"> WalletConnect

The Binance Chain Web Wallet supports connecting with external wallet providers via the [WalletConnect protocol](https://docs.walletconnect.org/tech-spec).

WalletConnect allows the user to scan a QR code from the wallet app to unlock and use their wallet seamlessly in the web UI.

In order for this to work, some modifications to the standard WalletConnect protocol are used in the Binance Chain wallet's implementation.

See the list of wallets which support WalletConnect on Binance Chain [here](walletconnect-support.md)

## Connecting via WalletConnect

Wallet providers should make use of the [WalletConnect Client SDK](https://docs.walletconnect.org/client-sdk) for their target programming language and OS. There are implementations [on GitHub](https://github.com/walletconnect) for iOS, Android, React Native, etc.

## Protocol Differences

Since we do not use Ethereum transactions, there are some differences:

* Typically `sendTransaction` is used with Ethereum transaction parameters in WalletConnect dApp integrations. But in Binance Chain's case, instead of invoking `sendTransaction` in the WalletConnect flow, the new [`sendCustomRequest`](https://docs.walletconnect.org/client-sdk#send-custom-request) call is used instead with a method called `bnb_sign` (see below).

* The external wallet provider is responsible for sending back the signature and public key of the transaction but should _not_ broadcast the transaction itself. We have instead defined a custom `result` format in the form of stringified JSON containing the signature and public key. The reason for this is that the wallet app probably does not have access to the complete serialized binary form of the transaction (as this requires Amino encoding).

* The web wallet will send back a second custom call (after `bnb_sign`) called `bnb_tx_confirmation`, which contains the boolean result of the transaction build/broadcast and any error message encountered by the web wallet during broadcasting. In a complete implementation, this confirmation callback should be responded to with a call to `approveRequest`.

## Sequence Diagram

This sequence diagram shows the flow of messages when the web wallet interacts with an external wallet provider via WalletConnect.

![WalletConnect Protocol Sequence](./assets/walletconnect_sequence.png)

## Custom Requests

A custom call request adheres to this structure:

```json
{
  "id": 1,
  "jsonrpc": "2.0",
  "method": "method_name",
  "params": [{ ... }],
}
```

We have two custom call request formats, here are examples of them:

### Example: bnb_sign

```json
{
  "method": "bnb_sign",
  "params": [
    {
      "account_number": "34",
      "chain_id": "Binance-Chain-Nile",
      "data": null,
      "memo": "test",
      "msgs": [
        {
          "inputs": [
            {
              "address": "tbnb1hgm0p7khfk85zpz5v0j8wnej3a90w709zzlffd",
              "coins": [
                {
                  "amount": 1000000000,
                  "denom": "BNB",
                },
              ],
            },
          ],
          "outputs": [
            {
              "address": "tbnb1ss57e8sa7xnwq030k2ctr775uac9gjzglqhvpy",
              "coins": [
                {
                  "amount": 1000000000,
                  "denom": "BNB",
                },
              ],
            },
          ],
        },
      ],
      "sequence": "31",
      "source": "1",
    }
  ]
}
```

#### Response (approveRequest)

A response like this should be sent back from the wallet app:

```json
{
  "id": 1553682007906047,
  "result": "{\"signature\":\"...\",\"publicKey\":\"...\"}"
}
```

In `result`, a JSON-encoded object must be included containing the following hex-string properties: `signature`, `publicKey`.

Note that:

* `id` and `jsonrpc` are usually pre-filled by the client SDK, so there should be no need to set this in the object yourself.

* `signature` should be 64 bytes in length (128 hex chars)

* `publicKey` should be 65 bytes in length (130 hex chars, non-compressed form, prefixed with `0x04`)

### Example: bnb_tx_confirmation

```json
{
  "method": "bnb_tx_confirmation",
  "params": [
    {
      "ok": true,
      "error": "Error message (optional)"
    }
  ]
}
```

Receipt of the `bnb_tx_confirmation` should be confirmed by the app with `approveRequest` as per the WalletConnect protocol flow.

For this response, `result` may be empty or contain an empty JSON-encoded object:

#### Response (approveRequest)

A response like this should be sent back from the wallet app:

```json
{
  "id": 1553682007906050,
  "result": ""
}
```

## Ending the Session

Remember to call `killSession()` when the user has finished using the integration from your app!

This will redirect the user back to the unlock screen in the web wallet.

## Continuous WalletConnect

A revised Wallet Connect communication steps are disccussed [here](https://github.com/binance-chain/BEPs/pull/23). After users’ consent, Mobile or other Wallet can *continuously* sign requested transactions from Web Wallet without promoting to user for confirmation, as long as the transactions satisfy the predefined and agreed with the conditions.

### Continuous Signing Wallet

Upon scanning the QR code, or after getting the first transaction to confirm, the mobile Wallet can ask for the below optional input parameters. After the wallet may directly sign the requested transactions without asking users to review and confirm the trade.

* Supported transaction type: NewOrder and Cancel

| Name | Type | Content |
|------|------|---------|
| Timeout Window | int64 | time in minutes. It stands for these minutes, mobile Wallet will not ask for confirmation but directly sign the requested transactions. If yes, the “Timeout Window” will be renewed after the last user transaction. |
| Allowed Symbols | string | A string of different asset symbols, separated by “,” (comma). Only the trading pairs that have base asset contained by this string can be traded. |
| Allowed Order Size | int64 | Only the orders that have a smaller quantity than this number are directly signed. |
| Allowed Total Quantity | int64 | The total quantity of the orders should be no larger than the value defined here |
| Allowed Number of Orders | int64 | Total number of order is allowed |
| Cancel Is Relaxed | bool | If yes, the “Allowed Symbols” and “Allowed Order Size” and “Allowed Total Quantity” and “Allowed Number of Orders” are NOT applicable to limit the Cancel action, i.e. all the cancels can be signed within the “Timeout Window”. |

### Implementation

The Equal has opensourced their WalletConnect implementation: https://github.com/Equal-Network/WalletConnect-BinanceDEX-GoogleChrome

Core characteristics:

* Support WalletConnect
* Read QR-code from Binance Dex
* Auto connect to Binance dex
* Auto approve session from WalletConnect
* Approve / reject request from WalletConnect
* Kill session