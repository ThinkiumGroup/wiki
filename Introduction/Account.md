### Account

A thinkium account is an entity that owns TKM assets and can send transactions on thinkium. Accounts can be controlled by users or deployed as smart contracts.

#### Account type

Thinkium has two account types:

-User account - an account controlled by the user himself.

-Contract account - a smart contract controlled by code and deployed on the network.

#### Common ground

-Receive, hold and send TKM and token.

-Interact with deployed smart contracts.

#### Different points

##### User account

-Creating an account is free

-Can initiate a transaction

-Transactions between accounts held can only be TKM wallets

##### Contract

-Creating a contract account is costly because you are using networked storage.

-Send the transaction when you receive the transaction (that is, you cannot initiate the transaction without triggering).

-Transactions from account to contract account can trigger code and perform many different operations, such as transferring tokens and even creating a new contract.

#### Public private key certificate

An account consists of a private key, a public key, and an address. When a transaction needs to be sent, it needs to be signed by the sender's private key. Your private key can really manage your assets. This will prevent malicious actors from broadcasting transactions because you can always verify the sender of the transaction.