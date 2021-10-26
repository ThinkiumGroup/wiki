## Test Contract Service address

For testing environment only! For testing only!

Service address: **contract-test.thinkium.org**

rpc address: **test.thinkiumrpc.net**

AES encryption password: **key1="yitawzdk3ueqarfq" ;key2="azrtiabarda3ufgq"**

(Encryption password is used to symmetrically encrypt and sign the private key, and then pass it to the Contract Service to resist the risk of private key leakage)



## Global parameter description

1. The url of each interface parameter is the rpc service address. The production environment needs to be configured with the production rpc address, which can be applied to the official customer service. You can also use your own deployed version.

2. The businessId of each interface parameter is the business id, which is used to match the configuration items of each business. It is currently used to match the Aes key (the aes key is used to encrypt the private key of the trading account)

    (1) The bussinessId is 1 and the corresponding secret key is yitawzdk3ueqarfq

    (2) The bussinessId is 2 and the corresponding secret key is azrtiabarda3ufgq

3. Each interface parameter notifyUrl and attach are not necessary. If these two parameters are passed in the transaction interface, it will be called back to the corresponding address, but 100% callback is not guaranteed. Therefore, it is necessary to call the 3.14 interface to actively query the transaction results

4. All interfaces that have the notifyUrl field will receive a callback. The callback structure is as follows, and the specific structure is subject to the return of the callback interface

```json
{
    "attach":"1-666212010161642094848790",
    "blockHeight":9061425,
    "code":200,
    "contractAddress":"0x0000000000000000000000000000000000000000",
    "errorMsg":"",
    "hash":"0x43a989f62947f94754f3433cd1a05fdb1f9f16d3c08105ede3b7a73130680a23",
    "inputUnpack":{
        "method":"",
        "inputmap":null
    },
    "logs":[
        {
            "address":"0x58e322d9fbe83d5476d217bcee076f5ec567ff35",
            "blockNumber":"0x8a4431",
            "data":"000000000000000000000000000000000000000000000000000000000000183636363231323031303136313634323039343834383739300000000000000000",
            "logIndex":"0x0",
            "topics":[
                "0xe156df32946fe9ea0fb3803e9b88ca80a09d92a56b05f1b049af2bc9c43adec0"
            ],
            "transactionHash":"0x43a989f62947f94754f3433cd1a05fdb1f9f16d3c08105ede3b7a73130680a23",
            "transactionIndex":"0x0"
        }
    ],
    "out":"0x000000000000000000000000000000000000000000000000000000000000005a",
    "root":"eyJmZWUiOiIxOTQ2MDEyMDAwMDAwMDAwMDAiLCJyb290IjpudWxsfQ==",
    "status":1,
    "transactionHash":"0x43a989f62947f94754f3433cd1a05fdb1f9f16d3c08105ede3b7a73130680a23",
    "tx":{
        "chainid":1,
        "extra":"0x",
        "from":"0xe1723ff732b9b90d5b083495678f9e218a2be70d",
        "hash":"",
        "input":"0x48e3ae17000000000000000000000000000000000000000000000000000000000000002000000000000000000000000000000000000000000000000000000000000000600000000000000000000000000000000000000000000000000000183636363231323031303136313634323039343834383739300000000000000000000000000000000000000000000000000000000000000000000000000000020b7b226365727448617368223a22374a4531776f5373614f59654d61486a77326b7a5976664f315950665533514c343347684a4b326b7a56455c7530303364222c226964223a3136352c22757365724964223a32392c226e616d65223a22e6b58be8af95222c22636572744e6f223a22363636323132303130313631363432303934383438373930222c2274797065223a322c22706174302c22737461747573223a302c22636861696e54696d65223a302c226170706c7954696d65223a302c226e6f746172697a6554696d65223a302c2263726561746554696d65223a313630323833373732392c2275706461746554696d65223a307d000000000000000000000000000000000000047375636300000000000000000000000000000000000000000000000000000000",
        "nonce":213,
        "timestamp":0,
        "to":"0x58e322d9fbe83d5476d217bcee076f5ec567ff35",
        "uselocal":false,
        "value":0
    }
}
```



## Contract service Http interface

### 1. Get account information

1. This interface is used to obtain the account information on the chain corresponding to the address, where the nonce is the transaction counter of the corresponding account on the chain. Every time a transaction is executed, the nonce value will automatically increase by 1 as long as the transaction is packaged whether it is successful or not. Therefore, each new transaction needs to get the latest nonce value and pass it into the corresponding interface.
2. The account information of the same address is isolated on different chains, and the nonce value is also isolated
3. Because on-chain transaction confirmation takes time, if you need to send transactions in batches, the client should self-increase the nonce value, that is, first obtain the latest nonce value on the chain, and add 1 to the nonce after each transaction is sent.



Interface address: **/v1/account/get**

Request method: **POST**
Request parameters:

| Parameter name | Required | Type | Description |
| ------- | ---- | ------ | ----------------------------- ------------- |
| chainId | Y | String | 1 |
| address | Y | String | 0xe3b3599093af404231761ca1cf36a11e97571312 |

Return parameter description:

| Parameter name | Type | Description |
| ------ | ------ | -------------- |
| code 		| string | Return code |
| msg 		| string | Return information |
| data 		| 		 | Returned business information |

data:

| Parameter name | Type | Description |
| --------------- | ------ | -------------------------- -------------------- |
| address 			| String 	| User address |
| codeHash 			| 			| 		|
| credit 			| Int 		||
| localCredit 		| 			| |
| longStorageRoot 	| 			| 			|
| nonce 			| Int 		| The nonce value is the nonce transaction executed by this account on the 										specified chain |
| storageRoot 		| 			| |

Request Example:

```json
{
  "chainId" : "1",
  "address":"0x6a1fb9bfb756bf3d8aa28a189c8d0cb1b277809a"
}
```

Return Example：

```json
{
    "code":200,
    "msg":"success",
    "data":{
        "address":"0x6a1fb9bfb756bf3d8aa28a189c8d0cb1b277809a",
        "balance":0,
        "balanceValue":0,
        "codeHash":null,
        "localCurrency":null,
        "longStorageRoot":null,
        "nonce":0,
        "storageRoot":null
    }
}
```



### 2. Compile the contract

Interface address: **/v1/contract/compile**

Request method: **POST**
Request parameters:

| Parameter name | Required | Type | Description |
| ----------- | ---- | ------------------ | ------------- ----------------------------------------------- |
| contractMap | Y | Map<String,String> | map type, key is the contract name, value is the contract code. If there are multiple contract files, one of the files must be named **Main.sol** and designated as the main contract file If you are combining multiple contract file codes into one, you need to specify the key as the contract name of the main contract, such as **Order** |

Return parameter description

| Parameter name | Type | Description |
| ------ | ------ | -------------- |
| code 		| string | Return code |
| msg 		| string | Return information |
| data 		| 		 | Returned business information |

data:

| Parameter name | Type | Description |
| ------------ | ---- | ------------------------------- ----------- |
| contractName 	| | contract name |
| abi 			| | The returned contract abi, which contains constructors and basic methods, etc. |
| bytecode 		| | Contract bytecode (used for deployment) |

Request example

Contract code example

```java
pragma solidity >= 0.5.0;

contract HelloWorld {
  uint256 age = 17;
  string nickname = "Hello";

  function getAge() public view returns (uint256 data){
    return age;
  }

  function getNickname() public view returns (string memory data){
    return nickname;
  }

  function setNickname(string memory data) public {
    nickname = data;
  }
}
```

Corresponding conversion request parameters

```json
{
    "businessId":"1",
    "contractMap":{
        "Main.sol":"pragma solidity >= 0.5.0;\ncontract HelloWorld {\n uint256 age = 17;\n string nickname = \"Hello\";\n function getAge() public view returns (uint256 data){\n return age;\n }\n function getNickname() public view returns (string memory data){\n return nickname;\n }\n function setNickname(string memory data) public {\n nickname = data;\n }\n}"
    }
}
```

OR

```json
{
    "businessId":"1",
    "contractMap":{
        "HelloWorld":"pragma solidity >= 0.5.0;\ncontract HelloWorld {\n uint256 age = 17;\n string nickname = \"Hello\";\n function getAge() public view returns (uint256 data){\n return age;\n }\n function getNickname() public view returns (string memory data){\n return nickname;\n }\n function setNickname(string memory data) public {\n nickname = data;\n }\n}"
    }
}
```

Return example

