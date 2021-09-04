# Contract template

## ERC777token

### presentation 
ERC777 Like ERC20, ERC777 is the standard for alternative tokens and focuses on allowing more complex interactions when trading tokens. The standard also brought several improvements, such as the elimination of the ambiguous Decimals, whose killer feature was the send and receive hooks. The hook method is a function in the contract that is called when tokens are sent and received to it, meaning that accounts and contracts can react to sending and receiving tokens.

### file
[Contract Document: ERC777Contract.sol](https://github.com/TxCodeGroup/ContractTemplate/blob/master/contracts/ERC777/ERC777Contract.sol)

[Sending interface contract: TokensSender.sol](https://github.com/TxCodeGroup/ContractTemplate/blob/master/contracts/ERC777/TokensSender.sol)

[Receiving interface contract: TokensRecipient.sol](https://github.com/TxCodeGroup/ContractTemplate/blob/master/contracts/ERC777/TokensRecipient.sol)

[test scripts: ERC777Contract.js](https://github.com/TxCodeGroup/ContractTemplate/blob/master/test/ERC777/ERC777Contract.js)

[Deployment script: 29_deploy_ERC777Contract.js](https://github.com/TxCodeGroup/ContractTemplate/blob/master/migrations/29_deploy_ERC777Contract.js)
### deploy 
####  ERC777 contracts
Define the following variables when deploying the contract
```javascript
string memory name, //Token name
string memory symbol, //tokken
uint256 initialSupply, //publish total
address[] memory defaultOperators //Default operator array
```
#### Send interface contract
In call ERC777 contract delivery method (transfer, send, burn, operatorSend, operatorBurn), the contract will be to ERC1820 registry of sender sent interface address, if the sender send interface contract address registered, send the tok interface contract The ensToSend() method is called. The following is how the send interface contract is deployed and registered.
Define the following variables when deploying the contract
```javascript
bool _setInterface // Whether to register an interface for the contract itself
```
Register the interface after deploying the contract
```javascript
await ERC1820Registry.setInterfaceImplementer(
    senderAddress,//Address of the account that sent the token
    web3.utils.keccak256("ERC777TokensSender"),//The keccak256 hash of the ERC777TokensSender interface
    TokensSender.address,//Address of the sending interface contract
);
```
#### Receive interface contract
In call ERC777 contract delivery method (transfer, send, burn, operatorSend, operatorBurn), the contract will be to receiving interface ERC1820 registry query the receiver address, if the receiver address, registered the receiving interface contracts tok in receiving interface contract The ensReceived() method is called. The following is how the receiving interface contract is deployed and registered.
Define the following variables when deploying the contract
```javascript
bool _setInterface //Whether to register an interface for the contract itself
```
Register the interface after deploying the contract
```javascript
await ERC1820Registry.setInterfaceImplementer(
    receiverAddress,//Account address for sending tokens
    web3.utils.keccak256("ERC777TokensRecipient"),//The keccAK256 hash of the ERC777TokensRecipient interface
    TokensRecipient.address,//receiving interface address
);
```
### ERC777 calls the method
#### compatible with ERC20 methods

```javascript
Return the token name
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
// This method is called to destroy tokens from the caller's account
burn(uint256 amount) public 
```
#### ERC777 Added method
```javascript
//Returns the smallest unit of the token
granularity() public view returns (uint256)
// Replace the transfer method
send(address recipient, uint256 amount, bytes memory data) public
// Validates the operator address of the specified address
isOperatorFor(address operator,address tokenHolder) public view returns (bool)
// Set operator for current account
authorizeOperator(address operator) public
// Undo operator for the current account
revokeOperator(address operator) public
// Returns an array of default operators
defaultOperators() public view returns (address[] memory)
// The operator sends the method
operatorSend(address sender,address recipient,uint256 amount,bytes memory data,bytes memory operatorData)
// Operator destruction methodmemory operatorData) public
```
#### Send interface contract
```javascript
//When ERC777 tokens are sent, this interface is called after the sending interface contract is found in the ERC1820 registry
tokensToSend(address _operator,address _from,address _to,uint _amount,bytes calldata _data,bytes calldata _operatorData)external
//Accept the token sending method
AcceptTokensToSend () public onlyOwner
// Reject the token sending method
rejectTokensToSend() public onlyOwner
```
#### Receive interface contract
```javascript
// When ERC777 tokens are sent, this interface is called after the receiving interface contract is found in the ERC1820 registry
tokensReceived(address _operator,address _from,address _to,uint _amount,bytes calldata _data,bytes calldata _operatorData)external
// Accept the receiving token method
AcceptTokens () public onlyOwner
// Reject the token method
rejectTokens() public onlyOwner
```