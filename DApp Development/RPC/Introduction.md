## Introduction

The RPC service is the link between the SDK and the nodes on the chain.

The RPC service has the capability of load balancing and fault-tolerant processing.

One RPC service can connect to multiple nodes.

If a node is down while other nodes are live, it will not affect the RPC service, and then the Dapp application will not be affected.



Currently, the official RPC service for testing and production environments is provided, and developers can choose which one to use when using the SDK.



Test RPC：**rpctest.thinkium.org**

Production RPC：**rpcproxy.thinkium.org**

