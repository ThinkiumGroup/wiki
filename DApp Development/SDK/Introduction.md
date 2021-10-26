## Introduction

Thinkium is compatible with the development interface of Ethereum, so it can directly use the SDK of Ethereum for chain development.

Ethereum SDK docs:   [https://ethereum.org/zh/developers/docs/programming-languages/]( https://ethereum.org/zh/developers/docs/programming-languages/)



If you want to do **cross-chain development**, you need to download the official Thinkium SDK. Currently we provide four language versions **JS**, **Java**, **Go**, **Python**.



This document is easy to check what interfaces are supported on the chain. For specific usage, it is recommended to download the SDK of the corresponding language. There are detailed test cases in the SDK.



JS SDK address: [https://github.com/ThinkiumGroup/web3.js](https://github.com/ThinkiumGroup/web3.js)

Java SDK address: [https://github.com/ThinkiumGroup/web3j](https://github.com/ThinkiumGroup/web3j)

Go SDK address: [https://github.com/ThinkiumGroup/web3.go](https://github.com/ThinkiumGroup/web3.go)

Python SDK address: [https://github.com/ThinkiumGroup/web3.py](https://github.com/ThinkiumGroup/web3.py)



Thinkium has a multi-chain structure, and account addresses have different asset status in different chains.

Currently supports 3 sub-chains:

chain 1 , account chain

chain 2 , POS chain

chain 103 , business chain
(In the future, more sub-chains will be added according to the specific business)



RPC address: The RPC is used to interact with the chain. The following is the official RPC address. If you build the chain node yourself. You can deploy your own RPC service and connect to your own RPC address while development.



TestNet:

Account Chain : **test1.thinkiumrpc.net**  chainId: **100008**

PoS Chain : **test2.thinkiumrpc.net**  chainId: **100009**

Business Chain : **test103.thinkiumrpc.net** chainId : **100110**

Cross Chain: **test.thinkiumrpc.net**



MainNet:

Account Chain : **proxy1.thinkiumrpc.net**  chainId: **100008**

PoS Chain : **proxy2.thinkiumrpc.net**  chainId: **100009**

Business Chain : **proxy103.thinkiumrpc.net** chainId : **100110**

Cross Chain: **proxy.thinkiumrpc.net** 
