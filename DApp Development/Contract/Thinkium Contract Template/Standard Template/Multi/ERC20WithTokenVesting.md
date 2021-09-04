# Contract template


## Release contract in installments

> An installment release contract is similar to a lock-up contract, except that the locked ERC20 tokens are released to the beneficiary over a period of time specified when the contract is deployed.
> The release period is calculated after the start time, in seconds, until the cliffDuration is released after the cliff time, and ends after the duration of the 'duration'.
> Start =now(); start=now(); cliffDuration=1 year; duration=4 year;
> The release method can be called at any time after 'cliffDuration', and the release amount is calculated as: total lock amount * ((current time - start time)/duration) - Released number

[Contract Document: ERC20WithTokenVesting.sol](https://github.com/TxCodeGroup/ContractTemplate/blob/master/contracts/Multi/ERC20WithTokenVesting.sol)

[Test script: ERC20WithTokenVesting.js](https://github.com/TxCodeGroup/ContractTemplate/blob/master/test/Multi/ERC20WithTokenVesting.js)

[Deployment script: 28_deploy_ERC20WithTokenVesting.js](https://github.com/TxCodeGroup/ContractTemplate/blob/master/migrations/28_deploy_ERC20WithTokenVesting.js)

### Define the following variables when deploying the contract
```javascript
address beneficiary,        //beneficiary
uint256 start,              //Start time
uint256 cliffDuration,      //Bluff time
uint256 duration,           //time of duration 
bool revocable              //Revocable or not
```
### The contract shall be executed after deployment
```javascript
// The lock-up tokens need to be transferred to the installment release contract after deployment
token.transfer(ERC20WithTokenVesting.address, SOME_TOKEN_AMOUNT);
```
### Calling methods
```javascript
//return the beneficiary's address
beneficiary() public view returns (address)
// Return to the start time
start() public view returns (uint256)
// Return to cliff time
cliff() public view returns (uint256)
// Returns the duration
duration() public view returns (uint256)
// Returns whether to undo
revocable() public view returns (bool)
// Returns the number released
released(address token) public view returns (uint256)
// Returns whether to undo
revoked(address token) public view returns (bool)
// Release method
release(IERC20 token) public
// Undo method
revoke(IERC20 token) public onlyOwner
```
