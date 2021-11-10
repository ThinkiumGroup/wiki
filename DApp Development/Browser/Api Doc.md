

### Global parameter description

The url of each interface parameter is the rpc service address. The production environment needs to be configured with the production rpc address, which can be applied to the official customer service. You can also use your own deployed version.



Test base url：**http://browser.thinkiumdev.net/browser-api/**

Production base url：**https://www.thinkiumscan.net/browser-api/**



## Service Http interface

### 1.Get transaction records

1. This interface is used to obtain transaction records, and records of different chains or the same chain can be obtained


interface address：**/v1/tradingList**	

Request method: **POST**
Request parameters:

| parameter name  | required | type   | illustrate                             |
| ------- | ---- | ------ | ------------------------------------------ |
| chainId 			| Y    | String 		| If the chain id is not passed, it is the total data of all chains    |
| address 			| Y    | String 		| 0xe3b3599093af404231761ca1cf36a11e97571312 |
| blockHeight 		| Y    | Long 			| Block height, only check this block of transactions        |
| parentType 		| Y    | Int 			| Parent type 2 Contract transaction 3 Ordinary transaction 7 Cross-												chain transaction  |
| childType 		| Y    | Int 			| See below for details              |
| orderType 		| Y    | Int 			| The default is reverse order, pass 1 for positive order|
| contractAddress 	| Y    | String 		| Contract address, only check this contract related     |
| contractAddresss 	| Y    | List<String> 	| Contract address list, note that there is an additional S, check the 												transactions related to this list|
| timeStamp 		| Y    | Long 			|                                      |
| hash 				| Y    | String 		| Check single data and send hash|
| chainId 			| Y    | String 		| 1                           |
| tables 			| Y    | List<Table> 	|  |

timeStamp:
	Note: paging basis, this value must be present to paging, and the data corresponding to the parameter of the last item of the current page is regarded as the request parameter data of the next page (the first page may not be transmitted)

tables:
	Note: Below the structure, an array composed of three data, tableId, tableName, and chainId of the returned data on each page, is used for paging, and it may be repeated according to timeStamp. It is recommended that this parameter is also transmitted. Use together to ensure uniqueness
|Parameter name | Type | Description |
| ------- | ---- | ------ |
|tableId	|	Int			Id|
|tableName	|string	|
|chainId	|	Int	|

childType:
	Note: It must be used in conjunction with parentType. For example, parentType=2, if childType starts with 2.
|key | Description |
| ------- | ---- |
|201 | Contract Release|
|202 | Ordinary contract transactions|
|203 | POC lock|
|204 |POC Award|
|205 |POC Redemption|
|207 |POS Award|
|208 |POS Lock|
|301 |Transfer Out|
|302 |Transfer in|
|303 |POS Award|
|401 |Cross-chain transaction withdrawal|
|402 |Cross-chain transaction deposit|
|403 |Cross-chain transaction cancellation|

Return parameter description:

| Parameter name | Type | Description |
| ------ | ------ | -------------- |
| code | string | Return code |
| msg  | string | Return information |
| data | 		| Returned business information |

data:

| Parameter name | Type | Description |
| --------------- | ------ | -------------------------- -------------------- |
| chainId 		 	| Int 		| chain id|
| chainName      	| String 	| Chain name in English|
| chainChinaeseName | String 	| Chain Name Chinese|
| currencyFee 		| BigDecimal| Handling fee|
| gasFee 			| BigDecimal| The transaction fee and the above are the same value|
| tradingHash 		| String 	| Trading hash|
| currencyAmount 	| BigDecimal| Transaction Amount Contract transactions will not be displayed in this field|
| blockHeight 		| Long 		| Block height|
| fromAddress 		| String 	| From Address|
| toAddress 		| String 	| To address|
| parentType 		| Int 		| Passing parameters and returning only|
| childType 		| Int 		| Same as above|
| parentTypeName 	| String 	||
| childTypeName 	| String 	||
| timeStamp 		| Long 		| Timestamp|
| transferType 		| Int 		| 0 transfer out 1 transfer in|
| status 			| Int 		| 0 failed 1 succeeded|
| tableName 		| String 	| Table name|
| tableId 			| Int 		| ID                |



