# Contract template
## Fixed total tokens

> Fixed total token is the most basic ERC20 token, which contains four basic information: token name, token abbreviation, precision and hairstyle total.

[Contract Document: ERC20FixedSupply.sol](https://github.com/TxCodeGroup/ContractTemplate/blob/master/contracts/ERC20/ERC20FixedSupply.sol)

[test scripts: ERC20FixedSupply.js](https://github.com/TxCodeGroup/ContractTemplate/blob/master/test/ERC20/ERC20FixedSupply.js)

[Deployment script: 2_deploy_ERC20FixedSupply.js](https://github.com/TxCodeGroup/ContractTemplate/blob/master/migrations/2_deploy_ERC20FixedSupply.js)

### Define the following variables when deploying the contract
```javascript
string memory name,     // Token name
string memory symbol,   //Tokens for
uint8 decimals,         //precision
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
```
