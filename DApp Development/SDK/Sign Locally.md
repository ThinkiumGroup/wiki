



In some application scenarios, local signature and verification methods are required.



### Sign Text String locally

```js
const Web3 = require('thinkium-web3js');

let web3 = new Web3();
let message = web3.toUtf8(originHash);
let hash = web3.cipher.hash256(message);
let signature = web3.cipher.sign(new Buffer.from(hash, 'hex'), privateKey);
```

### Verify signature locally

```js
web3.cipher.verify(hash, signature, publicKey) 
```



