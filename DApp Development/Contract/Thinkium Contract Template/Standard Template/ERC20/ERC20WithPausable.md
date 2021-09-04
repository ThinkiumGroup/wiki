# Contract template

## Pause tokens
> A suspended token is a token that can be used to suspend all functions of the token after it is issued by an account that has access to the token, which will be useful in the event of an anomaly in your contract

[Contract Document: ERC20WithPausable.sol](https://github.com/TxCodeGroup/ContractTemplate/blob/master/contracts/ERC20/ERC20WithPausable.sol)

[Test script: ERC20WithPausable.js](https://github.com/TxCodeGroup/ContractTemplate/blob/master/test/ERC20/ERC20WithPausable.js)

[Deployment script: 6_deploy_ERC20WithPausable.js](https://github.com/TxCodeGroup/ContractTemplate/blob/master/migrations/6_deploy_ERC20WithPausable.js)

### Define the following variables when deploying the contract
```javascript
string memory name,     //Token name
string memory symbol,   //Tokens for
uint8 decimals ,        //precision
uint256 totalSupply     //Total circulation
```
### Calling methods
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
// Special method
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
unpause() public onlyPauser whenPaused                    
```
