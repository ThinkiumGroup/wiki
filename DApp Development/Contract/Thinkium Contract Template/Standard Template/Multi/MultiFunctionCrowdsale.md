# Contract template


## Multi-function crowdfunding contract: additional issuance, destruction, capping, quota, suspension, time limit, whitelist, successful delivery, unsuccessful refund


[Contract Document: MultiFunctionCrowdsale.sol](https://github.com/TxCodeGroup/ContractTemplate/blob/master/contracts/Multi/MultiFunctionCrowdsale.sol)

[Test script: MultiFunctionCrowdsale.js](https://github.com/TxCodeGroup/ContractTemplate/blob/master/test/Multi/MultiFunctionCrowdsale.js)

[Deployment script: 20_deploy_MultiFunctionCrowdsale.js](https://github.com/TxCodeGroup/ContractTemplate/blob/master/migrations/20_deploy_MultiFunctionCrowdsale.js)

### Define the following variables when deploying the contract
```javascript
uint256 rate              //how many ERC20 tokens are exchanged for 1ETH
address payable wallet // to receive ETH beneficiary's address
IERC20 token // token address
Uint256 openingTime // Start time of crowdfunding
Uint256 closingTime // Crowd-funding end time
Uint256 goal // Crowdfunding goal
Uint256 cap // Number of cap capping, in wei
```
### ERC20 method needs to be implemented after the crowdfunding contract is placed
```javascript
Add casting rights for crowdfunding contracts
Token. AddMinter (crowdsale. Address);
// Revoke casting rights for the current account
token.renounceMinter();  
```
### Calling methods
```javascript
//Return the token address
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
// This method is called to destroy tokens from the caller's account
Burn (uint256 amount) to the public
// Call this method to destroy the token from the specified address, and the token is deducted from the sender's approval
BurnFrom (Address Account, uint256 amount) public
// Return the number of caps
Cap () Public View (uint256)
// Set the maximum number of accounts in wei
setCap(address beneficiary, uint256 cap) external onlyCapper
// Get the quota of the specified account
getCap(address beneficiary) public view returns (uint256)
// Obtain the ETH quantity provided by the specified account
getContribution(address beneficiary) public view returns (uint256)
// Returns whether the specified account has the permission to set quotas
isCapper(address account) public view returns (bool)
// Add quota permission to the specified account
addCapper(address account) public onlyCapper
// Cancel the quota setting permission of the current account
renounceCapper() public
// Returns whether the specified address has the pause right
IsPauser (Address Account) Public View returns (bool)
// Add pause permission to the specified address
Public onlyPauser addPauser (the address of the account)
// Cancel the suspension right of the current sending account
RenouncePauser () to the public
// Returns whether the contract is currently suspended
Paused () public view returns (bool)
// Suspend the contract
Pause () public onlyPauser whenNotPaused
// Resume the contract
Unpause () public onlyPauser whenPaused
// Return to the crowdfunding start time
openingTime() public view returns (uint256)
// Return to the crowdfunding end time
closingTime() public view returns (uint256)
// Returns whether the crowdfunding has started
isOpen() public view returns (bool)
// Returns whether the crowdfunding is over
hasClosed() public view returns (bool)
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
// Returns whether the contract has ended
finalized() public view returns (bool)
// Trigger the contract end method
finalize() public
// Returns the number of ERC20 stored on the contract
balanceOf(address account) public view returns (uint256)
// After the public funding is completed and the crowdfunding target is reached, the trigger can extract ERC20
withdrawTokens(address beneficiary) public
// Return crowdfunding target,ETH number
goal() public view returns (uint256)
// Trigger this method to give buyers a refund when the target is not reached after the public funding is completed
claimRefund(address payable refundee) public
// Returns whether the crowdfunding target has been reached
goalReached() public view returns (bool)
```
