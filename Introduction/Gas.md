### Gas fee

Gas is very important to thinkium. It is one of the foundations of thinkium's operation. Each transaction on thinkium needs to pay gas fees.

#### What is gas？

Gas is a unit that measures the amount of computing effort required to perform specific operations on the thinkum network.

Since each thinkium transaction requires computing resources to execute, each transaction requires a fee. Gas refers to the cost of successful transactions on thinkium.

Gas fees are paid in TKM, thinkium's local currency. The gas price is expressed in Gwei, which itself is the denomination of TKM - each Gwei is equal to 0.000000001 TKM (10 - 9 TKM). For example, instead of spending 0.000000001 TKM on your gas, you can say that your gas costs 1 Gwei“ The word "Gwei" itself means "Giga Wei", which is equal to 1000000000 Wei. Wei itself is the smallest unit of TKM.

#### Gas cost calculation

Ordinary transfer: fixed charge of 0.01 TKM

Contract transaction: calculated according to the actual consumption of the contract

Cross chain transfer: calculated according to the actual consumption steps of the cross chain system contract (about 0.08 TKM)

#### What is gas limit?

Gas limit refers to the maximum amount of gas you are willing to consume in the transaction. More complex transactions involving smart contracts require more computational work, so they require higher gas limits than simple payments.

If you specify too few gas, for example, the gas of simple TKM transfer is lower than 0.01 TKM (for example, 0.005), 0.005 TKM will be consumed to try to run the transfer, but it will not be completed. The chain then reverts to any changes, but gas is consumed because the miner has completed work worth 0.005 TKM.