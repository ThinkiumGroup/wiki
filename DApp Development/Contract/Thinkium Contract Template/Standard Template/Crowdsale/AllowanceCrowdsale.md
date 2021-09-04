# Contract template

## Universal crowdfunding
> The crowdfunding token means that after the token is issued, any address can purchase tokens from the crowdfunding address using ETH.  

> The exchange ratio between token and ETH is set at the same time as the contract is deployed.

> All crowdfunding contracts must be deployed after an ERC20 token has been successfully deployed, and a fixed amount of ERC20 contracts has been set in the deployment script  

[contract documents: AllowanceCrowdsale.sol](https://github.com/TxCodeGroup/ContractTemplate/blob/master/contracts/Crowdsale/AllowanceCrowdsale.sol)

[testing script : AllowanceCrowdsale.js](https://github.com/TxCodeGroup/ContractTemplate/blob/master/test/Crowdsale/AllowanceCrowdsale.js)

[Deployment script: 9_deploy_AllowanceCrowdsale.js](https://github.com/TxCodeGroup/ContractTemplate/blob/master/migrations/9_deploy_AllowanceCrowdsale.js)

### Define the following variables when deploying the contract
```javascript
uint256 rate               //Exchange ratio 1ETH how many ERC20 tokens to exchange
address payable wallet     //Address of the beneficiary receiving ETH
IERC20 token               //Tokens address
address tokenWallet        //The token is sent from this address
```
### Methods erc20 was implemented after the crowdfunding contract was deployed
```javascript
//Tokens in the sender's account must be approved for crowdfunding contracts after deployment  
token.approve(crowdsale.address, SOME_TOKEN_AMOUNT);
```
### Calling methods
```javascript
//Returns the token address
token() public view returns (IERC20)          
//Return beneficiary's address              
wallet() public view returns (address payable)              
//Return conversion ratio
rate() public view returns (uint256) 
//Returned sales
weiRaised() public view returns (uint256)         
//The token is purchased and sent to the specified address          
buyTokens(address beneficiary) public nonReentrant payable  
//Special methods
//Returns the existing address of the token
tokenWallet() public view returns (address)                 
//Check the number of tokens left in the quota
remainingTokens() public view returns (uint256)             
```