```json
{
    "code":200,
    "msg":"success",
    "data":{
        "contractAddress":"",
        "contractName":"HelloWorld",
        "abi":"[{\"constant\":false,\"inputs\":[{\"name\":\"data\",\"type\":\"string\"}],\"name\":\"setNickname\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":true,\"inputs\":[],\"name\":\"getAge\",\"outputs\":[{\"name\":\"data\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"view\",\"type\":\"function\"},{\"constant\":true,\"inputs\":[],\"name\":\"getNickname\",\"outputs\":[{\"name\":\"data\",\"type\":\"string\"}],\"payable\":false,\"stateMutability\":\"view\",\"type\":\"function\"}]",    	"bytecode":"0x601160005560c0604052600560808190527f48656c6c6f00000000000000000000000000000000000000000000000000000060a09081526100439160019190610056565b5034801561005057600080fd5b506100f1565b828054600181600116156101000203166002900490600052602060002090601f016020900481019282601f1061009757805160ff19168380011785556100c4565b828001600101855582156100c4579182015b828111156100c45782518255916020019190600101906100a9565b506100d09291506100d4565b5090565b6100ee91905b808211156100d057600081556001016100da565b90565b610338806101006000396000f3fe6080604052600436106100565763ffffffff7c01000000000000000000000000000000000000000000000000000000006000350416631c5d9faa811461005b578063967e6e6514610110578063abe4136f14610137575b600080fd5b34801561006757600080fd5b5061010e6004803603602081101561007e57600080fd5b81019060208101813564010000000081111561009957600080fd5b8201836020820111156100ab57600080fd5b803590602001918460018302840111640100000000831117156100cd57600080fd5b91908080601f0160208091040260200160405190810160405280939291908181526020018383808284376000920191909152509295506101c1945050505050565b005b34801561011c57600080fd5b506101256101d8565b60408051918252519081900360200190f35b34801561014357600080fd5b5061014c6101df565b6040805160208082528351818301528351919283929083019185019080838360005b8381101561018657818101518382015260200161016e565b50505050905090810190601f1680156101b35780820380516001836020036101000a031916815260200191505b509250505060405180910390f35b80516101d4906001906020840190610274565b5050565b6000545b90565b60018054604080516020601f6002600019610100878916150201909516949094049384018190048102820181019092528281526060939092909183018282801561026a5780601f1061023f5761010080835404028352916020019161026a565b820191906000526020600020905b81548152906001019060200180831161024d57829003601f168201915b5050505050905090565b828054600181600116156101000203166002900490600052602060002090601f016020900481019282601f106102b557805160ff19168380011785556102e2565b828001600101855582156102e2579182015b828111156102e25782518255916020019190600101906102c7565b506102ee9291506102f2565b5090565b6101dc91905b808211156102ee57600081556001016102f856fea165627a7a723058208c582212c275d0c3855b62b3cb43619e0389cc7ef234d69a2e9206b5728fda8b0029"
    }
}
```


### 2. Release the contract (using the compiled abi)

This interface does not return the contract address. The contract address needs to be queried through the 3.14 interface according to the returned hash. If the transaction is successful (status=1), the contractAddress in the return result is the contract address on the chain

Interface address: **/v1/contract/deploy/abi**

Request method: **POST**
Request parameters:

| Parameter name | Required | Type | Description |
| ------------ | ---- | ------------------------ | ------ -------------------------------------------------- ---- |
| businessId 	| Y | String | Business id, currently used to match the aes key of the corresponding business |
| from 			| Y | String | Transaction initiation address |
| chainId 		| Y | String | Chain ID |
| attach 		| F | String | Auxiliary information, used with notifyUrl, this field will be returned when 									callback |
| nonce 		| Y | String | Latest nonce of trading account |
| params 		| Y | List<Map<String,Object>> | Parameters required by contract constructor |
| privateKey 	| Y | String | The private key corresponding to the encrypted from address, which needs to be 									encrypted with the aes key corresponding to the businessId |
| notifyUrl 	| F | String | Callback address |
| contractJson 	| Y | json 	 | contract abi |

contractJson:

| Parameter name | Required | Type | Description |
| -------- | ---- | ------ | -------------- |
| bytecode 	| Y | String | Compiled bytecode |
| abi 		| Y | String | Contract abi |



Return parameter description

| Parameter name | Type | Description |
| ------ | ------ | -------------- |
| code 		| string | Return code |
| msg 		| string | Return information |
| data 		| 		 | Returned business information |

data:

| Parameter name | Type | Description |
| ------------ | ------ | --------------- |
| msg 			| 			| Return information |
| hash 			| String 	| Transaction hash |
| nonce 		| String 	| The latest nonce value of the account |
| contractJson 	| 			| Contract Data |

 

contractJson:

| Parameter name | Type | Description |
| --------------- | ------ | -------- |
| contractAddress 	| String | Contract Address |
| contractName 		| String | contract name |
| abi 				| String | Contract abi |
| bytecode 			| String | 				|

Request example

```json
{
    "businessId":"1",
    "from":"0x6a1fb9bfb756bf3d8aa28a189c8d0cb1b277809a",
    "chainId":"1",
    "attach":"1,2,3,4,5",
    "nonce":2,
    "params":{},
    "privateKey":"U28HRVeQCizyJ3SUtaqpkroysZ/hN4g8baLLZqKBHkSsbhbNfH+Fl7qxtQrhH1b9j60igdcbCZ4LyE2jwa9vdlN7SSCWK2W0f4jf7bEGkV0=",
    "notifyUrl":"http://localhost:8101/v1/test/",
    "contractJson":{
        "abi":"[{\"constant\":false,\"inputs\":[{\"name\":\"data\",\"type\":\"string\"}],\"name\":\"setNickname\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":true,\"inputs\":[],\"name\":\"getAge\",\"outputs\":[{\"name\":\"data\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"view\",\"type\":\"function\"},{\"constant\":true,\"inputs\":[],\"name\":\"getNickname\",\"outputs\":[{\"name\":\"data\",\"type\":\"string\"}],\"payable\":false,\"stateMutability\":\"view\",\"type\":\"function\"}]",
        "bytecode":"0x601160005560c0604052600560808190527f48656c6c6f00000000000000000000000000000000000000000000000000000060a09081526100439160019190610056565b5034801561005057600080fd5b506100f1565b828054600181600116156101000203166002900490600052602060002090601f016020900481019282601f1061009757805160ff19168380011785556100c4565b828001600101855582156100c4579182015b828111156100c45782518255916020019190600101906100a9565b506100d09291506100d4565b5090565b6100ee91905b808211156100d057600081556001016100da565b90565b610338806101006000396000f3fe6080604052600436106100565763ffffffff7c01000000000000000000000000000000000000000000000000000000006000350416631c5d9faa811461005b578063967e6e6514610110578063abe4136f14610137575b600080fd5b34801561006757600080fd5b5061010e6004803603602081101561007e57600080fd5b81019060208101813564010000000081111561009957600080fd5b8201836020820111156100ab57600080fd5b803590602001918460018302840111640100000000831117156100cd57600080fd5b91908080601f0160208091040260200160405190810160405280939291908181526020018383808284376000920191909152509295506101c1945050505050565b005b34801561011c57600080fd5b506101256101d8565b60408051918252519081900360200190f35b34801561014357600080fd5b5061014c6101df565b6040805160208082528351818301528351919283929083019185019080838360005b8381101561018657818101518382015260200161016e565b50505050905090810190601f1680156101b35780820380516001836020036101000a031916815260200191505b509250505060405180910390f35b80516101d4906001906020840190610274565b5050565b6000545b90565b60018054604080516020601f6002600019610100878916150201909516949094049384018190048102820181019092528281526060939092909183018282801561026a5780601f1061023f5761010080835404028352916020019161026a565b820191906000526020600020905b81548152906001019060200180831161024d57829003601f168201915b5050505050905090565b828054600181600116156101000203166002900490600052602060002090601f016020900481019282601f106102b557805160ff19168380011785556102e2565b828001600101855582156102e2579182015b828111156102e25782518255916020019190600101906102c7565b506102ee9291506102f2565b5090565b6101dc91905b808211156102ee57600081556001016102f856fea165627a7a723058208c582212c275d0c3855b62b3cb43619e0389cc7ef234d69a2e9206b5728fda8b0029"
    }
}
```

Return example

