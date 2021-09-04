## Introduction

Thinkium provides four SDKs for the majority of developers, **JS, Java, Go, Python**.

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

Test RPC: **rpctest.thinkium.org**

Production RPC: **rpcproxy.thinkium.org**

