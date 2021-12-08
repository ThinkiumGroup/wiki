## Zero-Cost Migrate DApp on Other Chains to Thinkium Chain Guideline

 

![img](https://thinkium-wiki.s3.ap-northeast-1.amazonaws.com/migrate/en-1.png) 

 

**DApp Construction**

1. MetaMask (Private Key management Plugin)

(Installation website: https://chrome.google.com/webstore/detail/metamask/nkbihfbeogaeaoehlefnkodbefgpgknn )

2. DApp front-end program (business logic implementation)

3. DApp back-end program (service of the business)

4. DApp contract (smart contracts deployed to blockchain are not changeable)





**Assuming DApp has been deployed to the ETH or BSC, and running normally. Please follow the next four key steps if you want to relocate your DApp to Thinkium. **



**1. Deploy DApp smart contract to Thinkium (70001 chain, 70002 chain, or 70103 chain), (shown as step 1 from the graphic)**



**2. Configure DApp contract address to front-end or back-end service (shown as step 2 and 6)**

The deployer’s blockchain address includes its nonce value, which is increased based the time of transactions were made in blockchains. However, there is no further step needed to adjust if the nonce value of the deployer’s blockchain address on Thinkium is the same as the deployer had in other chains when the dapp’s contracts are deployed. If not, please follow step 2 and step 6 of the guideline to change the address.



**3.Configure Thinkium’s RPC and chain ID to background service, and then send transactions to Thinkium after signing them.**



**4.Adding Thinkium’s RPC to MetaMask **

 

4.1 Please ignore this step if you have already installed MetaMask. 

Installation web: https://chrome.google.com/webstore/detail/metamask/nkbihfbeogaeaoehlefnkodbefgpgknn

 

4.2 Log in MetaMask Wallet, and then add the network (shown as below)

![img](https://thinkium-wiki.s3.ap-northeast-1.amazonaws.com/migrate/en-2.png) 

 

4.3 Adding the network (shown as below). Please be aware of which chain your contract has been deployed, because Thinkium has multiple chains. 

![img](https://thinkium-wiki.s3.ap-northeast-1.amazonaws.com/migrate/en-3.png)

 

| Network Name               | RPC URL                          | Chain ID | Symbol | Browsers                           |
| -------------------------- | -------------------------------- | -------- | ------ | ---------------------------------- |
| Thinkium Mainnet Chain 1   | https://proxy1.thinkiumrpc.net   | 70001    | TKM    | https://chain1.thinkiumscan.net/   |
| Thinkium Mainnet Chain 2   | https://proxy2.thinkiumrpc.net   | 70002    | TKM    | https://chain2.thinkiumscan.net/   |
| Thinkium Mainnet Chain 103 | https://proxy103.thinkiumrpc.net | 70103    | TKM    | https://chain103.thinkiumscan.net/ |

Now your can visit your DApp on Thinkium. 