```json
{
    "code":200,
    "msg":"success",
    "data":{
        "msg":"",
        "hash":"0x0b60f43eca86166ef4482d4e6a00425baab4428fb8ac4f4e1ce1a16d252ee6cd",
        "nonce":"2",
        "contractJson":{
            "contractAddress":"",
            "contractName":"",
            "abi":"[{\"constant\":false,\"inputs\":[{\"name\":\"data\",\"type\":\"string\"}],\"name\":\"setNickname\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":true,\"inputs\":[],\"name\":\"getAge\",\"outputs\":[{\"name\":\"data\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"view\",\"type\":\"function\"},{\"constant\":true,\"inputs\":[],\"name\":\"getNickname\",\"outputs\":[{\"name\":\"data\",\"type\":\"string\"}],\"payable\":false,\"stateMutability\":\"view\",\"type\":\"function\"}]",
            "bytecode":"0x601160005560c0604052600560808190527f48656c6c6f00000000000000000000000000000000000000000000000000000060a09081526100439160019190610056565b5034801561005057600080fd5b506100f1565b828054600181600116156101000203166002900490600052602060002090601f016020900481019282601f1061009757805160ff19168380011785556100c4565b828001600101855582156100c4579182015b828111156100c45782518255916020019190600101906100a9565b506100d09291506100d4565b5090565b6100ee91905b808211156100d057600081556001016100da565b90565b610338806101006000396000f3fe6080604052600436106100565763ffffffff7c01000000000000000000000000000000000000000000000000000000006000350416631c5d9faa811461005b578063967e6e6514610110578063abe4136f14610137575b600080fd5b34801561006757600080fd5b5061010e6004803603602081101561007e57600080fd5b81019060208101813564010000000081111561009957600080fd5b8201836020820111156100ab57600080fd5b803590602001918460018302840111640100000000831117156100cd57600080fd5b91908080601f0160208091040260200160405190810160405280939291908181526020018383808284376000920191909152509295506101c1945050505050565b005b34801561011c57600080fd5b506101256101d8565b60408051918252519081900360200190f35b34801561014357600080fd5b5061014c6101df565b6040805160208082528351818301528351919283929083019185019080838360005b8381101561018657818101518382015260200161016e565b50505050905090810190601f1680156101b35780820380516001836020036101000a031916815260200191505b509250505060405180910390f35b80516101d4906001906020840190610274565b5050565b6000545b90565b60018054604080516020601f6002600019610100878916150201909516949094049384018190048102820181019092528281526060939092909183018282801561026a5780601f1061023f5761010080835404028352916020019161026a565b820191906000526020600020905b81548152906001019060200180831161024d57829003601f168201915b5050505050905090565b828054600181600116156101000203166002900490600052602060002090601f016020900481019282601f106102b557805160ff19168380011785556102e2565b828001600101855582156102e2579182015b828111156102e25782518255916020019190600101906102c7565b506102ee9291506102f2565b5090565b6101dc91905b808211156102ee57600081556001016102f856fea165627a7a723058208c582212c275d0c3855b62b3cb43619e0389cc7ef234d69a2e9206b5728fda8b0029"
        }
    }
}
```

After that, the contract address is checked through the 14 interface (/v2/tx/get) as 0xb9b21d9000d6130b7ff5b53922aaf79582efb5c7





### 3. Contract release (v2) directly use code deployment

1. Use solidity language to write contracts.

2. In contractMap, the key is the contract name, and the value is the contract code.

3. If there are multiple contract files, one of the files must be named Main.sol --- the file where the main contract is located. Other xxx.sol dependent contracts of the main contract can be multiple, which need to be introduced in the header of the Main.sol file, for example: import "./xxx.sol"

4. If you are combining multiple contract file codes into one file, you need to specify the key as the contract name of the main contract, such as HelloWorld

5. **This interface does not return the contract address**. The contract address needs to be queried through the 3.14 interface based on the returned hash. If the transaction is successful (status=1), the contractAddress in the return result is the contract address on the chain.

Interface address: **/v2/contract/deploy**

Request method: **POST**
Request parameters:

| Parameter name | Required | Type | Description |
| ----------- | ---- | ------------------ | ------------- ----------------------------------------------- |
| businessId 	| Y | String 				| Business id, currently used to match the aes key of the corresponding 												business |
| from 			| Y | String 				| Transaction initiation address |
| chainId 		| Y | String 				| On which chain it happened |
| attach 		| F | String 				| Auxiliary information, this field will be returned when callback |
| contractMap 	| Y | Map<String,Object> 	| The json string after assembly of the contract's sol file |
| params 		| Y | Map<String,Object> 	| Contract construction method parameters {"a":"b","c":d..} |
| privateKey 	| Y | String 				| The private key corresponding to the encrypted from address, which 											needs to be encrypted with the aes key corresponding to the businessId |
| notifyUrl 	| F | String 				| After receiving the callback address notifyUrl, you need to return 											the following json to the server {result: "success"} |
| nonce 		| Y | String	 			| Initiating a contract needs to query the latest nonce corresponding 											to the address to initiate an operation |

Return parameter description

| Parameter name | Type | Description |
| ------ | ------ | -------- |
| code | String | Return code |
| msg | String | Return information |
| data | | Return data |

data:

| Parameter name | Type | Description |
| ------------ | ------ | -------- |
| msg | | Return information |
| hash | String | Hash |
| nonce | String | random number |
| contractJson | | Contract Data |

 

contractJson:

| Parameter name | Type | Description |
| ------------ | ------ | -------- |
| contractName | String | contract name |
| abi | String | Contract abi |
| bytecode | String | |

Request example

```json
{
    "businessId":"1",
    "from":"0x6a1fb9bfb756bf3d8aa28a189c8d0cb1b277809a",
    "chainId":"1",
    "attach":"1,2,3,4,5",
    "nonce":0,
    "params":{
    },
 "privateKey":"U28HRVeQCizyJ3SUtaqpkroysZ/hN4g8baLLZqKBHkSsbhbNfH+Fl7qxtQrhH1b9j60igdcbCZ4LyE2jwa9vdlN7SSCWK2W0f4jf7bEGkV0=",
    "notifyUrl":"http://localhost:8101/v1/test/",
    "contractMap":{
 "HelloWorld":"pragmasolidity>=0.5.0;\ncontractHelloWorld{\nuint256age=17;\nstringnickname=\"Hello\";\nfunctiongetAge()publicviewreturns(uint256data){\nreturnage;\n}\nfunctiongetNickname()publicviewreturns(stringmemorydata){\nreturnnickname;\n}\nfunctionsetNickname(stringmemorydata)public{\nnickname=data;\n}\n}"
    }
}
```

Reuurn example

```json
{
    "code":200,
    "msg":"success",
    "data":{
        "msg":"",
        "hash":"0x8e116ce9a742bcd99a223024f4832e9a6241baa3568a7093f7d91a1467449dcb",
        "nonce":"0",
        "contractJson":{
            "contractAddress":"",
            "contractName":"HelloWorld",
            "abi":"[{\"constant\":false,\"inputs\":[{\"name\":\"data\",\"type\":\"string\"}],\"name\":\"setNickname\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":true,\"inputs\":[],\"name\":\"getAge\",\"outputs\":[{\"name\":\"data\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"view\",\"type\":\"function\"},{\"constant\":true,\"inputs\":[],\"name\":\"getNickname\",\"outputs\":[{\"name\":\"data\",\"type\":\"string\"}],\"payable\":false,\"stateMutability\":\"view\",\"type\":\"function\"}]",
            "bytecode":"0x601160005560c0604052600560808190527f48656c6c6f00000000000000000000000000000000000000000000000000000060a09081526100439160019190610056565b5034801561005057600080fd5b506100f1565b828054600181600116156101000203166002900490600052602060002090601f016020900481019282601f1061009757805160ff19168380011785556100c4565b828001600101855582156100c4579182015b828111156100c45782518255916020019190600101906100a9565b506100d09291506100d4565b5090565b6100ee91905b808211156100d057600081556001016100da565b90565b610338806101006000396000f3fe6080604052600436106100565763ffffffff7c01000000000000000000000000000000000000000000000000000000006000350416631c5d9faa811461005b578063967e6e6514610110578063abe4136f14610137575b600080fd5b34801561006757600080fd5b5061010e6004803603602081101561007e57600080fd5b81019060208101813564010000000081111561009957600080fd5b8201836020820111156100ab57600080fd5b803590602001918460018302840111640100000000831117156100cd57600080fd5b91908080601f0160208091040260200160405190810160405280939291908181526020018383808284376000920191909152509295506101c1945050505050565b005b34801561011c57600080fd5b506101256101d8565b60408051918252519081900360200190f35b34801561014357600080fd5b5061014c6101df565b6040805160208082528351818301528351919283929083019185019080838360005b8381101561018657818101518382015260200161016e565b50505050905090810190601f1680156101b35780820380516001836020036101000a031916815260200191505b509250505060405180910390f35b80516101d4906001906020840190610274565b5050565b6000545b90565b60018054604080516020601f6002600019610100878916150201909516949094049384018190048102820181019092528281526060939092909183018282801561026a5780601f1061023f5761010080835404028352916020019161026a565b820191906000526020600020905b81548152906001019060200180831161024d57829003601f168201915b5050505050905090565b828054600181600116156101000203166002900490600052602060002090601f016020900481019282601f106102b557805160ff19168380011785556102e2565b828001600101855582156102e2579182015b828111156102e25782518255916020019190600101906102c7565b506102ee9291506102f2565b5090565b6101dc91905b808211156102ee57600081556001016102f856fea165627a7a723058201ed3aaf8d9869c0147c5b75df033d80a9395b8b08ea1fa3a108545951e019c1b0029"
        }
    }
}
```