Request example:
```json
{
	"address": "0x72161d9be1e6ab4265ddc5720c713c58fc63f568",
	"parentType": "",
	"childType": "",
	"page": 1,
	"rows": 60
}
```

Return example:

```json
{
	"status": true,
	"code": 200,
	"msg": "success",
	"data": {
		"total": 2,
		"data": [{
			"chainId": 2,
			"chainName": "title.pos_reward_chain",
			"chainChineseName": "PoS",
			"currencyFee": 32999200000000000,
			"gasFee": 32999200000000000,
			"tradingHash": "0xe29e50bbeadbb3413a65242e4e4cc5d326f9a710271ba275d350bab23f1df9a6",
			"currencyAmount": 200000000000000000000000,
			"blockHeight": 13900296,
			"belongtoChain": "title.pos_reward_chain",
			"sourceOfcurrency": "select.contract_trading-select.pos_lock",
			"fromAddress": "0x883c21c03e0a22137a439b552d671b9ec45472e7",
			"toAddress": "0x72161d9be1e6ab4265ddc5720c713c58fc63f568",
			"parentType": null,
			"childType": null,
			"parentTypeName": "select.contract_trading",
			"childTypeName": "select.pos_lock",
			"timeStamp": 1618486336,
			"transferType": 1,
			"status": 1,
			"tableName": "block_tx_2_1",
			"tableId": 1789410,
			"tokenNum": null,
			"toChainId": null,
			"getType": null,
			"swap": null,
			"liquidity": null,
			"crossChain": null
		}, {
			"chainId": 2,
			"chainName": "title.pos_reward_chain",
			"chainChineseName": "PoS链",
			"currencyFee": 87279600000000000,
			"gasFee": 87279600000000000,
			"tradingHash": "0x5826db5ffb479bd4a1807be8e0dabc0e796944f0dc0aa9656a9da0c07af83e7f",
			"currencyAmount": 1050000000000000000000000,
			"blockHeight": 13869336,
			"belongtoChain": "title.pos_reward_chain",
			"sourceOfcurrency": "select.contract_trading-select.pos_lock",
			"fromAddress": "0x883c21c03e0a22137a439b552d671b9ec45472e7",
			"toAddress": "0x72161d9be1e6ab4265ddc5720c713c58fc63f568",
			"parentType": null,
			"childType": null,
			"parentTypeName": "select.contract_trading",
			"childTypeName": "select.pos_lock",
			"timeStamp": 1618399190,
			"transferType": 1,
			"status": 1,
			"tableName": "block_tx_2_1",
			"tableId": 1783643,
			"tokenNum": null,
			"toChainId": null,
			"getType": null,
			"swap": null,
			"liquidity": null,
			"crossChain": null
		}]
	}
}
```

### 2. Cross-chain transaction
This interface is used to obtain cross-chain transactions, and if the cross-chain transaction fails, you can use this interface to obtain records, and then try again

Interface address: **/v1/checkCrossTx**

Request method: **POST**
Request parameters:

| Parameter name | Required | Type | Description |
| ----------- | ---- | ------------------ | ------------- ----------------------------------------------- |
| address		 | Y | String 	|User address|
| page 			 | Y | Int 		|Paging Pages|
| rows 			 | Y | Int 		|page number of rows|

Return parameter description

| Parameter name | Type | Description |
| ------ | ------ | -------------- |
| code 	 | string 	| Return code |
| msg 	 | string 	| Return information |
| data 	 | 			| Returned business information |

data:

| Parameter name | Type | Description |
| ------------ | ---- | ------------------------------- ----------- |
| total 		| int | number|
| data 			| List ||

data.data:

