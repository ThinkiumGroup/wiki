# Contract template

## Multi-function ERC20 token, can be issued, can be destroyed, can be suspended, with a cap


[Contract Document: ERC20MultiFunction.sol](https://github.com/TxCodeGroup/ContractTemplate/blob/master/contracts/Multi/ERC20MultiFunction.sol)

[Test script: ERC20MultiFunction.js](https://github.com/TxCodeGroup/ContractTemplate/blob/master/test/Multi/ERC20MultiFunction.js)

[Deployment script: 19_deploy_ERC20MultiFunction.js](https://github.com/TxCodeGroup/ContractTemplate/blob/master/migrations/19_deploy_ERC20MultiFunction.js)

###  Define the following variables when deploying the contract
```javascript
string memory name,     //Token name
string memory symbol,   //tokens for
uint8 decimals,         //precision
uint256 totalSupply,    //Total circulation
uint256 cap             //umber of cap capping
```
### Call methods
```javascript
// Return the token name
name() public view returns (string memory)
// Return token abbreviation
symbol() public view returns (string memory)
// Return token precision
decimals() public view returns (uint8)
// Returns the total number of issues
totalSupply() external view returns (uint256)
// Returns the balance of the specified address
balanceOf(address account) external view returns (uint256)
// Send tokens from the current account to the specified address
transfer(address recipient, uint256 amount) external returns (bool)
// Query the quota given by the owner to spender
allowance(address owner, address spender) external view returns (uint256)
// Approve spender to use the amount token on behalf of the sender
approve(address spender, uint256 amount) external returns (bool)
// Spender calls this function to send the Amount token in the Sender account to the Recipient
transferFrom(address sender, address recipient, uint256 amount) external returns (bool)
// Increase the quota given to Spender
increaseAllowance(address spender, uint256 addedValue) public returns (bool)
// Reduce the quota given to Spender
decreaseAllowance(address spender, uint256 subtractedValue) public returns (bool)
// Query whether the specified address has the right to mint coins
IsMinter (Address Account) Public View returns (bool)
// Add the coinage to the specified address. Only the address with the coinage can be added
Public onlyMinter addMinter (the address of the account)
// Revoke the coinage of the currently sent account
RenounceMinter () to the public
/ / COINS
Mint (Address Account, uint256 Amount) public onlyMinter returns (bool)
// This method is called to destroy tokens from the caller's account
Burn (uint256 amount) to the public
// Call this method to destroy the token from the specified address, and the token is deducted from the sender's approval
BurnFrom (Address Account, uint256 amount) public
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
// Return the number of caps
cap() public view returns (uint256)     
```