After checking the 14 interface, the contract address is 0x41ae171f6693911cc2e4ff45d5ee6160f3523b9b



### 4. Contract transaction (v2)

Contract transactions are used to call all methods in the contract that will cause the data state to change.

Interface address: **/v2/contract/send**

Request method: **POST**
Request parameters:

| Parameter name | Required | Type | Description |
| ------------ | ---- | ------------------ | ------------ ------------------------------------------------ |
| businessId 	| Y | String | Business id, currently used to match the aes key of the corresponding business |
| from 			| Y | String | Transaction initiation address |
| chainId 		| Y | String | On which chain it happened |
| attach 		| F | String | Auxiliary information, used in conjunction with notify, this field will be returned 								when callback |
| nonce 		| Y | String | Initiating a contract needs to query the latest nonce corresponding to the address 								to initiate an operation |
| function 		| Y | Map<String,Object> | {"name":"method name","params":[{"a":"b"},{"c":"d"}..]} |
| privateKey 	| Y | String | The private key corresponding to the encrypted from address, which needs to be 									encrypted with the aes key corresponding to the businessId |
| notifyUrl 	| F | String | Callback address notifyUrl After receiving, you need to return the following json to 								the server {result: "success"} |
| contractJson 	| Y | json | {"contractAddress":"","contractName":"","abi":"","bytecode":""} |

contractJson:

| Parameter name | Required | Type | Description |
| --------------- | ---- | ------ | ---------------- |
| contractAddress 	| Y | String | Contract address to be called |
| abi 				| Y | String | Contract abi |

Return parameter description

| Parameter name | Type | Description |
| ------ | ------ | -------- |
| code 	| String 	| Return code |
| msg 	| String 	| Return information |
| data 	| 			| Return data |

data:

| Parameter name | Type | Description |
| ------ | ------ | ----------- |
| msg 	| 			| Return information |
| hash 	| String 	| Hash |
| nonce | String 	| Transaction nonce value |

Request example

```json
{
    "businessId":"1",
    "chainId":"1",
    "from":"0x6a1fb9bfb756bf3d8aa28a189c8d0cb1b277809a",
    "attach":"",
    "nonce":1,
    "function":{
        "name":"setNickname",
        "params":{
            "data":"chain"
        }
    },
 "privateKey":"U28HRVeQCizyJ3SUtaqpkroysZ/hN4g8baLLZqKBHkSsbhbNfH+Fl7qxtQrhH1b9j60igdcbCZ4LyE2jwa9vdlN7SSCWK2W0f4jf7bEGkV0=",
    "notifyUrl":"",
    "contract":{
        "contractAddress":"0x41ae171f6693911cc2e4ff45d5ee6160f3523b9b",
        "abi":"[{\"constant\":true,\"inputs\":[],\"name\":\"getAge\",\"outputs\":[{\"internalType\":\"uint256\",\"name\":\"data\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"view\",\"type\":\"function\"},{\"constant\":true,\"inputs\":[],\"name\":\"getNickname\",\"outputs\":[{\"internalType\":\"string\",\"name\":\"data\",\"type\":\"string\"}],\"payable\":false,\"stateMutability\":\"view\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"internalType\":\"string\",\"name\":\"data\",\"type\":\"string\"}],\"name\":\"setNickname\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"}]"
    }
}
```

Return example

```json
{
    "code":200,
    "msg":"success",
    "data":{
        "msg":"",
        "hash":"0xd036f76b8658bebca7c919160195df371777bcc530b7359ece31b4963f3575bd",
        "nonce":"1"
    }
}
```



### 5. Contract call (v2)

Contract call, that is, call all methods in the contract that only view the data status.

No data modification will occur in the contract call, and the returned hash can be ignored.

Interface address: **/v2/contract/call**

Request method: **POST**
Request parameters:

| Parameter name | Required | Type | Description |
| ------------ | ---- | ------------------ | ------------ ------------------------------------------------ |
| businessId 	| Y | String | Business id, currently used to match the aes key of the corresponding business |
| from 			| Y | String | Transaction initiation address |
| chainId 		| Y | String | On which chain it happened |
| nonce 		| Y | String | Latest nonce value of transaction origination address |
| function 		| Y | Map<String,Object> | {"name":"method name","params":[{"a":"b"},{"c":"d"}..]} |
| privateKey 	| Y | String | The private key corresponding to the encrypted from address, which needs to be 							encrypted with the aes key corresponding to the businessId |
| contractJson | Y | json | {"contractAddress":"","abi":""} |

contractJson:

| Parameter name | Required | Type | Description |
| --------------- | ---- | ------ | ---------------- |
| contractAddress 	| Y | String | Contract address to be called |
| abi 				| Y | String | Contract abi |

Return parameter description

| Parameter name | Type | Description |
| ------ | ------ | -------- |
| code 	| String 	| Return code |
| msg 	| String 	| Return information |
| data 	| 			| Return data |

data:

| Parameter name | Type | Description |
| ------ | ---- | -------- |
| msg 	| | Return information |
| value | | Return data |

Request example
```json
{
    "businessId":"1",
    "chainId":"1",
    "from":"0x6a1fb9bfb756bf3d8aa28a189c8d0cb1b277809a",
    "nonce":4,
    "function":{
        "name":"getNickname",
        "params":{
        }
    },
 "privateKey":"U28HRVeQCizyJ3SUtaqpkroysZ/hN4g8baLLZqKBHkSsbhbNfH+Fl7qxtQrhH1b9j60igdcbCZ4LyE2jwa9vdlN7SSCWK2W0f4jf7bEGkV0=",
    "contract":{
        "contractAddress":"0x41ae171f6693911cc2e4ff45d5ee6160f3523b9b",
        "abi":"[{\"constant\":true,\"inputs\":[],\"name\":\"getAge\",\"outputs\":[{\"internalType\":\"uint256\",\"name\":\"data\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"view\",\"type\":\"function\"},{\"constant\":true,\"inputs\":[],\"name\":\"getNickname\",\"outputs\":[{\"internalType\":\"string\",\"name\":\"data\",\"type\":\"string\"}],\"payable\":false,\"stateMutability\":\"view\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"internalType\":\"string\",\"name\":\"data\",\"type\":\"string\"}],\"name\":\"setNickname\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"}]"
    }
}
```

Return example

```json
{
    "code":200,
    "msg":"success",
    "data":{
        "msg":"success",
        "hash":"0xe383006c50df6893b13f82c613709b3587c5733cca06d63eae59d97609d73dce",
        "value":{
            "data":"中国"
        },
        "nonce":"4"
    }
}
```


### 6. Encryption

Note: For testing, please use the local AES tool for encryption and decryption in production

Interface address: **/v1/key/encrypt**

Request method: **POST**
Request parameters:

| Parameter name | Required | Type | Description |
| ---------- | ---- | ------ | -------------------------- ----------- |
| businessId 	| Y | String | Business id, currently used to match the aes key of the corresponding business |
| value 		| Y | String | Data to be encrypted |

Return parameter description

| Parameter name | Type | Description |
| ------ | ------ | -------- |
| code 	| String 	| Return code |
| msg 	| String 	| Return information |
| data 	| 			| Return data |

Request example

```json
{
      "businessId":"1",
      "value":"265befdd607cdf7ff9bccab9b3b7815d4f96680e5afb73d25ff5974309757fba"
}
```

Return example

```json
{
    "code": 200,
    "msg": "success",
    "data": "U28HRVeQCizyJ3SUtaqpkroysZ/hN4g8baLLZqKBHkSsbhbNfH+Fl7qxtQrhH1b9j60igdcbCZ4LyE2jwa9vdlN7SSCWK2W0f4jf7bEGkV0="
}
```



