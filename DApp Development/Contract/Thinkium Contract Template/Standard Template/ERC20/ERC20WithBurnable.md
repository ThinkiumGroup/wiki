# Contract template

## Destructible tokens
> Destructible token means that after the coin is issued, the holder can destroy his own token, or a third party can be responsible for the destruction through approval.

[Contract Document: ERC20WithBurnable.sol](https://github.com/TxCodeGroup/ContractTemplate/blob/master/contracts/ERC20/ERC20WithBurnable.sol)

[Test script: ERC20WithBurnable.js](https://github.com/TxCodeGroup/ContractTemplate/blob/master/test/ERC20/ERC20WithBurnable.js)

[Deployment script: 3_deploy_ERC20WithBurnable.js](https://github.com/TxCodeGroup/ContractTemplate/blob/master/migrations/3_deploy_ERC20WithBurnable.js)

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
// This method is called to destroy tokens from the caller's account
Burn (uint256 amount) to the public
// Call this method to destroy the token from the specified address, and the token is deducted from the sender's approval
BurnFrom (Address Account, uint256 amount) public
```
