# node-flappycoin

[![npm][npm-image]][npm-url]
[![downloads][downloads-image]][downloads-url]
[![js-standard-style][standard-image]][standard-url]

[npm-image]: https://img.shields.io/npm/v/flappycoin.svg?style=flat
[npm-url]: https://npmjs.org/package/flappycoin

[downloads-image]: https://img.shields.io/npm/dm/flappycoin.svg?style=flat
[downloads-url]: https://npmjs.org/package/flappycoin

[standard-image]: https://img.shields.io/badge/code%20style-standard-brightgreen.svg?style=flat
[standard-url]: http://standardjs.com

node-flappycoin is a simple wrapper for the flappycoin client's JSON-RPC API.

If starting a new project, I highly encourage you to take a look at the more modern [flappycoin-core](https://github.com/Flapmin/flaps), which features:
* ES6 support
* optional promise support
* support for newer REST API, in addition to RPC methods


## Install

`npm install flappycoin`

## Examples

### Create client
```js
// all config options are optional
var client = new flappycoin.Client({
  host: 'localhost',
  port: 8332,
  user: 'username',
  pass: 'password',
  timeout: 30000
});
```

### Get balance across all accounts with minimum confirmations of 6

```js
client.getBalance('*', 6, function(err, balance, resHeaders) {
  if (err) return console.log(err);
  console.log('Balance:', balance);
});
```
### Getting the balance directly using `cmd`

```js
client.cmd('getbalance', '*', 6, function(err, balance, resHeaders){
  if (err) return console.log(err);
  console.log('Balance:', balance);
});
```

### Batch multiple RPC calls into single HTTP request

```js
var batch = [];
for (var i = 0; i < 10; ++i) {
  batch.push({
    method: 'getnewaddress',
    params: ['myaccount']
  });
}
client.cmd(batch, function(err, address, resHeaders) {
  if (err) return console.log(err);
  console.log('Address:', address);
});
```

Flap on!