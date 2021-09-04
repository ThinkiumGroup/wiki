# Contract template

## Snapshotable ERC20 tokens
> Snapshotable ERC20 tokens extend the ERC20 token with the snapshot mechanism. After the snapshot is created, the current balance and total supply are recorded for later access.

>  The Snapshot is created by the internal Snapshot function, which issues a Snapshot event and returns the Snapshot ID. To get the totalSupplyAt the time of the snapshot, totalSupplyAt calls this function with the snapshot ID. To get the account balance at snapshot time, balanceOfAt calls this function with the snapshot ID and account address.

[Contract Document: ERC20WithSnapshot.sol](https://github.com/TxCodeGroup/ContractTemplate/blob/master/contracts/Multi/ERC20WithSnapshot.sol)

[Test script: ERC20WithSnapshot.js](https://github.com/TxCodeGroup/ContractTemplate/blob/master/test/Multi/ERC20WithSnapshot.js)

[Deployment script: 26_deploy_ERC20WithSnapshot.js](https://github.com/TxCodeGroup/ContractTemplate/blob/master/migrations/26_deploy_ERC20WithSnapshot.js)

### Define the following variables when deploying the contract
```javascript
string memory name,     //Token name
string memory symbol,   //tokens for
uint8 decimals,         //precision
uint256 totalSupply     //Total circulation
```
### Calling methods
```javascript
//Return the token name
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
// A special method for the snapshot contract
// Create a snapshot
snapshot() public returns (uint256)
// Query the balance of the specified address based on the snapshot ID
balanceOfAt(address account, uint256 snapshotId) public view returns (uint256)
// Query the total number of issued snapshots based on the snapshot ID
totalSupplyAt(uint256 snapshotId) public view returns(uint256)
//
```
