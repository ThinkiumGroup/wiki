# Contract template

## Joint-stock beneficiary agreement
> Joint-stock beneficiary contract means that the address of the crowd-funding beneficiary is set as the contractual address of the joint-stock beneficiary on the basis of the crowd-funding contract, so that ETH will be saved into the joint-stock beneficiary contract after the proceeds from the public funding are obtained. When the shareholders of the arrangement of the contract want to get back the proceeds, they can get back the proceeds from the shareholding beneficiary agreement according to the proportion of shares set when the arrangement is made.

> Shareholders and share ratio are set at the time of the contract and cannot be changed later.

[Contract Document: CrowdsalePaymentSplitter.sol](https://github.com/TxCodeGroup/ContractTemplate/blob/master/contracts/Multi/CrowdsalePaymentSplitter.sol)

[Test script: CrowdsalePaymentSplitter.js](https://github.com/TxCodeGroup/ContractTemplate/blob/master/test/Multi/CrowdsalePaymentSplitter.js)

[Deployment script: 27_deploy_CrowdsalePaymentSplitter.js](https://github.com/TxCodeGroup/ContractTemplate/blob/master/migrations/27_deploy_CrowdsalePaymentSplitter.js)

### Define the following variables when deploying the contract
```javascript
address[] memory payees,    //An array of shareholders
uint256[] memory shares     //proportion of shares 
```
### Calling methods
```javascript
//Return the sum of shares
totalShares() public view returns (uint256)
// Returns the total amount released
TotalReleased () Public View returns (uint256)
// Returns the number of shares in the specified account
shares(address account) public view returns (uint256)
// Returns the amount released from the specified account
released(address account) public view returns (uint256)
// return the address of the shareholder account
payee(uint256 index) public view returns (address)
// Release method
release(address payable account) public
```