### 7. Decryption

Note: For testing, please use the local AES tool for encryption and decryption in production

Interface address: **/v1/key/decrypt**

Request method: **POST**
Request parameters:

| Parameter name | Required | Type | Description |
| ---------- | ---- | ------ | -------------------------- ----------- |
| businessId 	| Y | String | Business id, currently used to match the aes key of the corresponding business |
| value 		| Y | String | Data to be decrypted |

Return parameter description

| Parameter name | Type | Description |
| ------ | ------ | -------- |
| code 	| String 	| Return code |
| msg 	| String 	| Return information |
| data 	| 			| Return data |

Request example

```json
{
      "businessId":"1",
 "encryptedValue":"U28HRVeQCizyJ3SUtaqpkroysZ/hN4g8baLLZqKBHkSsbhbNfH+Fl7qxtQrhH1b9j60igdcbCZ4LyE2jwa9vdlN7SSCWK2W0f4jf7bEGkV0="
}
```

Return example

```json
{
    "code": 200,
    "msg": "success",
    "data": "265befdd607cdf7ff9bccab9b3b7815d4f96680e5afb73d25ff5974309757fba"
}
```


### 8. Return public key and address via private key

Note: For testing, use 3.10 for production

Interface address: **/v1/key/to/address**

Request method: **POST**
Request parameters:

| Parameter name | Required | Type | Description |
| ------ | ---- | ------ | ---- |
| key | Y | String | Private key |

Return parameter description

| Parameter name | Type | Description |
| ------ | ------ | -------- |
| code 	| String 	| Return code |
| msg 	| String 	| Return information |
| data 	| 			| Return data |

data:

| Parameter name | Type | Description |
| ---------- | ------ | ---- |
| privateKey| String | Private Key |
| publicKey | String | Public Key |
| address 	| String | Address |

Request example

```json
{
   "key":"265befdd607cdf7ff9bccab9b3b7815d4f96680e5afb73d25ff5974309757fba"
}
```

Return example

```json
{
    "code": 200,
    "msg": "success",
    "data": {
        "privateKey": "265befdd607cdf7ff9bccab9b3b7815d4f96680e5afb73d25ff5974309757fba",
        "publicKey": "0x04c4591e2ae74d5c58157eb20a569785c6f4c739d8600673b5a0ee459f5335c743b550b7f73478c1cf5b49d53f1be67fffa5db1f72d6dc2214e054cf7151c4772e",
        "address": "0x6a1fb9bfb756bf3d8aa28a189c8d0cb1b277809a"
    }
}
```


### 9. Public key and address (through encrypted private key)

Interface address: **/v1/key/encrypt/to/address**

Request method: **POST**
Request parameters:

| Parameter name | Required | Type | Description |
| ---------- | ---- | ------ | -------------------------- ----------------------- |
| businessId | Y | String | Business id, currently used to match the aes key of the corresponding business |
| keyEncrypt | Y | String | The encrypted private key needs to be encrypted with the aes key corresponding to the 							businessId |

Return parameter description

| Parameter name | Type | Description |
| ------ | ------ | -------- |
| code 	| String 	| Return code |
| msg 	| String 	| Return information |
| data 	| 			| Return data |

data:

| Parameter name | Type | Description |
| ---------- | ------ | ---- |
| privateKey| String | Private Key |
| publicKey | String | Public Key |
| address 	| String | Address |

Request example

```json
{
     "businessId":"1",
 "keyEncrypt":"U28HRVeQCizyJ3SUtaqpkroysZ/hN4g8baLLZqKBHkSsbhbNfH+Fl7qxtQrhH1b9j60igdcbCZ4LyE2jwa9vdlN7SSCWK2W0f4jf7bEGkV0="
}
```
Return example

```json
{
    "code": 200,
    "msg": "success",
    "data": {
        "privateKey": "U28HRVeQCizyJ3SUtaqpkroysZ/hN4g8baLLZqKBHkSsbhbNfH+Fl7qxtQrhH1b9j60igdcbCZ4LyE2jwa9vdlN7SSCWK2W0f4jf7bEGkV0=",
        "publicKey": "0x04c4591e2ae74d5c58157eb20a569785c6f4c739d8600673b5a0ee459f5335c743b550b7f73478c1cf5b49d53f1be67fffa5db1f72d6dc2214e054cf7151c4772e",
        "address": "0x6a1fb9bfb756bf3d8aa28a189c8d0cb1b277809a"
    }
}
```



### 10. Generate public and private keys

Note: For testing, please use 3.12 for production

Interface address: **/v1/key/gen**

Request method: **GET**
Request parameters:

  without

Return parameter description

| Parameter name | Type | Description |
| ------ | ------ | -------- |
| code 	| String 	| Return code |
| msg 	| String 	| Return information |
| data 	| 			| Return data |

data:

| Parameter name | Type | Description |
| ---------- | ------ | ---- |
| privateKey| String | Private Key |
| publicKey | String | Public Key |
| address 	| String | Address |


Request example



Return example

```json
{
    "code": 200,
    "msg": "success",
    "data": {
        "privateKey": "265befdd607cdf7ff9bccab9b3b7815d4f96680e5afb73d25ff5974309757fba",
        "publicKey": "0x04c4591e2ae74d5c58157eb20a569785c6f4c739d8600673b5a0ee459f5335c743b550b7f73478c1cf5b49d53f1be67fffa5db1f72d6dc2214e054cf7151c4772e",
        "address": "0x6a1fb9bfb756bf3d8aa28a189c8d0cb1b277809a"
    }
}
```



### 11.Generate public and private keys (encryption)

Note: return the encrypted public and private keys

Interface address: **/v1/key/gen/signed**

Request method: **POST**
Request parameters:

| Parameter name | Required | Type | Description |
| ---------- | ---- | ------ | -------------------------- ----------- |
| businessId | Y | String | Business id, currently used to match the aes key of the corresponding business |

Return parameter description

| Parameter name | Type | Description |
| ------ | ------ | -------- |
| code 	| String 	| Return code |
| msg 	| String 	| Return information |
| data 	| 			| Return data |

data:

| Parameter name | Type | Description |
| ---------- | ------ | ---- |
| privateKey| String | Private Key |
| publicKey | String | Public Key |
| address 	| String | Address |

Request example

```json
{
	"businessId": "1"
}
```

Return example

```json
{
    "code": 200,
    "msg": "success",
    "data": {
        "privateKey": "OThruwzX8UhJXZon8y1G9RAIrDTNDdH5UcGO5fYmXIzczg5f6UHq8V2VA0fcOOxNe1L2Gfx4Ra0+JX9xequP5ewqciFqhmD4fDeCAboafOw=",
        "publicKey": "f3xFt2oTP1og4zCPlp2NHIIK42KtiWTNPc+NFTK6U3hPr7vDRg3lNu6N8wsjurAe7MYbZxFXTVlaHzQkxYRWBwnu9WWauMV52Yy9DN2yj5Oxkpja1Yx0NT1i5FQ7FaZLyAkOaKHpgG3dy+Qhy/xrbAApM5yurTb0bOdpJF9grnqmS3PKDiBFBl5Bz6kSmJpm",
        "address": "0x13ae763822e051aa054fa763f6fe1b1ff0596025"
    }
}
```


### 12. Reverse input according to contract abi

Interface address: **/v1/tx/input/unpack**

Request method: **POST**
Request parameters:

| Parameter name | Required | Type | Description |
| ---------- | ---- | ------ | -------------------------- ----------------------- |
| input 	| Y | String | The input that needs to be inverted |
| contract 	| Y | Map<String,Object> | The encrypted private key needs to be encrypted with the aes key 						corresponding to the businessId |

contract:
| Parameter name | Required | Type | Description |
| ---------- | ---- | ------ | -------------------------- ----------------------- |
| abi | Y | String | Contract abi |

Return parameter description

| Parameter name | Type | Description |
| ------ | ------ | -------- |
| code 	| String 	| Return code |
| msg 	| String 	| Return information |
| data 	| 			| Return data |

data:

| Parameter name | Type | Description |
| ---------- | ------ | ---- |
| method 	| String | Invoke method |
| inputmap 	| Map<String,Object> | |

Request example

