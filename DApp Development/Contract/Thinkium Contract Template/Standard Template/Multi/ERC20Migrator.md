# Contract template

## Token migration contract
>  A token migration contract is a contract that needs to be abandoned after an ERC20 contract has been installed for some reason. Each ERC20 token holder must choose to participate in the migration. To opt-in, users must approve the number of ERC20 tokens they want to migrate for this contract. After the Settings are approved, anyone can trigger migration to a new token contract. In this way, token holders "hand over" their old balance and will mint an equal amount of ERC20 tokens in the new ERC20 token. New ERC20 token contracts must be mineable. The balance of the old ERC20 token will be left in the migration contract and will remain there forever.

[contract files: ERC20Migrator.sol](https://github.com/TxCodeGroup/ContractTemplate/blob/master/contracts/Multi/ERC20Migrator.sol)

[test scripts: ERC20Migrator.js](https://github.com/TxCodeGroup/ContractTemplate/blob/master/test/Multi/ERC20Migrator.js)

[Deployment script: 25_deploy_ERC20Migrator.js](https://github.com/TxCodeGroup/ContractTemplate/blob/master/migrations/25_deploy_ERC20Migrator.js)

### Define the following variables when deploying the contract
```javascript
IERC20 legacyToken,    //Old ERC20 contract address
```
### The contract shall be executed after deployment
```javascript
//All users of the old contract must approve tokens in their accounts to the migration contract after deployment
token.approve(migrator.address, ALL_TOKEN_AMOUNT);
// Add migration contract casting rights to new tokens
NewTokentoken. AddMinter (migrator. Address);
// Revoke casting rights for the current account
NewTokentoken. RenounceMinter ();
// Set the new token contract address and start the migration
migrator.beginMigration(newToken.address);
```
### Calling methods
```javascript
//return the old contract address
LegacyToken () Public View returns (IERC20)
// return the new contract address
newToken() public view returns (IERC20)
// Set the new token contract address and start the migration
beginMigration(ERC20Mintable newToken_) public
// Migrate the specified number of tokens from the specified account to the new contract
migrate(address account, uint256 amount) public
// Migrate all tokens from the specified account to the new contract
migrateAll(address account) public
```
