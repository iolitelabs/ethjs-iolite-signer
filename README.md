## ethjs-iolite-signer

A simple module for signing iOlite transactions.

**WARNING: This module does not have EIP155 replay protection, do not use until it is upgraded.**

## Install

```
npm install --save ethjs-iolite-signer
```

## Usage

```js
const HttpProvider = require('ethjs-provider-http');
const Eth = require('ethjs-query');
const eth = new Eth(new HttpProvider('http://localhost:8545'));
const sign = require('ethjs-iolite-signer').sign;
const BN = require('bignumber.js');

const address = '0x0F6af8F8D7AAD198a7607C96fb74Ffa02C5eD86B';
const privateKey = '0xecbcd9838f7f2afa6e809df8d7cdae69aa5dfc14d563ee98e97effd3f6a652f2';

eth.getTransactionCount(address).then((nonce) => {
  eth.sendRawTransaction(sign({
    to: '0xce31a19193d4b23f4e9d6163d7247243bAF801c3',
    value: 300000,
    gas: new BN('43092000'),
    // when sending a raw transactions it's necessary to set the gas price, currently 0.00000002 ETH
    gasPrice: new BN('20000000000'),
    nonce: nonce,
    metadata: '0xf87b948f9767c5e8fff4be9295f71c8efed26332d19f11b864f906a4400000000000000000000000000000000000000000000000000000000000000020000000000000000000000000000000000000000000000000000000000000000c48656c6c6f20694f6c6974650000000000000000000000000000000000000000',
    metadataLimit: '0x1234'
  }, privateKey)).then((txHash) => {
    console.log('Transaction Hash', txHash);
  });
});
```

Note, that address and private key are a valid address and private key. Only use this example address for local testing and setup. You will loose your Ether if you send it to this address.

## Method API

```
sign     <Function  (Object, String [, Boolean]) : (String|Array)>
signWeb3 <Function  (Object, String [, Boolean]) : (Object)>
recover  <Function  (Object|String, Number, Object, Object) : (Object)>
```

## Contributing

Please help better the ecosystem by submitting issues and pull requests to `ethjs-signer`. We need all the help we can get to build the absolute best linting standards and utilities. We follow the AirBNB linting standard and the unix philosophy.

## Guides

You'll find more detailed information on using `ethjs-signer` or `ethjs-iolite-signer` and tailoring it to your needs in our guides:

- [User guide](docs/user-guide.md) - Usage, configuration, FAQ and complementary tools.
- [Developer guide](docs/developer-guide.md) - Contributing to `ethjs-signer` or `ethjs-iolite-signer` and writing your own code and coverage.