```json
{
    "input": "0x95f3660400000000000000000000000000000000000000000000000000000000000000200000000000000000000000000000000000000000000000000000000000000006e4b8ade59bbd0000000000000000000000000000000000000000000000000000", 
    "contract": {
        "abi": "[{\"constant\":true,\"inputs\":[],\"name\":\"getAge\",\"outputs\":[{\"internalType\":\"uint256\",\"name\":\"data\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"view\",\"type\":\"function\"},{\"constant\":true,\"inputs\":[],\"name\":\"getNickname\",\"outputs\":[{\"internalType\":\"string\",\"name\":\"data\",\"type\":\"string\"}],\"payable\":false,\"stateMutability\":\"view\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"internalType\":\"string\",\"name\":\"data\",\"type\":\"string\"}],\"name\":\"setNickname\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"}]"
}
}
```

Return example

```json
{
    "code": 200, 
    "msg": "success", 
    "data": {
        "method": "setNickname", 
        "inputmap": {
            "data": "chain"
        }
}
}
```

### 13. Query transaction details based on transaction hash (V1)
Note: This interface is only used to query transaction details, you should use this interface to query transaction results in production

Interface address: **/v1/tx/get**

Request method: **POST**
Request parameters:

| Parameter name | Required | Type | Description |
| ---------- | ---- | ------ | -------------------------- ----------------------- |
| chainId 	| Y | String | Chain ID |
| hash 		| Y | String | Transaction hash |

Return parameter description

| Parameter name | Type | Description |
| ------ | ------ | -------- |
| code 		| String 	| Return code |
| msg 		| String 	| Return information |
| data 		| 			| Return data |

data:
| Parameter name | Type | Description |
| ---------- | ------ | ---- |
| blockHeight 		| Int 		| Packing block height |
| contractAddress 	| String 	| Contract Address |
| logs 				| list 		| Time set |
| out 				| 			| If it is a contract transaction, the contract execution result |
| root 				| 			|
| status 			| 			| Transaction status 1 is successful 0 failed |
| transactionHash 	| String 	| Transaction hash |
| tx 				| 			| Transaction details |
| errorMsg 			| String 	| Error message |

Logs:
| Parameter name | Type | Description |
| ---------- | ------ | ---- |
| address 			| String 		| Address |
| blockNumber 		|	Int 		| Block height |
| contractName 		| String 		| |
| data 				| String 		| |
| event 			| list 			| |
| logIndex 			| String 		| |
| topics 			| List:String 	| |
| transactionHash 	| String 		| |
| transactionIndex 	| String 		| Call method |

tx:
| Parameter name | Type | Description |
| ---------- | ------ | ---- |
| chainid 	| String 	| |
| extra 	| 			| gas fee |
| from 		| String 	| Transaction initiation address |
| hash 		| String 	| |
| input 	| 			| |
| inputValue| Map<String,Object>| inpu after inverse solution |
| nonce 	| 			| |
| timestamp | String 	| Timestamp |
| to 		| String 	| Accepted Address |
| uselocal 	| String 	| |
| value 	| String 	| Amount |

Request example

```json
{
    "chainId" : "1",
    "hash":"0xd036f76b8658bebca7c919160195df371777bcc530b7359ece31b4963f3575bd"
}
```

Return example

```json
{
    "code": 200,
    "msg": "success",
    "data": {
        "blockHeight": 10234537,
        "contractAddress": "0x0000000000000000000000000000000000000000",
        "errorMsg": "",
        "gasFee": "13050400000000000",
        "gasFeeValue": 0.0130504,
        "gasUsed": 32626,
        "logs": null,
        "out": "0x",
        "root": "eyJmZWUiOiIxMzA1MDQwMDAwMDAwMDAwMCIsInJvb3QiOm51bGx9",
        "status": 1,
        "transactionHash": "0xd036f76b8658bebca7c919160195df371777bcc530b7359ece31b4963f3575bd",
        "tx": {
            "chainid": 1,
            "extra": "0x",
            "from": "0x6a1fb9bfb756bf3d8aa28a189c8d0cb1b277809a",
            "hash": "",
            "input": "0x1c5d9faa00000000000000000000000000000000000000000000000000000000000000200000000000000000000000000000000000000000000000000000000000000006e4b8ade59bbd0000000000000000000000000000000000000000000000000000",
            "nonce": 1,
            "timestamp": 0,
            "to": "0x41ae171f6693911cc2e4ff45d5ee6160f3523b9b",
            "uselocal": false,
            "value": 0
        }
    }
}
```

### 14. Query transaction details based on transaction hash (V2)
Note: This interface automatically reverses the contract transaction results and call parameters. If the contract is not registered or is not a contract transaction, an error will be reported. Therefore, this interface is not recommended in production and is only suitable for auxiliary docking

Interface address: **/v2/tx/get**

Request method: **POST**
Request parameters:

| Parameter name | Required | Type | Description |
| ---------- | ---- | ------ | -------------------------- ----------------------- |
| chainId 	| Y | String | Chain ID |
| hash 		| Y | String | Transaction hash |

Return parameter description

| Parameter name | Type | Description |
| ------ | ------ | -------- |
| code 		| String 	| Return code |
| msg 		| String 	| Return information |
| data 		| 			| Return data |

data:
| Parameter name | Type | Description |
| ---------- | ------ | ---- |
| blockHeight 		| Int 	| Packing block height |
| contractAddress 	| String| Contract Address |
| logs 				| list 	| Time set |
| out 				| 		| If it is a contract transaction, the contract execution result |
| root 				| 		| Call method |
| status 			| 		| Transaction status 1 is successful 0 failed |
| transactionHash 	| String| Transaction hash |
| tx 				| 		| Transaction details |
| errorMsg 			| String| Error message |
| outValue 			| String| Out corresponding inverse solution information |

Logs:
| Parameter name | Type | Description |
| ---------- | ------ | ---- |
| address 			| String | Address |
| blockNumber 		| Int | Block height |
| contractName 		| String | Registered contract name |
| data		 		| String | Event non-indexed parameters |
| event 			| list | Event after reverse solution |
| logIndex 			| String | Event Index |
| topics 			| List:String | The first data is the hash of the event signature, and the rest are the event 									parameters of the index |
| transactionHash 	| String | |
| transactionIndex 	| String | Call method |

tx:
| Parameter name | Type | Description |
| ---------- | ------ | ---- |
| chainid 		| String 	| |
| extra 		| 			| gas fee |
| from 			| String 	| Transaction initiation address |
| hash 			| String 	| |
| input 		| 			| |
| inputValue 	| Map<String,Object>| inpu after inverse solution |
| nonce 		| 			| transaction nonce |
| timestamp 	| String 	| Timestamp |
| to 			| String 	| Accepted Address |
| uselocal 		| String 	| |
| value 		| String 	| Amount |

Request example


```json
{
    "chainId" : "1",
    "hash":"0xd036f76b8658bebca7c919160195df371777bcc530b7359ece31b4963f3575bd"
}
```

Return example

```json
{
    "code": 200,
    "msg": "success",
    "data": {
        "blockHeight": 10234537,
        "contractAddress": "0x0000000000000000000000000000000000000000",
        "contractName": "HelloWorld",
        "errorMsg": "",
        "gasFee": "13050400000000000",
        "gasFeeValue": 0.0130504,
        "gasUsed": 32626,
        "logs": null,
        "out": "0x",
        "root": "eyJmZWUiOiIxMzA1MDQwMDAwMDAwMDAwMCIsInJvb3QiOm51bGx9",
        "status": 1,
        "transactionHash": "0xd036f76b8658bebca7c919160195df371777bcc530b7359ece31b4963f3575bd",
        "tx": {
            "chainid": 1,
            "extra": "0x",
            "from": "0x6a1fb9bfb756bf3d8aa28a189c8d0cb1b277809a",
            "hash": "",
            "input": "0x1c5d9faa00000000000000000000000000000000000000000000000000000000000000200000000000000000000000000000000000000000000000000000000000000006e4b8ade59bbd0000000000000000000000000000000000000000000000000000",
            "inputValue": {
                "data": "中国"
            },
            "method": "setNickname",
            "nonce": 1,
            "timestamp": 0,
            "to": "0x41ae171f6693911cc2e4ff45d5ee6160f3523b9b",
            "uselocal": false,
            "value": 0
        }
    }
}
```

### 15. Get all chain information

Interface address: **/v1/chain/get/info**

Request method: **POST**
Request parameters:

| Parameter name | Required | Type | Description |
| ---------- | ---- | ------ | -------------------------- ----------------------- |
| chainIds | Y | list | Chain ID |

Return parameter description

| Parameter name | Type | Description |
| ------ | ------ | -------- |
| code 		| String 	| Return code |
| msg 		| String 	| Return information |
| data 		| 			| Return data |

