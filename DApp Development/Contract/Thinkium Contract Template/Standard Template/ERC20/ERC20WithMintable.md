# Contract template

## Additional tokens can be issued
>  Issuable tokens are those that can be issued by the account with the right to mint. Casting rights can also be added and revoked.

[Contract Document: ERC20WithMintable.sol](https://github.com/TxCodeGroup/ContractTemplate/blob/master/contracts/ERC20/ERC20WithMintable.sol)

[Test script: ERC20WithMintable.js](https://github.com/TxCodeGroup/ContractTemplate/blob/master/test/ERC20/ERC20WithMintable.js)

[Deployment script: 4_deploy_ERC20WithMintable.js](https://github.com/TxCodeGroup/ContractTemplate/blob/master/migrations/4_deploy_ERC20WithMintable.js)

###  Define the following variables when deploying the contract
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
// Query whether the specified address has the right to mint coins
IsMinter (Address Account) Public View returns (bool)
// Add the coinage to the specified address. Only the address with the coinage can be added
Public onlyMinter addMinter (the address of the account)
// Revoke the coinage of the currently sent account
RenounceMinter () to the public
/ / COINS             
mint(address account, uint256 amount) public onlyMinter returns (bool) 
```
