https://s3-us-west-2.amazonaws.com/t-chain-data/dev/1649233499781.png

**WHAT IS THINKIUM?**

Thinkium is an all encompassing public chain network that runs through a hierarchical multi-level chain structure and integrates Layer1+Layer2 technologies in order to achieve unlimited scalability at linear cost. 

**THINKIUM ECOlOGY**

In Thinkium, different subjects interact according to distinct constraints and extend to the physical world. The interaction between these things becomes increasingly intricate when more subjects are introduced.

All personal data belongs to users in the Thinkium ecosystem. Authorization is a must for any institution or individual to read these data. Assets can be circulated freely across the ecology and are stored as tokens which can be verified, traced and exchanged whenever needed.

**Dual Coin Ecosytem**

Thinkium provides a support for the establishment of independent industry ecology for subchains where each subchain. Aside from the basic token, each subchain (and the chain tree it is based on) can hold a second token that can be used for business applications and market circulation within the subchain system. Thinkium also allows several chains with connected businesses to be grouped in a tree-structure, with all branches inheriting the settings of the parent chain's second generation tokens. This trait allows second-generation tokens to be moved across chains with connected businesses via cross-chain transactions, effectively solving the cross-chain problem posed by the ERC20 contract's inherent qualities.

**Single chain** 

Thinkium is able to connect infinitely to all digital assets in the blockchain existing today while allowing all asset to efficiently work together on the Thinkium chain. Thinkium has the option to create an independent single-chain, which can assist early-stage small enterprises in adopting the Thinkium blockchain when they need to create an application chain customized for their specific case at a low cost. It's possible that when the independent single-chain develops, it'll need to interface with other chains. These single chains are able to connect to the main chain via full-chain mapping to gain access to a wider ecological realm.

Thinkium is able to achieve unlimited scalability. On the public chain, application scope can be widened limitlessly so that it can handle the landing of large-scale Web-level apps and the needs of the users therefore, bridging the gap between the virtual and physical world as we advance into the web 3.0 era.



**THINKIUM CORE ENGINE**

With a consensus protocol, the thinkium core engine ensures that different nodes runs the same content and ensures that any node can join without permission.

The Thinkium core engine begins with solving problems in actual businesses by enabling support for massive user level applications including decentralization, consistency and issues of scalability of the public chain, and is able to address the multi-chain parallel capability needs and ability to confirm fast transaction confirmation, very high system security and availability, high-frequency transaction carrying capacity, Turing completeness of smart contracts, high flexibility, and scalability of the system, simple development capabilities, data privacy, etc.

Thinkium core engine’s chain structure is hierarchical and multi-level divided into two types which are:

·    Main chain

·    Business chain

Each chain is a self-contained system with its own state. The main chain serves as the overall system's leader and coordinator. It maintains the metadata and summary of each business chain's confirmed blocks, creates random seeds for all chains' committee elections, and records the election results. The workload is spread across all business chains at the same time, and the contract is generated in parallel using a message-driven protocol based on the Actor model. By updating and verifying the blocks of the main chain, all nodes in the system can ensure that any block data from the main chain has been included in the business chain.

This structure has the following main advantages:

-  Each chain's consensus is carried out independently and in parallel, reducing network bandwidth and computing processing needs significantly.
-  Nodes entering the system simply need to receive the current state of the main chain from a trustworthy source or rebuild from the parent block, and they do not need to synchronize all of the system's data, significantly reducing the overall load.
-  The main chain can serve as the system's coordinator, allowing for cross-chain synchronization and dynamic changes to the system's topology.
-  To validate transactions originated from another business chain, nodes can utilize the main chain's summary and Merkle proof. As a result, the business chain's block producer does not require information from other business chains in order to perform inter-chain transactions.

A four-layer implementation architecture is created to permit future scalability and update of the system based on the hierarchical multi-level chain structure described above.

The first layer is primarily concerned with broad system-wide consensus and is in charge of splitting requests and nodes, as well as allocating various requests to different committees for processing.

The second layer is primarily responsible for solving the single-chain consensus problem, as well as processing requests and generating logs. Each committee is made up of a number of nodes.