data:
| Parameter name | Type | Description |
| ---------- | ------ | ---- |
| chainId | Int | |
| datanodes | list | |
| mode | Int | |
| parent | Int | |

datanodes:
| Parameter name | Type | Description |
| ---------- | ------ | ---- |
| dataNodeId | String | Node id |
| dataNodeIp | String | Node ip |
| dataNodePort | String | Node Port |

Request example
```json
{
     "chainIds": []
}
```

Return example

```json
{
    "code": 200,
    "msg": "success",
    "data": [
        {
            "chainId": 0,
            "datanodes": [
                {
                    "dataNodeId": "0x3224de0da639511fec588d2e28f4472476b1600d003a10e38e0456426337624aaecd6636e5ce7ff95fc10746471ce7b680f664ccbf17057ca18c761706afa391",
                    "dataNodeIp": "192.168.1.11",
                    "dataNodePort": 23021
                }
            ],
            "mode": 17,
            "parent": 1048576
        },
        {
            "chainId": 1,
            "datanodes": [
                {
                    "dataNodeId": "0xf236c00e5c1fd175e2ecfe3ccc29dcf27caafe82d4f532b20b64e34b0bb1d132ffd5efaa8e3b2316ccf3f4d9b2112213b01c792f107bd0565be7ac3d506bf31f",
                    "dataNodeIp": "192.168.1.11",
                    "dataNodePort": 23026
                }
            ],
            "mode": 18,
            "parent": 0
        },
        {
            "chainId": 2,
            "datanodes": [
                {
                    "dataNodeId": "0xa9d8dd87c9ece1787cbb16ba179df6d1d4b29580c03ae1da6e4634b154f8e2feb052fc1c07ca1e362f9b3e2b5f43822df9dd6578e782701de83afeca91a7b453",
                    "dataNodeIp": "192.168.1.12",
                    "dataNodePort": 23021
                }
            ],
            "mode": 18,
            "parent": 0
        },
        {
            "chainId": 103,
            "datanodes": [
                {
                    "dataNodeId": "0x44c98ab831f3ca4553e491bba06753e959ceb55d43e18bc76539572feb1e0dbaf2fbfc19f571d6544e82be1c7c39760f6a023d4be4dcb9473dd580c731d03926",
                    "dataNodeIp": "192.168.1.12",
                    "dataNodePort": 23026
                }
            ],
            "mode": 18,
            "parent": 0
        }
    ]
}
```

### 16. Get current information about the chain

Interface address: **/v1/chain/get/stats**

Request method: **POST**
Request parameters:

| Parameter name | Required | Type | Description |
| ---------- | ---- | ------ | -------------------------- ----------------------- |
| chainId | Y | String | Chain ID |

Return parameter description

| Parameter name | Type | Description |
| ------ | ------ | -------- |
| code 		| String 	| Return code |
| msg 		| String 	| Return information |
| data 		| 			| Return data |

data:
| Parameter name | Type | Description |
| ---------- | ------ | ---- |
| N 				| String 		| Number of Accounts |
| accountcount 		| Int 			| |
| currentcomm 		| List:String 	| |
| currentheight 	| Long 			| current height |
| epochduration 	| Int 			| epoch duration |
| accountcount 		| Int 			| |
| limit 			| Long 			| least |
| price 			| String 		| |
| lastNduration 	| Int 			| Last Duration |
| lastepochduration | Int 			| Last epoch duration |
| lives 			| Int 			| |
| tps 				| Int 			| |
| tpsLastEpoch 		| Int 			| |
| tpsLastN 			| Int 			| |
| txcount 			| Int 			| Number of transactions |
| version 			| String 		| Version |

Request example

```json
{
     "chainId": "1"
}
```

Return example

```json
{
    "code": 200,
    "msg": "success",
    "data": {
        "chainId": 0,
        "currentheight": 10235029,
        "epochduration": 2603,
        "epochlength": 1000,
        "gaslimit": 2500000,
        "gasprice": "400000000000",
        "lastepochduration": 2595,
        "lives": 1635307,
        "tps": 0,
        "tpsLastEpoch": 0,
        "n": 10,
        "tpsLastN": 0,
        "lastNduration": 26,
        "txcount": 506,
        "accountcount": 0,
        "currentcomm": [
            "0x025779691bd93cc460e761ad2e8f5900a33a47112322c5503ee5d944e3aa7445b4efbb544881c13284d304c8c8cf0f0804ddc498be550555776fe15b714406ca",
            "0x4f47e053cb4f4ff38fc52d9bfb7342b39edd7ef72f7f6cce22b2fa8a3b2656afec9076c239251d2b229245765c1dca005fb448f05e9ea946f40db9908d37abb4",
            "0x783f4b2490461ecfd8ee8d3451e434de06bacb0ffff56de53a33fe545589094fa0b929eeaa62dc5203d1e831ccdd37d206d0b85b193921efb223bf0cb2f37b4c",
            "0x9855b69ea2ff6b419de14b2ba18910e2427d251a3ffa453d9307a01dbabc213ef08cfad7459538dac14407046048bdd9f936ba317708b3f07a62782a2be6cca7"
        ]
    }
}
```

### 17. Obtain chain committee information

Interface address: **/v1/chain/get/committee**

Request method: **POST**
Request parameters:

| Parameter name | Required | Type | Description |
| ---------- | ---- | ------ | -------------------------- ----------------------- |
| chainId | Y | String | Chain ID |
| epoch | Y | String | Number of elections |

Return parameter description

| Parameter name | Type | Description |
| ------ | ------ | -------- |
| code 	| String 		| Return code |
| msg	| String 		| Return information |
| data 	| List:String 	| Return data, node id |

Request example

```json
{
     "chainId": "1",
     "epoch": "1"
}
```

Return example

```json
{
    "code": 200,
    "msg": "success",
    "data": [
        "0xe90a151759bf070969aae664e00502bb08568c85a73874492a3ec480c5178d5da29c790896fc62106e32d172819dec94202ff90f3b7ba3e6adf38508bc58cf43",
        "0x783f4b2490461ecfd8ee8d3451e434de06bacb0ffff56de53a33fe545589094fa0b929eeaa62dc5203d1e831ccdd37d206d0b85b193921efb223bf0cb2f37b4c",
        "0x6e4a2f626a7d6dd082b713acdd3be49872097ab79f664f807095f665a50c68803688d1a242c8580ce6e8355468f666d1d43e3bdb0deebd0df17f97e1ea397355",
        "0x025779691bd93cc460e761ad2e8f5900a33a47112322c5503ee5d944e3aa7445b4efbb544881c13284d304c8c8cf0f0804ddc498be550555776fe15b714406ca",
        "0x4f47e053cb4f4ff38fc52d9bfb7342b39edd7ef72f7f6cce22b2fa8a3b2656afec9076c239251d2b229245765c1dca005fb448f05e9ea946f40db9908d37abb4",
        "0x9855b69ea2ff6b419de14b2ba18910e2427d251a3ffa453d9307a01dbabc213ef08cfad7459538dac14407046048bdd9f936ba317708b3f07a62782a2be6cca7",
        "0xa93b150f11c422d8700554859281be8e34a91a859e0e021af186002c7e4a2661ea2467a63b417030d68e2fdddeb4342943dff13225da77124abf912fd092f71f"
    ]
}
```

### 18. Get block transaction

Interface address: **/v1/block/txs/get**

Request method: **POST**
Request parameters:

| Parameter name | Required | Type | Description |
| ---------- | ---- | ------ | -------------------------- ----------------------- |
| chainId | Y | String | Chain ID |
| height | Y | String | Block height |
| page | Y | String | Page number |
| size | Y | String | Page size |

Return parameter description

| Parameter name | Type | Description |
| ------ | ------ | -------- |
| code 		| String 	| Return code |
| msg 		| String 	| Return information |
| data 		| 			| Return data |

data:
| Parameter name | Type | Description |
| ------ | ------ | -------- |
| elections 		| String 	| |
| accountchanges 	| list 		| |

accountchanges:
| Parameter name | Type | Description |
| ------ | ------ | -------- |
| chainid 	| Int 		| Issuer |
| hash 		| String 	| transaction hash |
| from 		| String 	| Transaction initiation address |
| extra 	| String 	| |
| input 	| String 	| |
| nonce 	| Int 		| nonce when trading |
| timestamp | Long 		| Transaction time |
| to 		| String 	| Recipient |
| uselocal 	| boolean 	| |
| value 	| Int 		| |


Request example

```json
{
     "chainId": "103",
     "height": "10270887",
     "page": "1",
     "size": "10"
}
```

