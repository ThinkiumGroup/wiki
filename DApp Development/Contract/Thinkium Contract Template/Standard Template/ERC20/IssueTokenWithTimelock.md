# Contract template

## Issue tokens and lock up positions
### noted
>  Issuing lockeable ERC20 tokens requires deploying two contract files at the same time. The principle is that after deploying one ERC20 token, the address of the token is passed as a parameter to the second locked-up contract.

> After the lock-up contract is installed, the transfer method of ERC20 token contract should be called to transfer all tokens from the sender account to the account of lock-up contract.

> The above two points are already set up in the deployment script

[Contract Document: ERC20WithTokenTimelock.sol](https://github.com/TxCodeGroup/ContractTemplate/blob/master/contracts/ERC20/ERC20WithTokenTimelock.sol)

[Test script: ERC20WithTokenTimelock.js](https://github.com/TxCodeGroup/ContractTemplate/blob/master/test/ERC20/ERC20WithTokenTimelock.js)

[Deployment script: 7_deploy_IssueTokenWithTimelock.js](https://github.com/TxCodeGroup/ContractTemplate/blob/master/migrations/7_deploy_IssueTokenWithTimelock.js)

### Define the following variables when deploying the contract
```javascript
IERC20 token            //ERC20 token address
address beneficiary     //can be another account than the sender
uint256 releaseTime     //Unlock timestamp
```
### Calling methods (omitted ERC20 call method)
```javascript
token() public view returns (IERC20)            //Returns ERC20 contract
beneficiary() public view returns (address)     //Return beneficiary's address
releaseTime() public view returns (uint256)     //Returns the unlock time
release() public                                //Triggers the unlock, which can be called by anyone but can only be released to the beneficiary
```
