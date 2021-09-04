



Address beautification function, conversion between TH and 0x address.

Currently, the address conversion function on the JS side is provided.



```javascript
import Web3 from "thinkium-web3js";
const web3 = new Web3();
web3.Iban.toIban(address) // 0x to TH
web3.Iban.toAddress(address).toLowerCase();  //TH to 0x
```