The third layer is mostly concerned with solving consensus among numerous chains. The logs and request data generated by each committee are combined into a single log using a specified encoding scheme. The system's purpose is to provide a consistent log for each node. As a result, aggregation methods are required to combine all of the logs created by the committee's nodes into a single log.

The network layer is the fourth layer, and it is the basic layer that makes connections and facilitates communication between nodes.

**Implementation of the consensus protocol**

There are three types of nodes in each chain in the Thinkium core engine:

-  data nodes, 

- consensus nodes, and 

- ordinary nodes. 

  The data node is in charge of storing all of the data in its chain as well as the information flow between them. The consensus node key responsibilities are chain computation, packaging, and consensus. Ordinary nodes are used to carry services and do not participate in consensus and verification data. Each participating consensus node is assigned at random, and they will be re-selected as time goes on.

 

**THINKIUM IDENTITY AND AUTHENTICATION**

The Thinkium core engine offers users with an identity identification system that is ubiquitous, configurable, and secure. The Thinkium blockchain system's address account is not directly linked to the user's identity, but it does allow users to authenticate the account.

A verifiable claim can be used to verify an account's identity and other attributes.

The Thinkium core engine offers three types of declaration methods, enabling customers to pick the protocol that best meets their needs while balancing security, cost, and efficiency. The blockchain has an immutable character when it comes to establishing verifiable claims. As a reliable and traceable bulletin board, it's ideal.

 

**DEVELOPMENT TOOLS**

The Thinkium core engine design is a  unique development architecture concealing a multitude of obscure ideas and tools for users. It may be incorporated into a Thinkium desktop application, making it simple to get started for everyone. Simultaneously, it gives developers with a Decentralized application and the full-stack SDK necessary for development of smart contract allowing them to construct target apps more quickly. 

**THINKIUM DESKTOP**

The Thinkium core engine comes with a standard desktop application, the Thinkium desktop, that can retrieve, download, and run applications. The desktop version can run on both PCs and mobile terminals, allowing users to access the blockchain from a variety of devices. 

**DEVELOPMENT FRAMEWORK**

The development framework of the Thinkium core engine is quite friendly. It includes: Thinkium smart contract SDK used for for fast debugging and developing smart contracts, Thinkium application development SDK used for developing applications more quickly and can be published on D-store and operated on Thinkium Desktop.

**·    THINKIUM SMART CONTRACT SDK**

The Thinkium core engine will include a smart contract online IDE as well as a universal editor plug-in to help developers convert quickly. The Thinkium core engine will provide a compiler for the smart contract language T, which can turn T into a virtual machine language to cut learning costs and make contract developers more productive. The Thinkium smart contract SDK offers native development libraries in addition to the compiler. The native development library allows the smart contract to read native data from the Thinkium blockchain. 

 

**·    THINKIUM APPLICATION DEVELOPMENT SDK**

The Thinkium core engine provides an application development language and operating environment to allow users to access the Thinkium public blockchain in the simplest way possible. Application developers may create Thinkium decentralized apps using this collection of development SDKs in the same way they would develop a web application. The code is then put together and released to the D-store with the aid of the publishing tool in the SDK. This will allow users find and use new application through the Thinkium desktop.

 

**·    API**

The API is based on the blockchain's and smart contracts' main features. To enable remote call capabilities, it wraps the underlying interface, smart contracts, and D-Store back-end functionality inside a standard protocol based on HTTP. The Thinkium core engine wraps functions on the API layer's standard interface. Users can access the full capabilities of the blockchain through remote calls if they utilize the Thinkium-API.

 

**·    D-STORE BACKEND** 

The D-Store backend not only allows categorised indexing and searching of apps, but it can also leverage blockchain data to tally app use and create various rankings automatically. D-Store solves the dispersed phenomena of smart contracts on the existing public chain by employing a multi-dimensional organizing mechanism. This prevents resource waste caused by repetitive development. Simultaneously, more users are collected on the same contract, resulting in larger advantages for contract developers, which leads to higher-quality contract functionalities and boosting blockchain development.



Thinkium is bridging the physical business world and the digital world, the technological leader in the web 3.0.





Join our:

Official website: https://www.thinkium.net/

Github: https://github.com/ThinkiumGroup/wiki





 