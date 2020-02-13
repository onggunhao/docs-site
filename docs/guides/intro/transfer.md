---
id: transfer
title: Make a Transfer
---

Binance Chain is essentially a digital asset creation and exchange platform.
The features listed below are currently supported on Binance Chain:

- The Issuance, Burning, Minting and Freezing of Tokens
- Transfer of Tokens
- The Listing and Delisting of Tokens

Transfer is the most basic transaction Binance Chain supports, it moves assets among different addresses.

Please note the fees must be paid first in`BNB` before the transaction can be executed.

## Build Transfer Transaction

For sdk init, you should know the http api URL. Besides, you should know what kind of network the api gateway is in, since we have different configurations for test network and production network.

<!--DOCUSAURUS_CODE_TABS-->
<!--JavaScript-->

```js
const BnbApiClient = require("@binance-chain/javascript-sdk");
const axios = require("axios");

const asset = "BNB"; // asset string
const amount = 1.123; // amount float
const addressTo = "bnb1jxfh2g85q3v0tdq57fnevx6xcxtcnhtsmcu54m"; // addressTo string
const message = "A note to you"; // memo string
const api = "https://dex.binance.org/"; /// api string can be "https://testnet-dex.binance.org" for testnet

let privKey = "DEADBEEF"; // privkey hexstring (keep this safe)

const bnbClient = new BnbApiClient(api);
const httpClient = axios.create({ baseURL: api });

bnbClient.chooseNetwork("testnet"); // or this can be "mainnet"
bnbClient.setPrivateKey(privKey);
bnbClient.initChain();

const addressFrom = bnbClient.getClientKeyAddress(); // sender address string (e.g. bnb1...)
const sequenceURL = `${api}api/v1/account/${addressFrom}/sequence`;

httpClient
  .get(sequenceURL)
  .then(res => {
    const sequence = res.data.sequence || 0;
    return bnbClient.transfer(
      addressFrom,
      addressTo,
      amount,
      asset,
      message,
      sequence
    );
  })
  .then(result => {
    console.log(result);
    if (result.status === 200) {
      console.log("success", result.result[0].hash);
    } else {
      console.error("error", result);
    }
  })
  .catch(error => {
    console.error("error", error);
  });
```

<!--Go-->

```Go
//-----   Init KeyManager  -------------
keyManager1, _ := NewKeyManager()
//-----   Init sdk  -------------
client, err := sdk.NewDexClient("dex.binance.org", types.TestNetwork, keyManager) //api string can be "testnet-dex.binance.org" for testnet
accn,_:=client.GetAccount(client.GetKeyManager().GetAddr().String())
//-----   Init KeyManager  -------------
keyManager, _ := keys.NewMnemonicKeyManager(mnemonic)
//----   Send tx  -----------
send, err := client.SendToken([]msg.Transfer{{testAccount2, []ctypes.Coin{{nativeSymbol, 100000000}}}, {testAccount3, []ctypes.Coin{{nativeSymbol, 100000000}}}}, true)

fmt.Printf("Send token: %v\n", send)

```

<!--Python-->

```py
from binance_chain.http import HttpApiClient
from binance_chain.messages import TransferMsg
from binance_chain.wallet import Wallet

wallet = Wallet('private_key_string')
client = HttpApiClient()

transfer_msg = TransferMsg(
    wallet=wallet,
    symbol='BNB',
    amount=1,
    to_address='<to address>',
    memo='Thanks for the beer'
)
res = client.broadcast_msg(transfer_msg, sync=True)
```

<!--END_DOCUSAURUS_CODE_TABS-->
