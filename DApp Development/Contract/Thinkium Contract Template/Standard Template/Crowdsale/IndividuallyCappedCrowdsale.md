# Contract template

## Crowdfunding with quotas
> The crowdfunding token means that after the token is issued, any address can purchase tokens from the crowdfunding address using ETH.

> The exchange ratio between token and ETH is set at the same time as the contract is deployed.

> All crowdfunding contracts must be deployed after an ERC20 token has been successfully deployed, and a fixed amount of ERC20 contracts has been set in the deployment script

> Quota crowdfunding means that accounts that buy tokens must set quotas before they can buy tokens

[Contract Document: IndividuallyCappedCrowdsale.sol](https://github.com/TxCodeGroup/ContractTemplate/blob/master/contracts/Crowdsale/IndividuallyCappedCrowdsale.sol)

[Test script: IndividuallyCappedCrowdsale.js](https://github.com/TxCodeGroup/ContractTemplate/blob/master/test/Crowdsale/IndividuallyCappedCrowdsale.js)

[Deployment script: 12_deploy_IndividuallyCappedCrowdsale.js](https://github.com/TxCodeGroup/ContractTemplate/blob/master/migrations/12_deploy_IndividuallyCappedCrowdsale.js)

### Define the following variables when deploying the contract
```javascript
uint256 rate               //how many ERC20 tokens are exchanged for 1ETH
address payable wallet     //to receive ETH beneficiary's address
IERC20 token               //token address
address tokenWallet        //Tokens are sent from this address
```
###  ERC20 method needs to be implemented after the crowdfunding contract is placed
```javascript
//Tokens in the sender's account must be approved for crowdfunding contracts after deployment
token.approve(crowdsale.address, SOME_TOKEN_AMOUNT);
```
### Calling methods
```javascript
//Return the token address
token() public view returns (IERC20)          
//return the beneficiary's address            
wallet() public view returns (address payable)              
//Return the exchange ratio
rate() public view returns (uint256) 
//Return sales
weiRaised() public view returns (uint256)         
//The token is purchased and sent to the specified address        
buyTokens(address beneficiary) public nonReentrant payable  
//Special method
//Return the existing address of the token
tokenWallet() public view returns (address)                 
//Check the number of tokens left in the quota
remainingTokens() public view returns (uint256)
//Set the maximum number of accounts, in bits
setCap(address beneficiary, uint256 cap) external onlyCapper
//Get the quota of the specified account
getCap(address beneficiary) public view returns (uint256)
//Obtain the ETH quantity provided by the specified account
getContribution(address beneficiary) public view returns (uint256)
//Returns whether the specified account has the permission to set quotas
isCapper(address account) public view returns (bool)
//Add quota permission to the specified account
addCapper(address account) public onlyCapper
//Cancel the quota setting permission of the current account
renounceCapper() public
```
