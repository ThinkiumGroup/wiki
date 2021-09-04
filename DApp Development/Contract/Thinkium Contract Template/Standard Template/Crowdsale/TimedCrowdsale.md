# Contract template

## Time-limited crowdfunding

> The crowdfunding token means that after the token is issued, any address can purchase tokens from the crowdfunding address using ETH.

> The exchange ratio between token and ETH is set at the same time as the contract is deployed.

> All crowdfunding contracts must be deployed after an ERC20 token has been successfully deployed, and a fixed amount of ERC20 contracts has been set in the deployment script

> Time-limited crowdfunding means that the start time and end time of crowdfunding are set

[Contract Document: TimedCrowdsale.sol](https://github.com/TxCodeGroup/ContractTemplate/blob/master/contracts/Crowdsale/TimedCrowdsale.sol)

[test scripts: TimedCrowdsale.js](https://github.com/TxCodeGroup/ContractTemplate/blob/master/test/Crowdsale/TimedCrowdsale.js)

[Deployment script: 14_deploy_TimedCrowdsale.js](https://github.com/TxCodeGroup/ContractTemplate/blob/master/migrations/14_deploy_TimedCrowdsale.js)

### Define the following variables when deploying the contract
```javascript
Uint256 rate 			// how many ERC20 tokens are exchanged for 1ETH
Address payable wallet 	// to receive ETH beneficiary's address
IERC20 token			 // token address
Address tokenWallet		 // Tokens are sent from this address
Uint256 openingTime 		// Start time of crowdfunding
Uint256 closingTime 		// Crowd-funding end time
```
### ERC20 method needs to be implemented after the crowdfunding contract is placed
```javascript
//Tokens in the sender's account must be approved for crowdfunding contracts after deployment
token.approve(crowdsale.address, SOME_TOKEN_AMOUNT);
```
### Calling methods
```javascript 
// Return the token address
Token () Public view returns (IERC20)
// return the beneficiary's address
Wallet () Public View returns (Address payable)
// Return the exchange ratio
Rate () Public View returns (uint256)
// Return sales
WeiRaised () Public View returns (uint256)
// The token is purchased and sent to the specified address
BuyTokens (address beneficiary) public nonReentrant
// Special method
// Return the existing address of the token
TokenWallet () Public View returns (address)
// Check the number of tokens left in the quota
RemainingTokens () Public View Returns (Uint256)
// Return to the crowdfunding start time
OpeningTime () Public View
// Return to the crowdfunding end time
Public View returns (uint256)
// Returns whether the crowdfunding has started
IsOpen () Public View returns (bool)
// Returns whether the crowdfunding is over
hasClosed() public view returns (bool) 
```
