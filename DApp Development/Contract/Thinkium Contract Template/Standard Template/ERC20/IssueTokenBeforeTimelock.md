# Contract template

## Lock up after issuing tokens
### noted
> Place the contract in accordance with the method of issuing ERC20 tokens, record the contract address, and then execute the placement script of issuing first and then locking up.

> Instead of doing this in practice, you can replace the code that instantiates the contract with the contract address, and then transfer the token to the lock-in contract address via an externally called method.

> To run this example, the deployed ERC20 contract is directly instantiated in the deployed script.

[Contract Document: ERC20WithTokenTimelock.sol](https://github.com/TxCodeGroup/ContractTemplate/blob/master/contracts/ERC20/ERC20WithTokenTimelock.sol)

[Test script: ERC20WithTokenTimelock.js](https://github.com/TxCodeGroup/ContractTemplate/blob/master/test/ERC20/ERC20WithTokenTimelock.js)

[Deployment script: 8_deploy_IssueTokenBeforeTimelock.js](https://github.com/TxCodeGroup/ContractTemplate/blob/master/migrations/8_deploy_IssueTokenBeforeTimelock.js)

### define the following variables when deploying the contract
```javascript
IERC20 token            //ERC20 token address
address beneficiary     //can be another account than the sender
uint256 releaseTime     //Unlock timestamp
```
### Calling methods (omitted ERC20 call method)
```javascript
token() public view returns (IERC20)            //Returns ERC20 contract
beneficiary() public view returns (address)     //Return beneficiary's address
releaseTime() public view returns (uint256)     // Returns the unlock time
release() public                                //Triggers the unlock, which can be called by anyone but can only be released to the beneficiary
```
