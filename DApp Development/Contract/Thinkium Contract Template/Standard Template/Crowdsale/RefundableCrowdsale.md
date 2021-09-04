# Contract template

## Crowdfunding for unsuccessful refunds

> The crowdfunding token means that after the token is issued, any address can purchase tokens from the crowdfunding address using ETH.

> The exchange ratio between token and ETH is set at the same time as the contract is deployed.

> All crowdfunding contracts must be deployed after an ERC20 token has been successfully deployed, and a fixed amount of ERC20 contracts has been set in the deployment script

> Unsuccessful refund crowdfunding refers to crowdfunding goals (measured by ETH number) set on top of successful crowdfunding delivered.

> If the crowdfunding target is not reached after the public funding time, the purchaser can return ETH through claimRefund().

> When the crowdfunding time arrives, the buyer can only withdraw the ERC20 token using a Deposite () method if the crowdfunding target is reached.

### Crowdfunding rules:
1. Exchange rate 1ETH:100ERC20
2. Tokens are deposited in accounts[0]
3. The ETH obtained through crowdfunding is handed over to accounts[1]
4. The start time of crowdfunding is the current time
5. Crowdfunding ends in 5 seconds
6. The crowdfunding target is 20 Eth
7. If you don't reach your crowdfunding goal, you can get a refund after the crowdfunding ends
8. Reach the crowdfunding goal and withdraw tokens after the crowdfunding ends

[Contract Document: RefundableCrowdsale.sol](https://github.com/TxCodeGroup/ContractTemplate/blob/master/contracts/Crowdsale/RefundableCrowdsale.sol)

[Test script1(Reach crowdfunding goal): RefundableCrowdsaleReached.js](https://github.com/TxCodeGroup/ContractTemplate/blob/master/test/Crowdsale/RefundableCrowdsaleReached.js)

[Test script2(failed to reach crowdfunding target): RefundableCrowdsaleNotReach.js](https://github.com/TxCodeGroup/ContractTemplate/blob/master/test/Crowdsale/RefundableCrowdsaleNotReach.js)

[Deployment script: 18_deploy_RefundableCrowdsale.js](https://github.com/TxCodeGroup/ContractTemplate/blob/master/migrations/18_deploy_RefundableCrowdsale.js)

###  Define the following variables when deploying the contract
```javascript
uint256 rate               //how many ERC20 tokens are exchanged for 1ETH
Address payable wallet	   // to receive ETH beneficiary's address
IERC20 token 			   // token address
Address tokenWallet 	   // Tokens are sent from this address
Uint256 openingTime 	   // Start time of crowdfunding
Uint256 closingTime	   	   // Crowd-funding end time
Uint256 goal 			   // Crowdfunding goal
` ` `
### ERC20 method needs to be implemented after the crowdfunding contract is placed
​```javascript
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
// Return sales
weiRaised() public view returns (uint256)         
//The token is purchased and sent to the specified address        
buyTokens(address beneficiary) public nonReentrant payable  
//Special method
//Return the existing address of the token
tokenWallet() public view returns (address)                 
//Check the number of tokens left in the quota
remainingTokens() public view returns (uint256)
//Return to the crowdfunding start time
openingTime() public view returns (uint256)
//Return to the crowdfunding end time
closingTime() public view returns (uint256)
//Returns whether the crowdfunding has started
isOpen() public view returns (bool)
//Returns whether the crowdfunding is over
hasClosed() public view returns (bool)
//Returns whether the contract has ended
finalized() public view returns (bool)
//Trigger the contract end method
finalize() public
//Returns the number of ERC20 stored on the contract
balanceOf(address account) public view returns (uint256)
//After the public funding is completed and the crowdfunding target is reached, the trigger can extract ERC20
withdrawTokens(address beneficiary) public
//Return crowdfunding target,ETH number
goal() public view returns (uint256)
//Trigger this method to give buyers a refund when the target is not reached after the public funding is completed
claimRefund(address payable refundee) public
//Returns whether the crowdfunding target has been reached
goalReached() public view returns (bool)
```
