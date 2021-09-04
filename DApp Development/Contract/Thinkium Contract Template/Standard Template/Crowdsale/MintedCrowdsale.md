# Contract template

## Additionable crowdfunding

> When the token is issued, an initial total amount can be set, or it can be set to 0. The token will be cast only when the token is sold at a specified exchange rate.

> The exchange ratio between token and ETH is set at the same time as the contract is deployed.

> All crowdfunding contracts must be deployed after an ERC20 token has been successfully deployed. The deployment script already has an ERC20 contract that can be issued with additional tokens

[Contract Document: MintedCrowdsale.sol](https://github.com/TxCodeGroup/ContractTemplate/blob/master/contracts/Crowdsale/MintedCrowdsale.sol)

[Test script: MintedCrowdsale.js](https://github.com/TxCodeGroup/ContractTemplate/blob/master/test/Crowdsale/MintedCrowdsale.js)

[Deployment script: 10_deploy_MintedCrowdsale.js](https://github.com/TxCodeGroup/ContractTemplate/blob/master/migrations/10_deploy_MintedCrowdsale.js)

### Define the following variables when deploying the contract
```javascript
uint256 rate               //how many ERC20 tokens are exchanged for 1ETH
address payable wallet     // to receive ETH beneficiary's address
IERC20 token               //token address
```
### ERC20 method needs to be implemented after the crowdfunding contract is placed
```javascript
//Add casting rights for crowdfunding contracts
token.addMinter(crowdsale.address);        
//Revoke casting rights for the current account
token.renounceMinter();                    
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
```
