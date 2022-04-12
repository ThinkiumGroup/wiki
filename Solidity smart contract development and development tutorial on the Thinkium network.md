**Solidity smart contract development and development tutorial on the Thinkium Network.**

![](https://s3-us-west-2.amazonaws.com/t-chain-data/dev/1649765116307.jpeg)

- **What is a Smart Contract?**

The smart contract term was coined by Nick szabo in 1997. Smart contracts  are nothing but programs that exist on the blockchain. These "smart  contracts" can be used by making outside method calls or calls from  other smart contracts. These smart contracts execute in the EVM  (Ethereum virtual machine). Smart contracts can reduce malicious  exceptions, fraudulent losses, and a need for trusted intermediator,  when properly written and audited.

- **What is Solidity?**

As we saw that smart contracts are nothing but programs and you need a  programming language to write these programs. Ethereum core contributors invented a programming language called Solidity to write smart  contracts (aka computer programs that run on the blockchain). Solidity  is a high-level, object-oriented language inspired by JavaScript, C++,  and Python - it has syntax very similar to JavaScript. There are other  blockchains and Ethereum forks that support Solidity - such as Tron.  Solidity is not the only language you can use to write smart contracts  though. There are other languages that can be used to write smart  contracts, like Vyper, the most popular and adopted smart contract  language after solidity.

- **There are two ways of executing Solidity program which are :**

\1. Offline Mode 
\2. Online Mode

- **Offline Mode**

To operate a Solidity smart contract in Offline mode, you must install node.js, truffle and ganache on your machine.
I will not discus this method in this article since I will mainly focus on online mode.

- **Online Mode**

The beauty of Solidity is that it is come up with an online IDE — Remix  Ethereum IDE. You can create your smart contract with the help of this  online IDE ( Remix) . It also provides an offline installer to run it  locally without any internet.

- **What is Remix?**

We're going to use Remix to write all of the code in this tutorial. Remix is a browser-based IDE that allows you to write, compile, deploy smart  contracts! It has a lot of nice features like persistent file storage!  We'll use Remix so that we don't have to download any developer tools or install anything to get started. Head on over to Remix in a new tab in  order to follow along with this tutorial.

- **Check the infograph for a** 
  **Simple steps to follow**.

  ![](https://s3-us-west-2.amazonaws.com/t-chain-data/dev/1649764792796.jpeg)

**Step1:** Set up your metamask wallet
Network. 
Open your metamask extention on chrome, go to settings, go to Network,  choose add custom network and fill the space with the i formations below

![](https://s3-us-west-2.amazonaws.com/t-chain-data/dev/1649765223587.jpeg)

or check Thinkium github for the informations :https://github.com/ChaosverseGroup/wiki

**Step 2**: send your wallet address to Thinkium team to get test coins.

**Step 3:** a. Open Remix on your chrome browser https://remix.ethereum.org/

**b.** Choose a new file and create the name Contract for example. and will take you to empty environment for coding.

![](https://s3-us-west-2.amazonaws.com/t-chain-data/dev/1649765603402.jpeg)

**N/B** The may or not a pop up asking you to sign into your wallet, choose  your metamask wallet and authorize, and ensure to choose Thinkium  network. Then proceed to your remix environment.

**c.** Start coding. Copy the code below and paste.

![](https://s3-us-west-2.amazonaws.com/t-chain-data/dev/1649766134569.jpeg)

- **Let me explain**

**Line 1:** Specifying SPDX license type, whenever the source code of a smart  contract is made available to the public, these licenses can help  resolve/avoid copyright issues. If you do not wish to specify any  license type, you can use a special value UNLICENSED or simply skip the  whole comment (it won’t result in an error, just a warning).

**Line 3:** On the first line we are declaring which Solidity compiler we want to  use. For instance, we are targeting any version between ≥ 0.7.0 and  <0. 9.0

**Line 5-6:** We are declaring our contract here and naming it as Contract . It is  normal practice to use the same filename as the contract name. For  example - this contract will be saved in the file name Contract.sol  (.sol is the file extension for solidity smart contracts).

**Line 8-9:** constructor, A constructor is an optional function declared with the  constructor keyword which is executed only upon contract creation.  Constructor functions can be either public or internal. If there is no  constructor, the contract will assume the default constructor.
The constructor takes a string parameter and assigns its value to the global variable name.

**Line 12-13:**The name can be changed using the function
changeName(string) which acts as a setter, while

**Line 15-16:** getName() acts as a getter.

**Step 4:**Compiling your smart contract: click on the second icon on the left

![](https://s3-us-west-2.amazonaws.com/t-chain-data/dev/1649766134569.jpeg)

and click on compile

![](https://s3-us-west-2.amazonaws.com/t-chain-data/dev/1649766568730.jpeg)

**Step 5:** Deploy your smart contracts on Thinkium chain: click on the third icon on the left,

![](https://s3-us-west-2.amazonaws.com/t-chain-data/dev/1649766701673.jpeg)

![](https://s3-us-west-2.amazonaws.com/t-chain-data/dev/1649766784385.jpeg)

on the environment section, choose injected Web3

A pop up where you need to authorize it in your metamask so your wallet address will appear on the account section.

**b.** Click on deploy

![](https://s3-us-west-2.amazonaws.com/t-chain-data/dev/1649766873672.jpeg)

and confirm the transaction in your metamask and then your contract will be displayed on the deployed contract section.

![](https://s3-us-west-2.amazonaws.com/t-chain-data/dev/1649766975712.jpeg)

**For more information contact**

**Official website :**thinkium.net

**Nigerian local community:** https://t.me/ThinkiumNig