|Parameter name | Type | Description |
| ------------ | ---- | ------------------------------- ----------- |
| chainId 			| Int 		| chain id|
| fromChainId 		| Int 		| issuing chain|
| toChainId 		| Int 		| Receiving Chain|
| fromAddress 		| String 	| Outgoing address|
| toAddress 		| String 	| Transfer address|
| nonce 			| Int 		||
| value 			| String 	| Transaction amount|
| expire 			| Boolean 	| Is it expired? false, not expired, true expired|
| writeCheckTxHash 	| String 	| Transaction hash|
| createTime 		| Long 		| Launch time|

Request example:

Contract code example

```java
{
    "address":"0x7f28b80861779ef731bc1f56a4a7a36c3c285d44",
    "page":1,
    "rows":10
}
```

Corresponding conversion request parameters:

```json
{
    "status": true,
    "code": 200,
    "msg": "success",
    "data": {
        "total": 1,
        "data": [
            {
                "chainId": 1,
                "fromChainId": 1,
                "toChainId": 2,
                "fromAddress": "0x7f28b80861779ef731bc1f56a4a7a36c3c285d44",
                "toAddress": "0x7f28b80861779ef731bc1f56a4a7a36c3c285d44",
                "nonce": 233,
                "value": "1000000000000000000",
                "expire": false,
                "writeCheckTxHash": "0x282c1963f3221781dd995c0f084c2aa5dc2ce755de41520db1e9cf15280f91c8",
                "createTime": 1619458434
            }
        ]
    }
}
```

### 3. Get PosNode by data node id

Interface address: **/v1/getPosNodeByDataNodeId**

Request method: **POST**
Request parameters:

| Parameter name | Required | Type | Description |
| ------------ | ---- | ------------------------ | ------ -------------------------------------------------- ---- |
| nodeId | Y | String | Data node id |

Return parameter description

| Parameter name | Type | Description |
| ------ | ------ | -------- |
| code 	 | String 	| Return code |
| msg    | String 	| Return information |
| data   | 			| Return data |

data:

| Parameter name | Type | Description |
| ------------ | ---- | ------------------------------- ----------- |
| total 		| int  | number|
| data 			| List ||

data.data:

| Parameter name | Type | Description |
| ------------ | ---- | ------------------------------- ----------- |
| nodeId 			| String ||
| ip 				| String ||
| contractAddress 	| String ||
| manager 			| String | Management|
| version 			| String | version|
| canPledgedAmount 	| String | Pledged Amount|


Request example:

```json
{
    "nodeId":"0xf439fa8217e9c7efcb899846b2f2cc90d238c4808faa81c23788372c7f4310ced94427d63779fac3d70dc1e464062af969d1c29d7025f80196fda3e774c4f46a"
}
```

Return example:

```json
{
    "status": true,
    "code": 200,
    "msg": "success",
    "data": {
        "total": 1,
        "data": [
            {
                "nodeId": "0xcc20c14527d9e7bbfed1f9b986ea706643a5fa4eb1bca8e69b757f9dca71eb7bf4d60d0d2185066cf8a36b5feb96a0826d4bc7402891676e5f239fb6705df119",
                "ip": "202.202.214.209",
                "contractAddress": "0x309b3e76b201f58a8a52c5aaf370477754819f2e",
                "manager": "",
                "version": "v2",
                "canPledgedAmount": "0"
            }
        ]
    }
}
```

### 4. Obtain the consensus node pledge record

Interface address: **/v1/posLog**

Request method: **POST**
Request parameters:

| Parameter name | Required | Type | Description |
| ----------- | ---- | ------------------ | ------------- ----------------------------------------------- |
| contractAddress 	| Y | String | Contract address|
| startHeight 		| Y | String | Starting block height|

Return parameter description

| Parameter name | Type | Description |
| ------ | ------ | -------- |
| code 	| String 	| Return code |
| msg 	| String 	| Return information |
| data 	| 			| Return data |

data:

| Parameter name | Type | Description |
| ------------ | ---- | ------------------------------- ----------- |
| total 	| int 	| number|
| data 		| List 	||

data.data:

| Parameter name | Type | Description |
| ------------ | ------ | -------- |
| hash 			| String ||
| from 			| String | from address|
| value 		| String | Amount|
| blockHeight 	| String | Block height   |

Request example:

```json
{
    "contractAddress":"0x8971024a0267731c55e87aea3b094f33d2ebe3b3",
    "startHeight":0
}
```

Return example:

```json
{
    "status": true,
    "code": 200,
    "msg": "success",
    "data": {
        "total": 3,
        "data": [
            {
                "hash": "0x9c03f1df87f080ade9a48223f0826892fdfbd46f3647cfb30fcbf0a5a6b9bf52",
                "from": "0xb3ff8dec779090e4086bbb6f21fb13197deacf00",
                "value": "50000000000000000000000",
                "blockHeight": "16629175"
            },
            {
                "hash": "0x0e27efe5deea1e6bd6bd4c2c79c8fbc9dc06a0e5ac5afa7c2c3ac18a7a532aa7",
                "from": "0xb3ff8dec779090e4086bbb6f21fb13197deacf00",
                "value": "1000000000000000000000",
                "blockHeight": "18050355"
            },
            {
                "hash": "0x2c978e3edca054e20649d069acd11bb6aa60db172f03b5619fa391740e727fff",
                "from": "0xb3ff8dec779090e4086bbb6f21fb13197deacf00",
                "value": "1000000000000000000000",
                "blockHeight": "18077922"
            }
        ]
    }
}
```

### 5.Register the Contract 

Interface address:**/v1/registerContract**

Request method：**POST** 
Request parameters:

| Parameter name  | Required | Type   | Description      |
| --------------- | -------- | ------ | ---------------- |
| chainId         | Y        | Int    | Chain Id         |
| address         | Y        | String | From Address     |
| rpcUrl          | Y        | String | Rpc Url          |
| contractAddress | Y        | String | Contract Address |
| contractName    | Y        | String | Contract Name    |
| abi             | Y        | String | Contract Abi     |
| tokenName       | Y        | String | Token Name       |
| iconUrl         | Y        | String | Token Icon Url   |

Return parameter description

| arameter name | Type   | Description        |
| ------------- | ------ | ------------------ |
| code          | String | Return code        |
| msg           | String | Return information |
| data          |        | Return data        |

Request example:

