# Contract template

## Finishable crowdfunding  
> Crowdfunding tokens means that after the token is issued, any address can purchase tokens from the crowdfunding address using ETH.  

> The exchange ratio between token and ETH is set at the time of contract deployment.  

> All crowdfunding contracts must be deployed after an ERC20 token has been successfully deployed. A fixed amount of ERC20 contracts has been set in the deployment script  

> Finalable crowdfunding is the method of ending crowdfunding that is added to the time-limited crowdfunding  

[Contract Document: FinalizableCrowdsale.sol](https://github.com/TxCodeGroup/ContractTemplate/blob/master/contracts/Crowdsale/FinalizableCrowdsale.sol)

[Test script: FinalizableCrowdsale.js](https://github.com/TxCodeGroup/ContractTemplate/blob/master/test/Crowdsale/FinalizableCrowdsale.js)

[Deployment script: 16_deploy_FinalizableCrowdsale.js](https://github.com/TxCodeGroup/ContractTemplate/blob/master/migrations/16_deploy_FinalizableCrowdsale.js)

### extra 
> In the finalizablecrowdsale. sol contract file, you can set a method to end the crowdfunding. Because it is an internal function, it can only be set in the contract file.
```
function _finalization() internal {
    // Write the business logic after crowdfunding, which will be executed when finalize() method is called
    super._finalization();
}
```

### Define the following variables when deploying the contract
```javascript
uint256 rate               //Exchange ratio 1ETH how many ERC20 tokens to exchange
address payable wallet     //Address of the beneficiary receiving ETH
IERC20 token               //Tokens address
address tokenWallet        //The token is sent from this address
uint256 openingTime        // Start time of crowdfunding
uint256 closingTime        // Closing time of crowdfunding
```
### The ERC20 approach needs to be implemented after the crowdfunding contract is placed
```javascript
//Tokens in the sender's account must be approved for crowdfunding contracts after deployment
token.approve(crowdsale.address, SOME_TOKEN_AMOUNT);
```
### Calling methods
```javascript
//Returns the token address
token() public view returns (IERC20)          
//Return beneficiary's address              
wallet() public view returns (address payable)              
//Return conversion ratio
rate() public view returns (uint256) 
//Returned sales
weiRaised() public view returns (uint256)         
//The token is purchased and sent to the specified address       
buyTokens(address beneficiary) public nonReentrant payable  
//Special methods
//Returns the existing address of the token
tokenWallet() public view returns (address)                 
//Check the number of tokens left in the quota
remainingTokens() public view returns (uint256)
//Return to the crowdfunding start time
openingTime() public view returns (uint256)
//Return to the crowdfunding end time
closingTime() public view returns (uint256)
//Returns if the crowdfunding has started
isOpen() public view returns (bool)
//Returns whether the crowdfunding is over
hasClosed() public view returns (bool)
//Returns whether the contract has ended
finalized() public view returns (bool)
//Trigger the contract end method
finalize() public
```
