# Contract template
## Whitelist crowdfunding
> The crowdfunding token means that after the token is issued, any address can purchase tokens from the crowdfunding address using ETH.

> The exchange ratio between token and ETH is set at the same time as the contract is deployed.

> All crowdfunding contracts must be deployed after an ERC20 token has been successfully deployed, and a fixed amount of ERC20 contracts has been set in the deployment script

> Whitelisted crowdfunding means that only those accounts that are whitelisted can participate in crowdfunding to buy tokens

[Contract Document: WhitelistCrowdsale.sol](https://github.com/TxCodeGroup/ContractTemplate/blob/master/contracts/Crowdsale/WhitelistCrowdsale.sol) 

[Test script: WhitelistCrowdsale.js](https://github.com/TxCodeGroup/ContractTemplate/blob/master/test/Crowdsale/WhitelistCrowdsale.js) 

[Deployment script: 15_deploy_WhitelistCrowdsale.js](https://github.com/TxCodeGroup/ContractTemplate/blob/master/migrations/15_deploy_WhitelistCrowdsale.js) 

### Define the following variables when deploying the contract
```javascript
Uint256 rate 			// how many ERC20 tokens are exchanged for 1ETH
Address payable wallet // to receive ETH beneficiary's address
IERC20 token 			// token address
Address tokenWallet		 // Tokens are sent from this address
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
remainingTokens() public view returns (uint256)
// Returns whether the specified account is whitelisted
isWhitelisted(address account) public view returns (bool)
// Add the specified account to the whitelist
addWhitelisted(address account) public onlyWhitelistAdmin
// Remove the specified account from the whitelist
removeWhitelisted(address account) public onlyWhitelistAdmin
// Remove your account from the whitelist
renounceWhitelisted() public
// Returns whether the specified account is a whitelist administrator
isWhitelistAdmin(address account) public view returns (bool)
// Add the specified account to the whitelist administrator
addWhitelistAdmin(address account) public onlyWhitelistAdmin
// Remove your account from the whitelist administrator
renounceWhitelistAdmin() public
```
