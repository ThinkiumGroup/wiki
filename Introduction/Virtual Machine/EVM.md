#### EVM Virtual Machine

The thinkium public chain is fully compatible with Ethereum EVM virtual machine. Any contract edited by Ethereum EVM can run on the thinkium public chain. The following introduction is quoted from Ethereum EVM

#### Introduction to Ethereum virtual machine EVM

#### EVM description

EVM is executed as a stack machine with 1024 item depths. Each item is a 256 bit word, which is selected to facilitate the use of 256 bit Cryptography (such as keccak-256 hash or secp256k1 signature).

During execution, EVM maintains a transient * memory * (as a word addressed byte array) that does not persist between transactions.

However, the contract does contain a Merkle Patricia * storage * tree (as a word addressable word array) associated with the relevant account and part of the global state.

Compile the smart contract bytecode and execute the opcode as the digital EVM, such as standard stack operations ` XOR `, ` and `, ` add `, ` sub `, etc. The EVM also implements many specific blockchain stack operations, such as' address', 'balance', 'keccak256', 'blockhash', etc.

[![ Chart showing where gas is required for EVM operation]（ https://ethereum.org/static/9628ab90bfd02f64cf873446cbdc6c70/302a4/gas.png )

#### From ledger to state machine

The analogy of "distributed ledger" is usually used to describe blockchains such as bitcoin, which uses basic cryptographic tools to realize a decentralized currency. Cryptocurrency behaves like "normal" currency because the rules specify what can and cannot be done to modify the ledger. For example, a bitcoin address cannot spend more bitcoins than it previously received. These rules support all transactions on bitcoin and many other blockchains.

Although Ethereum has its own native cryptocurrency (ether), which follows almost exactly the same intuitive rules, it also supports a more powerful function: smart contract. For this more complex feature, a more complex analogy is needed. Ethereum is not a distributed ledger, but a distributed state machine. Ethereum's state is a big data structure, which not only contains all accounts and balances, but also a * machine state *, which can change between blocks according to a set of predefined rules, and can execute any machine code. EVM defines specific rules for changing state from block to block.

![ Show EVM composition chart]（ https://ethereum.org/static/e8aca8381c7b3b40c44bf8882d4ab930/302a4/evm.png )

#### Ethereum state transition function

EVM behaves like a mathematical function: given an input, it produces a deterministic output. Therefore, it is very helpful to more formally describe Ethereum as having * * state transition function * *:

```

1Y(S, T)= S'

two

```

Given an old valid state ` (s) ` and a new set of valid transactions ` (T) ` the Ethereum state transition function ` y (s, t) ` generates a new valid output state ` s'`

#### Status

In the context of Ethereum, the state is a huge data structure, called the modified Merkle Patricia trie. It keeps all accounts linked by hash and can be simplified to a single root hash stored on the blockchain.

#### Trade

The transaction is an encrypted signature instruction from the account. There are two types of transactions: transactions that result in message invocation and transactions that result in contract creation.

Contract creation will result in the creation of a new contract account containing the compiled smart contract bytecode. Whenever another account makes a message call to the contract, it executes its bytecode.