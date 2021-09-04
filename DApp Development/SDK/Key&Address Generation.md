

Currently, JS  has provided mnemonic, private key, public key, address generation method, which is convenient for app-side developers to use.



### 1 Generate Mnemonic

```js
const bip39 = require('bip39');
let mnemonicWords = await bip39.generateMnemonic();
console.log('createMnemonicWords', mnemonicWords);
```

### 2 Generate PrivateKey through Mnemonic

```js
let seed = await bip39.mnemonicToSeed(mnemonicWords);
let hdWallet = hdkey.fromMasterSeed(seed);
let key1 = hdWallet.derive("m/44'/60'/0'/0/0");
let privateKey = '0x' + key1._privateKey.toString('hex');
console.log('privateKey', privateKey);
```

### 3 Generate PublicKey through PrivateKey

```js
var util = require('ethereumjs-util');
let publicKey = util.bufferToHex(util.privateToPublic( util.toBuffer(privateKey)));
console.log('publicKey', publicKey)
```

### 4 Generate Address through PublicKey

```js
var util = require('ethereumjs-util');
var address = util.pubToAddress(util.toBuffer(publicKey), true);
//  base BIP55 contract to encode address again
address = util.toChecksumAddress('0x' + address.toString('hex'));
console.log('address', address)
```

### 
