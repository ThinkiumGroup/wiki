TMMSK wallet development Demo

GitHub ：[https://github.com/ThinkiumGroup/TMMSK-Demo.git](https://github.com/ThinkiumGroup/TMMSK-Demo.git)



### Check if the browser is running the TMMSK plug-in

```react
function checkTmmsk() {
  if (typeof window !== 'undefined' && typeof window.thinkium !== 'undefined') {
    alert('TMMSK is installed');
  } else {
    alert('TMMSK not exists');
  }
}
```



### Initialize window.thinkium

TMMSK will inject window.thinkium instance into the current page

```react
function init(type = 0) {
  //let currentChainId = parseInt(window.window.thinkium.chainId, 16)
  let thinkium = window.thinkium
  //Prohibit automatic refresh, required by metamask
  thinkium.autoRefreshOnNetworkChange = false
  //Start calling metamask
  thinkium.enable().then(function (accounts) {
    if(type == 0) {
      alert('The connection is successful, the current wallet address is: ' + accounts[0].toLowerCase())
    }
    //Initialize provider
    let provider = window['thinkium'] || window.web3.currentProvider
    //Initialize Web3
    window.web3 = new Web3(provider)
    window.defaultAccount = accounts[0].toLowerCase()
  }).catch(function (error) {
    console.log('enable-error', error)
    alert('connection error')
  })
}
```



### Get account address

```react
async function getAddress() {
  // Authorization to obtain an account
  const accounts = await window.web3.eth.getAccounts();
  const myAccount = accounts[0];
  alert('The current wallet address is ' + myAccount)
}
```



### Transfer on the same chain

```react
 async function transfer() {
    let transactionParameters = {
      from: '0x0d7a8575469d627563C8e90ea65408deCa98d38a',  //0x address
      to: '0xc1ec694522bf577775c6e704f0ad479dba0ad436',    //0x address
      value: '10000000000000',
      input: ''
    }

    let txHash = await window.thinkium.request({
      method: 'eth_sendTransaction',
      params: [transactionParameters],
    })
    alert('The transfer transaction is sent successfully, the hash is：' + txHash)
  }
```



### Get balance

```react
async function getBalance() {
    // Authorization to obtain an account
    const accounts = await window.web3.eth.getAccounts();
    const myAccount = accounts[0];
    console.log(myAccount, 1);
    // Return the balance of the account at the specified address
    const balance = await window.web3.eth.getBalance(myAccount) 
    // window.thinkium.request({ method: 'eth_getBalance', params: [myAccount, "latest"], "id": 2 });
    alert('The current account balance is ' + new BigNumber(balance).div("1e+18"))
  }
```



### Get transaction

```react
async function checkTransaction() {
  // let txHash = '0x8cfe9b79e326b4def2db02a261626724ae1db0d8f88bdd910cb333a1223e2d1d';
  let txHash = '0x74f92bb0a085e00eb095afe33dbd663635d88a5eff92ff47c385b251077c9a10';
  let result = await window.web3.eth.getTransactionReceipt(txHash); // success
  console.log('--result', result)
}
```



### Contract call

```react
function callContract() {
    let contractAddress = '0x36fde683c46483a2ffd9aeb7b77a511db077c19c';
    let myContract = new window.web3.eth.Contract(HelloWorldAbi, contractAddress);

    myContract.methods.set('111').send({ from: window.defaultAccount })
      .on('transactionHash', function (transactionHash) {
        console.log('transactionHash',transactionHash)
      })
      .on('confirmation', function (confirmationNumber, receipt) {
        console.log('confirmation', { confirmationNumber: confirmationNumber, receipt: receipt })
      })
      .on('receipt', function (receipt) {
        console.log('receipt', { receipt: receipt })
      })
      .on('error', function (error, receipt) {
        console.log('error',{ error: error, receipt: receipt })
      })

     myContract.methods.get().call().then((res) => {
      console.log('---resultGet', res)
    })
  }
```