```json
{
"chainId": 1,
"rpcUrl": "rpctest.thinkium.org",
"contractAddress": "0xc7550bed364a8783bb1443c0a5a965775ea3608e",
"contractName": "test111",
"abi": "[{\"constant\":true,\"inputs\":[],\"name\":\"name\",\"outputs\":[{\"name\":\"\",\"type\":\"string\",\"components\":[],\"internalType\":\"\",\"indexed\":false,\"dynamic\":true}],\"type\":\"function\",\"payable\":false,\"stateMutability\":\"view\"},{\"constant\":false,\"inputs\":[{\"name\":\"spender\",\"type\":\"address\",\"components\":[],\"internalType\":\"\",\"indexed\":false,\"dynamic\":false},{\"name\":\"value\",\"type\":\"uint256\",\"components\":[],\"internalType\":\"\",\"indexed\":false,\"dynamic\":false}],\"name\":\"approve\",\"outputs\":[{\"name\":\"\",\"type\":\"bool\",\"components\":[],\"internalType\":\"\",\"indexed\":false,\"dynamic\":false}],\"type\":\"function\",\"payable\":false,\"stateMutability\":\"nonpayable\"},{\"constant\":true,\"inputs\":[],\"name\":\"totalSupply\",\"outputs\":[{\"name\":\"\",\"type\":\"uint256\",\"components\":[],\"internalType\":\"\",\"indexed\":false,\"dynamic\":false}],\"type\":\"function\",\"payable\":false,\"stateMutability\":\"view\"},{\"constant\":false,\"inputs\":[{\"name\":\"from\",\"type\":\"address\",\"components\":[],\"internalType\":\"\",\"indexed\":false,\"dynamic\":false},{\"name\":\"to\",\"type\":\"address\",\"components\":[],\"internalType\":\"\",\"indexed\":false,\"dynamic\":false},{\"name\":\"value\",\"type\":\"uint256\",\"components\":[],\"internalType\":\"\",\"indexed\":false,\"dynamic\":false}],\"name\":\"transferFrom\",\"outputs\":[{\"name\":\"\",\"type\":\"bool\",\"components\":[],\"internalType\":\"\",\"indexed\":false,\"dynamic\":false}],\"type\":\"function\",\"payable\":false,\"stateMutability\":\"nonpayable\"},{\"constant\":true,\"inputs\":[],\"name\":\"decimals\",\"outputs\":[{\"name\":\"\",\"type\":\"uint8\",\"components\":[],\"internalType\":\"\",\"indexed\":false,\"dynamic\":false}],\"type\":\"function\",\"payable\":false,\"stateMutability\":\"view\"},{\"constant\":false,\"inputs\":[{\"name\":\"spender\",\"type\":\"address\",\"components\":[],\"internalType\":\"\",\"indexed\":false,\"dynamic\":false},{\"name\":\"addedValue\",\"type\":\"uint256\",\"components\":[],\"internalType\":\"\",\"indexed\":false,\"dynamic\":false}],\"name\":\"increaseAllowance\",\"outputs\":[{\"name\":\"\",\"type\":\"bool\",\"components\":[],\"internalType\":\"\",\"indexed\":false,\"dynamic\":false}],\"type\":\"function\",\"payable\":false,\"stateMutability\":\"nonpayable\"},{\"constant\":false,\"inputs\":[],\"name\":\"unpause\",\"outputs\":[],\"type\":\"function\",\"payable\":false,\"stateMutability\":\"nonpayable\"},{\"constant\":true,\"inputs\":[{\"name\":\"account\",\"type\":\"address\",\"components\":[],\"internalType\":\"\",\"indexed\":false,\"dynamic\":false}],\"name\":\"isPauser\",\"outputs\":[{\"name\":\"\",\"type\":\"bool\",\"components\":[],\"internalType\":\"\",\"indexed\":false,\"dynamic\":false}],\"type\":\"function\",\"payable\":false,\"stateMutability\":\"view\"},{\"constant\":true,\"inputs\":[],\"name\":\"burnAmount\",\"outputs\":[{\"name\":\"\",\"type\":\"uint256\",\"components\":[],\"internalType\":\"\",\"indexed\":false,\"dynamic\":false}],\"type\":\"function\",\"payable\":false,\"stateMutability\":\"view\"},{\"constant\":true,\"inputs\":[{\"name\":\"account\",\"type\":\"address\",\"components\":[],\"internalType\":\"\",\"indexed\":false,\"dynamic\":false},{\"name\":\"snapshotId\",\"type\":\"uint256\",\"components\":[],\"internalType\":\"\",\"indexed\":false,\"dynamic\":false}],\"name\":\"balanceOfAt\",\"outputs\":[{\"name\":\"\",\"type\":\"uint256\",\"components\":[],\"internalType\":\"\",\"indexed\":false,\"dynamic\":false}],\"type\":\"function\",\"payable\":false,\"stateMutability\":\"view\"},{\"constant\":true,\"inputs\":[],\"name\":\"paused\",\"outputs\":[{\"name\":\"\",\"type\":\"bool\",\"components\":[],\"internalType\":\"\",\"indexed\":false,\"dynamic\":false}],\"type\":\"function\",\"payable\":false,\"stateMutability\":\"view\"},{\"constant\":false,\"inputs\":[],\"name\":\"renouncePauser\",\"outputs\":[],\"type\":\"function\",\"payable\":false,\"stateMutability\":\"nonpayable\"},{\"constant\":true,\"inputs\":[{\"name\":\"account\",\"type\":\"address\",\"components\":[],\"internalType\":\"\",\"indexed\":false,\"dynamic\":false}],\"name\":\"balanceOf\",\"outputs\":[{\"name\":\"\",\"type\":\"uint256\",\"components\":[],\"internalType\":\"\",\"indexed\":false,\"dynamic\":false}],\"type\":\"function\",\"payable\":false,\"stateMutability\":\"view\"},{\"constant\":false,\"inputs\":[{\"name\":\"account\",\"type\":\"address\",\"components\":[],\"internalType\":\"\",\"indexed\":false,\"dynamic\":false}],\"name\":\"addPauser\",\"outputs\":[],\"type\":\"function\",\"payable\":false,\"stateMutability\":\"nonpayable\"},{\"constant\":false,\"inputs\":[],\"name\":\"pause\",\"outputs\":[],\"type\":\"function\",\"payable\":false,\"stateMutability\":\"nonpayable\"},{\"constant\":true,\"inputs\":[],\"name\":\"symbol\",\"outputs\":[{\"name\":\"\",\"type\":\"string\",\"components\":[],\"internalType\":\"\",\"indexed\":false,\"dynamic\":true}],\"type\":\"function\",\"payable\":false,\"stateMutability\":\"view\"},{\"constant\":true,\"inputs\":[{\"name\":\"snapshotId\",\"type\":\"uint256\",\"components\":[],\"internalType\":\"\",\"indexed\":false,\"dynamic\":false}],\"name\":\"totalSupplyAt\",\"outputs\":[{\"name\":\"\",\"type\":\"uint256\",\"components\":[],\"internalType\":\"\",\"indexed\":false,\"dynamic\":false}],\"type\":\"function\",\"payable\":false,\"stateMutability\":\"view\"},{\"constant\":false,\"inputs\":[{\"name\":\"account\",\"type\":\"address\",\"components\":[],\"internalType\":\"\",\"indexed\":false,\"dynamic\":false}],\"name\":\"addMinter\",\"outputs\":[],\"type\":\"function\",\"payable\":false,\"stateMutability\":\"nonpayable\"},{\"constant\":false,\"inputs\":[],\"name\":\"renounceMinter\",\"outputs\":[],\"type\":\"function\",\"payable\":false,\"stateMutability\":\"nonpayable\"},{\"constant\":true,\"inputs\":[],\"name\":\"current\",\"outputs\":[{\"name\":\"\",\"type\":\"uint256\",\"components\":[],\"internalType\":\"\",\"indexed\":false,\"dynamic\":false}],\"type\":\"function\",\"payable\":false,\"stateMutability\":\"view\"},{\"constant\":false,\"inputs\":[{\"name\":\"spender\",\"type\":\"address\",\"components\":[],\"internalType\":\"\",\"indexed\":false,\"dynamic\":false},{\"name\":\"subtractedValue\",\"type\":\"uint256\",\"components\":[],\"internalType\":\"\",\"indexed\":false,\"dynamic\":false}],\"name\":\"decreaseAllowance\",\"outputs\":[{\"name\":\"\",\"type\":\"bool\",\"components\":[],\"internalType\":\"\",\"indexed\":false,\"dynamic\":false}],\"type\":\"function\",\"payable\":false,\"stateMutability\":\"nonpayable\"},{\"constant\":false,\"inputs\":[{\"name\":\"to\",\"type\":\"address\",\"components\":[],\"internalType\":\"\",\"indexed\":false,\"dynamic\":false},{\"name\":\"value\",\"type\":\"uint256\",\"components\":[],\"internalType\":\"\",\"indexed\":false,\"dynamic\":false}],\"name\":\"transfer\",\"outputs\":[{\"name\":\"\",\"type\":\"bool\",\"components\":[],\"internalType\":\"\",\"indexed\":false,\"dynamic\":false}],\"type\":\"function\",\"payable\":false,\"stateMutability\":\"nonpayable\"},{\"constant\":true,\"inputs\":[{\"name\":\"account\",\"type\":\"address\",\"components\":[],\"internalType\":\"\",\"indexed\":false,\"dynamic\":false}],\"name\":\"isMinter\",\"outputs\":[{\"name\":\"\",\"type\":\"bool\",\"components\":[],\"internalType\":\"\",\"indexed\":false,\"dynamic\":false}],\"type\":\"function\",\"payable\":false,\"stateMutability\":\"view\"},{\"constant\":true,\"inputs\":[{\"name\":\"owner\",\"type\":\"address\",\"components\":[],\"internalType\":\"\",\"indexed\":false,\"dynamic\":false},{\"name\":\"spender\",\"type\":\"address\",\"components\":[],\"internalType\":\"\",\"indexed\":false,\"dynamic\":false}],\"name\":\"allowance\",\"outputs\":[{\"name\":\"\",\"type\":\"uint256\",\"components\":[],\"internalType\":\"\",\"indexed\":false,\"dynamic\":false}],\"type\":\"function\",\"payable\":false,\"stateMutability\":\"view\"},{\"constant\":false,\"inputs\":[{\"name\":\"name\",\"type\":\"string\",\"components\":[],\"internalType\":\"\",\"indexed\":false,\"dynamic\":true},{\"name\":\"symbol\",\"type\":\"string\",\"components\":[],\"internalType\":\"\",\"indexed\":false,\"dynamic\":true}],\"name\":null,\"outputs\":[],\"type\":\"constructor\",\"payable\":false,\"stateMutability\":\"nonpayable\"},{\"constant\":false,\"inputs\":[{\"name\":\"id\",\"type\":\"uint256\",\"components\":[],\"internalType\":\"\",\"indexed\":false,\"dynamic\":false}],\"name\":\"Snapshot\",\"outputs\":[],\"type\":\"event\",\"payable\":false,\"stateMutability\":null},{\"constant\":false,\"inputs\":[{\"name\":\"account\",\"type\":\"address\",\"components\":[],\"internalType\":\"\",\"indexed\":false,\"dynamic\":false}],\"name\":\"Paused\",\"outputs\":[],\"type\":\"event\",\"payable\":false,\"stateMutability\":null},{\"constant\":false,\"inputs\":[{\"name\":\"account\",\"type\":\"address\",\"components\":[],\"internalType\":\"\",\"indexed\":false,\"dynamic\":false}],\"name\":\"Unpaused\",\"outputs\":[],\"type\":\"event\",\"payable\":false,\"stateMutability\":null},{\"constant\":false,\"inputs\":[{\"name\":\"account\",\"type\":\"address\",\"components\":[],\"internalType\":\"\",\"indexed\":true,\"dynamic\":false}],\"name\":\"PauserAdded\",\"outputs\":[],\"type\":\"event\",\"payable\":false,\"stateMutability\":null},{\"constant\":false,\"inputs\":[{\"name\":\"account\",\"type\":\"address\",\"components\":[],\"internalType\":\"\",\"indexed\":true,\"dynamic\":false}],\"name\":\"PauserRemoved\",\"outputs\":[],\"type\":\"event\",\"payable\":false,\"stateMutability\":null},{\"constant\":false,\"inputs\":[{\"name\":\"account\",\"type\":\"address\",\"components\":[],\"internalType\":\"\",\"indexed\":true,\"dynamic\":false}],\"name\":\"MinterAdded\",\"outputs\":[],\"type\":\"event\",\"payable\":false,\"stateMutability\":null},{\"constant\":false,\"inputs\":[{\"name\":\"account\",\"type\":\"address\",\"components\":[],\"internalType\":\"\",\"indexed\":true,\"dynamic\":false}],\"name\":\"MinterRemoved\",\"outputs\":[],\"type\":\"event\",\"payable\":false,\"stateMutability\":null},{\"constant\":false,\"inputs\":[{\"name\":\"from\",\"type\":\"address\",\"components\":[],\"internalType\":\"\",\"indexed\":true,\"dynamic\":false},{\"name\":\"to\",\"type\":\"address\",\"components\":[],\"internalType\":\"\",\"indexed\":true,\"dynamic\":false},{\"name\":\"value\",\"type\":\"uint256\",\"components\":[],\"internalType\":\"\",\"indexed\":false,\"dynamic\":false}],\"name\":\"Transfer\",\"outputs\":[],\"type\":\"event\",\"payable\":false,\"stateMutability\":null},{\"constant\":false,\"inputs\":[{\"name\":\"owner\",\"type\":\"address\",\"components\":[],\"internalType\":\"\",\"indexed\":true,\"dynamic\":false},{\"name\":\"spender\",\"type\":\"address\",\"components\":[],\"internalType\":\"\",\"indexed\":true,\"dynamic\":false},{\"name\":\"value\",\"type\":\"uint256\",\"components\":[],\"internalType\":\"\",\"indexed\":false,\"dynamic\":false}],\"name\":\"Approval\",\"outputs\":[],\"type\":\"event\",\"payable\":false,\"stateMutability\":null},{\"constant\":false,\"inputs\":[],\"name\":\"snapshot\",\"outputs\":[{\"name\":\"\",\"type\":\"uint256\",\"components\":[],\"internalType\":\"\",\"indexed\":false,\"dynamic\":false}],\"type\":\"function\",\"payable\":false,\"stateMutability\":\"nonpayable\"},{\"constant\":true,\"inputs\":[],\"name\":\"getMemberCount\",\"outputs\":[{\"name\":\"\",\"type\":\"uint256\",\"components\":[],\"internalType\":\"\",\"indexed\":false,\"dynamic\":false}],\"type\":\"function\",\"payable\":false,\"stateMutability\":\"view\"},{\"constant\":true,\"inputs\":[{\"name\":\"index\",\"type\":\"uint256\",\"components\":[],\"internalType\":\"\",\"indexed\":false,\"dynamic\":false}],\"name\":\"getMember\",\"outputs\":[{\"name\":\"\",\"type\":\"address\",\"components\":[],\"internalType\":\"\",\"indexed\":false,\"dynamic\":false}],\"type\":\"function\",\"payable\":false,\"stateMutability\":\"view\"},{\"constant\":true,\"inputs\":[{\"name\":\"account\",\"type\":\"address\",\"components\":[],\"internalType\":\"\",\"indexed\":false,\"dynamic\":false}],\"name\":\"isMember\",\"outputs\":[{\"name\":\"\",\"type\":\"bool\",\"components\":[],\"internalType\":\"\",\"indexed\":false,\"dynamic\":false}],\"type\":\"function\",\"payable\":false,\"stateMutability\":\"view\"},{\"constant\":false,\"inputs\":[{\"name\":\"account\",\"type\":\"address\",\"components\":[],\"internalType\":\"\",\"indexed\":false,\"dynamic\":false},{\"name\":\"amount\",\"type\":\"uint256\",\"components\":[],\"internalType\":\"\",\"indexed\":false,\"dynamic\":false}],\"name\":\"mint\",\"outputs\":[{\"name\":\"\",\"type\":\"bool\",\"components\":[],\"internalType\":\"\",\"indexed\":false,\"dynamic\":false}],\"type\":\"function\",\"payable\":false,\"stateMutability\":\"nonpayable\"},{\"constant\":false,\"inputs\":[{\"name\":\"account\",\"type\":\"address\",\"components\":[],\"internalType\":\"\",\"indexed\":false,\"dynamic\":false},{\"name\":\"amount\",\"type\":\"uint256\",\"components\":[],\"internalType\":\"\",\"indexed\":false,\"dynamic\":false}],\"name\":\"burnFrom\",\"outputs\":[],\"type\":\"function\",\"payable\":false,\"stateMutability\":\"nonpayable\"}]",
"address": "0xdfc9aa32f4bb1c90842f5f79c78b3124a9fe5c76",
"tokenName": "WYHGGHH",
"iconUrl": "http://xxx/pic%2Fed46f1315fcd4a70ae77ef3f91118603.png"
}
```

Return example:

```json
{
"status": true,
"code": 200,
"msg": "success",
"data": null
}
```