Return example

```json
{
    "code": 200,
    "msg": "success",
    "data": {
        "elections": null,
        "accountchanges": [
            {
                "chainid": 103,
                "from": "0x9ae84284d7b152af900281c9e3969c8770197459",
                "to": "0x7476313b9ec8a54dcbb4070514b4f0e4da8a1d2b",
                "nonce": 222,
                "value": 0,
                "input": "0x8803dbee0000000000000000000000000000000000000000000000000de0b6b3a764000000000000000000000000000000000000000000000000000001b2b83a8117897100000000000000000000000000000000000000000000000000000000000000a00000000000000000000000009ae84284d7b152af900281c9e3969c8770197459000000000000000000000000000000000000000000000000000000005fbb8ed20000000000000000000000000000000000000000000000000000000000000002000000000000000000000000d9de66aacfc0872f3814c85f8771bbb2be01d582000000000000000000000000cfd5c7b893555b3bb48d4d2682af0016ae3509fb",
                "hash": "0xd3d79de66a2e19ad864c1a5b9f23ff66402ba2aa632679003664486848062eda",
                "uselocal": false,
                "extra": "0x7b22676173223a363030303030307d",
                "timestamp": 1606127019
            }
        ]
    }
}
```

### 19. Get block header information

Interface address: **/v1/block/header/get**

Request method: **POST**
Request parameters:

| Parameter name | Required | Type | Description |
| ---------- | ---- | ------ | -------------------------- ----------------------- |
| chainId 	| Y | String | Chain ID |
| height 	| Y | String | Block height |

Return parameter description

| Parameter name | Type | Description |
| ------ | ------ | -------- |
| code 		| String 	| Return code |
| msg 		| String 	| Return information |
| data 		| 			| Return data |

data:
| Parameter name | Type | Description |
| ------ | ------ | -------- |
| elections 		| String | |
| accountchanges 	| list | |

accountchanges:
| Parameter name | Type | Description |
| ------ | ------ | -------- |
| chainid 		| Int 		| Issuer |
| deltaroot 	| 			| |
| empty 		| boolean 	| |
| hash 			| String 	| transaction hash |
| height 		| Int 		| Block height |
| mergeroot 	| 			| |
| previoushash 	| String 	| |
| rewardaddress | String 	| Award address |
| rrera 		| 			| |
| rrnext 		| 			| |
| stateroot 	| String	| |
| timestamp 	| Long 		| |
| txcount 		| Int 		| How many transactions occurred in this block |


Request example

```json
{
     "chainId": "103",
     "height": "10270887"
}
```

Return example

```json
{
    "code": 200,
    "msg": "success",
    "data": {
        "hash": "0x8d9773300e165eb0812c7647134dba0ce655984e30d34151ceb5540f2bc39033",
        "previoushash": "0x72c9df3c81e4013705b4b4a0d606f5593222e0016a0515243ce65181f6235301",
        "chainid": 103,
        "height": 10270887,
        "empty": false,
        "rewardaddress": "0x0b70e6f67512bcd07b7d1cbbd04dbbfadfbeaf37",
        "mergeroot": "",
        "deltaroot": "",
        "stateroot": "0xfd796ee38a0a62c91ee6afa1d7aaa67cc5f2c3eae23ab4648f18b6bdc30037a3",
        "rrera": 0,
        "rrcurrent": "",
        "rrnext": "",
        "txcount": 1,
        "timestamp": 1606127019,
        "ErrMsg": ""
    }
}
```

### 20. Perform main currency transactions
Note: This interface simply supports cross-chain transactions. ToChainId that is different from chainId is passed in. Cross-chain transactions consist of multiple steps. Failure in any of these steps will cause the final cross-chain transaction to fail.

Interface address: **/v1/tx/send**

Request method: **POST**
Request parameters:

| Parameter name | Required | Type | Description |
| ---------- | ---- | ------ | -------------------------- ----------------------- |
| bussinessId 	| Y | String | Service id |
| chainId 		| Y | String | Chain id |
| fromChainId 	| Y | String | Transfer chain id (same as chainId, cross-chain transaction) |
| toChainId 	| Y | String | Transfer chain id (cross-chain transaction) |
| from 			| Y | String | Outgoing address |
| to 			| Y | String | Transfer address |
| value 		| Y | Int 	 | Number of transactions |
| nonce 		| Y | Int 	 | transaction nonce |
| attach 		| Y | String | Business parameters |
| privateKey 	| Y | String | Encrypted private key |
| notifyUrl 	| Y | String | Callback address |

Return parameter description

| Parameter name | Type | Description |
| ------ | ------ | -------- |
| code 		| String 	| Return code |
| msg 		| String 	| Return information |
| data 		| 			| Return data |

data:
| Parameter name | Type | Description |
| ------ | ------ | -------- |
| Msg 	| String 	| Prompt Information |
| Hash 	| String 	| Transaction hash |
| Nonce | Int 		| nonce after transaction |

Request example

```json
{
     "businessId": "1",
     "chainId": "1",
     "fromChainId": "1", // Same as chainId, cross-chain transactions are transferred out of the chain
     "toChainId": "1", // For cross-chain transactions, transfer the chain id, and the ordinary transaction is the 					//same as the chainId
     "from": "0xd40a7fa793ee48cf6a489366a53d2cbd7be1c9b3",
     "to": "0xa973fc18182fe0a813F6CBadF38b6c8C1789317D",
     "value": 10,
     "nonce": 34,
     "attach": "1234,thinkey,gs",
     "privateKey": "1wz/9W9G5zLbAVlfzGWqvrJY+uzyq7yPvI7UssKWVeETAlSqCoaiBvrtPZrsfpuLpN2B4K2LE5k6D8AJ7W8YJUxDp0qe6n1KF+buqrX9xpM=",
     "notifyUrl": "http://localhost:8101/v1/test/"
}
```

Return example

```json
{
    "code": 200,
    "msg": "success",
    "data": {
        "msg": "",
        "hash": "0x54a0cab9ab9773b0d29b770d1138d0a500e50f32eebaefbff13304f22a157319",
        "nonce": "34"
    }
}
}
```
Note: Use 14 to obtain transaction details interface to obtain data after initiation.



### 21. Main currency transaction-sig transaction

Interface address: **/v1/tx/signed/send**

Request method: **POST**
Request parameters:

| Parameter name | Required | Type | Description |
| ---------- | ---- | ------ | -------------------------- ----------------------- |
| bussinessId 	| Y | String | Service id |
| chainId 		| Y | String | Chain id |
| attach 		| Y | String | Business parameters |
| notifyUrl	 	| Y | String | Callback address |
| Transaction 	| Y | JSON | Data from Sdk sig |

Return parameter description

| Parameter name | Type | Description |
| ------ | ------ | -------- |
| code 		| String 	| Return code |
| msg 		| String 	| Return information |
| data 		| 			| Return data |

data:
| Parameter name | Type | Description |
| ------ | ------ | -------- |
| Msg 	| String 	| Prompt Information |
| Hash 	| String 	| Transaction hash |
| Nonce | Int 		| nonce after transaction |

Request example

```json
{
     "businessId": "1",
     "chainId": "1",
     "attach": "1,2,3,4,5",
     "notifyUrl": "http://localhost:8101/v1/test/",
     "transaction": {
        "chainId": "1",
        "fromChainId": "1",
        "toChainId": "1",
        "from": "0xd40a7fa793ee48cf6a489366a53d2cbd7be1c9b3",
        "to": "0xa973fc18182fe0a813F6CBadF38b6c8C1789317D",
        "nonce": "35",
        "value": "35000000000000000000",
        "sig": "0xd9b79ff166dac5efadbb91104b0ac3988a424f1da08d80a18996cc6f603eccda5ff3b1ac2ed6f84884baed074b1d6aa63440c6907e123ea3ab0cd44403465ad701",
        "pub": "0x04ca6c6d236352ccb7b856c63ed2ee095b5d66e03467667e0a37dc5271bc611c26a85a783c54726e93fe2d4bce0305b75c64b77d9c625bfa513fe70b40076a368c",
        "input": "",
        "useLocal": false,
        "extra": "",
        "multipubs": null,
        "multisigs": null
    }
}
```

Return example

```json
{
    "code": 200,
    "msg": "success",
    "data": {
        "msg": "",
        "hash": "0xab59d34babccdcbb99de6ea627be78ef1786939d4356ffdc8149e488ea13b12a",
        "nonce": "0"
    }
}
```
Note:the verification method is the same as the main currency transaction













