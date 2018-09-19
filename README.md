# truffle-hdwallet-provider-privkey-headers

HD Wallet-enabled Web3 provider. Use it to sign transactions for addresses derived from a raw private key string. 
This extension allows adding HTTP headers to the requests that
can be used for example for authorization. 

package extended by: `pzerfos@cs.ucla.edu`

## Install

```
$ npm install --save pzerfos/truffle-hdwallet-provider-privkey-headers
```

## General Usage

Headers are provided as a Javascript array of JS objects, one for each header, following the format:
```javascript
const headers = [
  {
    name: 'header_name',
    value: 'header_value'
  }
];
``` 

Usage: `w = new WalletProvider(privKey, providerURL, headers);`

You can use this provider wherever a Web3 provider is needed, not just in Truffle. For Truffle-specific usage, see next section.

```javascript
const HDWalletProvider = require("truffle-hdwallet-provider-privkey");
const privKey = "2442e1526f1..."; // raw private key
const provider = new HDWalletProvider(privKey, "http://localhost:8545");
```

By default, the `HDWalletProvider` will use the address of the first address that's generated from the private key. Currently, the `HDWalletProvider` manages only one address at a time, but it can be easily upgraded to manage (i.e., "unlock") multiple addresses.

Parameters:

- `privateKey`: `string`. Private key of account (DO NOT SHARE THIS EVER).
- `provider_uri`: `string`. URI of Ethereum client to send all other non-transaction-related Web3 requests.

## Truffle Usage

*to be updated*

You can easily use this within a Truffle configuration. For instance:

truffle.js
```javascript
const HDWalletProvider = require("truffle-hdwallet-provider-privkey");

const privKey = "2442e1526f1..."; // raw private key

module.exports = {
  networks: {
    development: {
      host: "localhost",
      port: 8545,
      network_id: "*" // Match any network id
    },
    ropsten: {
      provider: () => {
        return new HDWalletProvider(privKey, "https://ropsten.infura.io/MY_INFURA_KEY")
      },
      network_id: 3
    }
  }
};
```

## Web3 Provider

*to be updated*

You can also use the Wallet provider as an easy way to get a Web3 object that has an unlocked account to sign transactions through an INFURA node.

```javascript
const Web3 = require('web3')
const WalletProvider = require('truffle-hdwallet-provider-privkey')

const privKey = "2442e1526f1..."; // raw private key

const w = new WalletProvider(privKey, "https://ropsten.infura.io/MY_INFURA_KEY")
web3 = new Web3(w.engine)
```

## Notes

Make sure the `from` address you use when sending transactions is entirely lowercase or you will see an error like this:

```
TypeError: private key should be a Buffer
```

