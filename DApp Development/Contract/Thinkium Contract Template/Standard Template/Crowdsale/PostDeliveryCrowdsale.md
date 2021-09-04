# Contract template

## Crowdfunding to be delivered after expiration 
> The crowdfunding token means that after the token is issued, any address can purchase tokens from the crowdfunding address using ETH.

>  The exchange ratio between token and ETH is set at the same time as the contract is deployed.

> All crowdfunding contracts must be deployed after an ERC20 token has been successfully deployed, and a fixed amount of ERC20 contracts has been set in the deployment script

> Crowdfunding delivered after maturity refers to a time-limited crowdfunding and terminable crowdfunding basis. Only when the crowdfunding time reaches and the closing method is triggered, can the purchaser withdraw the ERC20 token through a Deposite () method

[Contract Document: PostDeliveryCrowdsale.sol](https://github.com/TxCodeGroup/ContractTemplate/blob/master/contracts/Crowdsale/PostDeliveryCrowdsale.sol)

[Test script: PostDeliveryCrowdsale.js](https://github.com/TxCodeGroup/ContractTemplate/blob/master/test/Crowdsale/PostDeliveryCrowdsale.js)

[Deployment script: 17_deploy_PostDeliveryCrowdsale.js](https://github.com/TxCodeGroup/ContractTemplate/blob/master/migrations/17_deploy_PostDeliveryCrowdsale.js)

### Define the following variables when deploying the contract
```javascript
uint256 rate               //how many ERC20 tokens are exchanged for 1ETH
address payable wallet     //to receive ETH beneficiary's address
IERC20 token               //token address
address tokenWallet        //Tokens are sent from this address
uint256 openingTime        // Start time of crowdfunding
uint256 closingTime        //  Crowd-funding end time
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
// Return the existing address of the token
tokenWallet() public view returns (address)                 
//Check the number of tokens left in the quota
remainingTokens() public view returns (uint256)
//Return to the crowdfunding start time
openingTime() public view returns (uint256)
// Return to the crowdfunding end time
closingTime() public view returns (uint256)
//Returns whether the crowdfunding has started
isOpen() public view returns (bool)
// Returns whether the crowdfunding is over
hasClosed() public view returns (bool)
//Returns the number of ERC20 stored on the contract
balanceOf(address account) public view returns (uint256)
//ERC20 can be withdrawn at the end of the public funding
withdrawTokens(address beneficiary) public
```
