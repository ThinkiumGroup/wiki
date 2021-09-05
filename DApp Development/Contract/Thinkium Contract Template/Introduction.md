# Contract template

This is a contract library based on Openzeppelin, a further simplification and use of the Openzeppelin contract library. Detailed test scripts were made for each contract.



GitHub ：https://github.com/ThinkiumGroup/ContractTemplate



###  Issue ERC20 tokens
- [Fixed total tokens](./Standard Template /ERC20/ERC20FixedSupply.md)
- [can destroy their tokens](./Standard Template /ERC20/ERC20WithBurnable.md)
- [can raise their tokens](./Standard Template /ERC20/ERC20WithMintable.md)
- [is capped their tokens](./Standard Template /ERC20/ERC20WithCapped.md)
- [can suspend their tokens](./Standard Template /ERC20/ERC20WithPausable.md)
### Lock-up contract
- [Issue tokens and lock up](./Standard Template /ERC20/IssueTokenWithTimelock.md)
- [lock up after issued tokens](./Standard Template /ERC20/IssueTokenBeforeTimelock.md)
### Launch crowdfunding tokens
- [Universal crowdfunding](./Standard Template /Crowdsale/AllowanceCrowdsale.md)
- [Scalable crowdfunding](./Standard Template /Crowdsale/MintedCrowdsale.md)
- [Crowdfunding with a cap](./Standard Template /Crowdsale/CappedCrowdsale.md)
- [Crowdfunding with quotas](./Standard Template /Crowdsale/IndividuallyCappedCrowdsale.md)
- [Suspended crowdfunding](./Standard Template /Crowdsale/PausableCrowdsale.md)
- [Time-limited crowdfunding](./Standard Template /Crowdsale/TimedCrowdsale.md)
- [Whitelist crowdfunding](./Standard Template /Crowdsale/WhitelistCrowdsale.md)
- [Terminable crowdfunding](./Standard Template /Crowdsale/FinalizableCrowdsale.md)
- [Crowdfunding to be delivered at maturity](./Standard Template /Crowdsale/PostDeliveryCrowdsale.md)
- [Crowdfunding for unsuccessful refunds](./Standard Template /Crowdsale/RefundableCrowdsale.md)

### Multifunction contract
- [Multi-function ERC20 token, can be issued, can be destroyed, can be suspended, there is a cap](./Standard Template /Multi/ERC20MultiFunction.md)
- [Multi-function crowdfunding contract: additional issuance, destruction, capping, quota, suspension, time limit, whitelist, successful delivery, unsuccessful refund  ](./Standard Template /Multi/MultiFunctionCrowdsale.md)
- [Joint-stock beneficiary agreement](./Standard Template /Multi/CrowdsalePaymentSplitter.md)

### Issue ERC777 tokens
- [ERC777 tokens,](./Standard Template /ERC777/ERC777Contract.md)

### Issue ERC721 tokens
- [Fully functional ERC721 tokens](./Standard Template /ERC721/ERC721Full.md)
- [Destructible ERC721 tokens](./Standard Template /ERC721/ERC721Burnable.md)
- [ERC721 tokens can be minted](./Standard Template /ERC721/ERC721Mintable.md)
- [A suspended ERC721 token](./Standard Template /ERC721/ERC721Pausable.md)

### Draft 
- [Token migration contract](./Standard Template /Multi/ERC20Migrator.md)
- [Snapchable ERC20 tokens](./Standard Template /Multi/ERC20WithSnapshot.md)
- [Release contract](./Standard Template /Multi/ERC20WithTokenVesting.md)

---
### Install
```shell
$ npm install            //Installing dependency packages
```
### Deploy to the test node
```shell
$ npm run compile        //Compile the contract
$ npm run node           //Open a test node
$ npm run test           //Test contract
$ npm run migrate        //Deploy the contract to the test node
```
### Deploy the contract to truffle  
```shell
$ truffle develop           //Open the Truffle development environment  
truffle(develop)> compile   //Compile the contract
truffle(develop)> test      //Test contract
truffle(develop)> migrate   //Deploy contracts
```

