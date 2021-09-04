# Contract template

## Suspended crowdfunding
> The crowdfunding token means that after the token is issued, any address can purchase tokens from the crowdfunding address using ETH.

> The exchange ratio between token and ETH is set at the same time as the contract is deployed.

> All crowdfunding contracts must be deployed after an ERC20 token has been successfully deployed, and a fixed amount of ERC20 contracts has been set in the deployment script

[Contract Document: PausableCrowdsale.sol](https://github.com/TxCodeGroup/ContractTemplate/blob/master/contracts/Crowdsale/PausableCrowdsale.sol)

[Test script: PausableCrowdsale.js](https://github.com/TxCodeGroup/ContractTemplate/blob/master/test/Crowdsale/PausableCrowdsale.js)

[Deployment script: 13_deploy_PausableCrowdsale.js](https://github.com/TxCodeGroup/ContractTemplate/blob/master/migrations/13_deploy_PausableCrowdsale.js)

### Define the following variables when deploying the contract
```javascript
uint256 rate               //how many ERC20 tokens are exchanged for 1ETH
address payable wallet     // to receive ETH beneficiary's address
IERC20 token               // token address
address tokenWallet        //Tokens are sent from this address
```
### ERC20 method needs to be implemented after the crowdfunding contract is placed
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
//Returns whether the specified address has the pause right
isPauser(address account) public view returns (bool)       
//Add pause permission to the specified address
addPauser(address account) public onlyPauser              
//Cancel the suspension right of the current sending account
renouncePauser() public        
//Returns whether the contract is currently suspended                      
paused() public view returns (bool)                    
//Suspend the contract
pause() public onlyPauser whenNotPaused         
//Resume the contract         
unpause() public onlyPauser whenPaused                   
```
