# Thinkium chain web3 development tutorial - JAVA

### Target

 	1. Understand the basic operation process of the chain
 	2. Understand contracts and perform contract-related operations on the chain
 	3. Interact with the chain using java

Note:

1. The test rpc in this article is https://test1.thinkiumrpc.net, and other available test rpcs are https://test2.thinkiumrpc.net, https://test103.thinkiumrpc.net, readers can choose by themselves
2. The source code clone address of this article is https://github.com/ThinkiumGroup/web3j-demo.git

#### Basic Environment and Tools

1. Basic java environment, not repeated here (java, maven)
2. Basic git environment
3. Basic web3j compilation environment (installed online by yourself)
4. Basic solc compilation environment (installed online by yourself)
5. [blockchain browser](https://browser.thinkiumdev.net/)
6. [Tap Link](https://www.thinkiumdev.net/DApp%20Development/Faucet.html)

#### Project construction

1. Clone the base project with git
2. configure maven
3. Initialize the project
4. Project Structure Analysis
   1. com.web3j is the core of the project
      1. demo is the whole test demo
      2. generate is the java source file compiled using web3j
      3. The Rpc environment is configured in the util
   2. In resources, bin and abi use solc to compile sol files

#### test preparation

1. First prepare a Solidity source code file, this test file - Storage.sol in the project resource

2. Then use solc to compile the file to generate data (refer to the command: sudo solc --bin --abi Storage.sol), the results are as follows
   
   ```shell
   sudo solc --bin  --abi Storage.sol
   ======= Storage.sol:Storage =======
   Binary:
   608060405234801561001057600080fd5b50610150806100206000396000f3fe608060405234801561001057600080fd5b50600436106100365760003560e01c80632e64cec11461003b5780636057361d14610059575b600080fd5b610043610075565b60405161005091906100a1565b60405180910390f35b610073600480360381019061006e91906100ed565b61007e565b005b60008054905090565b8060008190555050565b6000819050919050565b61009b81610088565b82525050565b60006020820190506100b66000830184610092565b92915050565b600080fd5b6100ca81610088565b81146100d557600080fd5b50565b6000813590506100e7816100c1565b92915050565b600060208284031215610103576101026100bc565b5b6000610111848285016100d8565b9150509291505056fea26469706673582212205fd13809e018341b527cfb6c32c0bb14338d2116c0487c547c4faea7f246e16464736f6c63430008090033
   Contract JSON ABI
   [{"inputs":[],"name":"retrieve","outputs":[{"internalType":"uint256","name":"","type":"uint256"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"uint256","name":"num","type":"uint256"}],"name":"store","outputs":[],"stateMutability":"nonpayable","type":"function"}]
   ```
   
   Below Binary is the bin of the contract, which is bytecode, and the ABI is followed by the abi compiled by the contract.
   
3. After the result is obtained, the bytecode is stored in a file, and the abi is also stored in another file (note that it is an empty file), such as Storage.bin and Storage.abi in the project

4. Use web3j to compile the file to generate a java class file, the command is as follows

   1. ```shell
      web3j generate solidity -b file location containing bin -a file location containing abi -o generate java file to location -p which package to generate java file
      E.g:web3j  generate solidity   -b /Users/muzi/Desktop/StoBin.bin -a /Users/muzi/Desktop/Storage.abi -o /Users/muzi/IdeaProjects/web3j-sample/main/java -p com.muzi.muxin.wrapper
      ```

5. Then move the java file to the generate of the project

6. At this point, the preparation work is complete, and then start the test

#### test process

1. First determine the Rpc address in the util package
2. included in the project
   1. wallet creation
      1. ```java
         public static void createWallet(String password) throws InvalidAlgorithmParameterException, NoSuchAlgorithmException, NoSuchProviderException, CipherException, JsonProcessingException {
                 WalletFile walletFile;
                 ECKeyPair ecKeyPair = Keys.createEcKeyPair();
                 walletFile = Wallet.createStandard(password, ecKeyPair);
                 System.out.println("address " + walletFile.getAddress());
                 ObjectMapper objectMapper = ObjectMapperFactory.getObjectMapper();
                 String jsonStr = objectMapper.writeValueAsString(walletFile);
                 decryptWallet(jsonStr, password);
             }
         ```
      
         
      
      2. ```java
         address 0x4Da8e87539E3c988D6e2431510C8fccBcaf83855
         privateKey 95dda4681ed7b9e0eab5e21c07e495a3fdc9975e51e0a8ee7344c55cb45782cf
         ```
      
         
      
      3. After the address is created go to[Tap Link](https://www.thinkiumdev.net/DApp%20Development/Faucet.html)get the test tkm
   2. Transfer function (main currency tkm transfer)
      1. ```java
         public static void sendIP1559Transaction() throws Exception {
                 //Which wallet account address to transfer to
                 String toAddress = "0xAc1656e2c41711053c6Ad151bcF4A395A24C1Ee1";
         
                 //Get a certificate
                 Credentials credentials = getCredentials("", "", privateKey);
         
                 /**
                  * Create and send transfer transactions
                  */
                 TransactionReceipt transactionReceipt = Transfer.sendFundsEIP1559(
                         web3j,
                         credentials,
                         toAddress, //toAddress
                         BigDecimal.ONE.valueOf(1), //transfer value
                         Convert.Unit.ETHER, //transfer unit
                         BigInteger.valueOf(300000), // gasLimit
                         DefaultGasProvider.GAS_LIMIT, //maxPriorityFeePerGas (max fee per gas transaction willing to give to miners)
                         BigInteger.valueOf(3_100_000_000L) //maxFeePerGas (max fee transaction willing to pay)
                 ).send();
                 System.out.println("get transaction status-------------------->>>:"+transactionReceipt.isStatusOK());
             }
         ```
      
         
      
      2. The result is as follows:
         1. ```java
            get transaction status-------------------->>>:true
            ```
         
         2. true 就是success  false 就是fail
   3. contract deploy
      1. 
      
         ```java
          public static void deployContract() throws Exception {
                 /**
                  * Create a certificate
                  */
                 Credentials credentials = getCredentials("", "", privateKey);
                 /**
                  * get chain id
                  */
                 String chainId = getChainId();
                 /**
                  * Build Transaction Manager
                  */
                 TransactionManager transactionManager = new RawTransactionManager(
                         web3j, credentials, Long.parseLong(chainId));
         
                 /**
                  * Default gasPrice and gasLimit
                  */
                 ContractGasProvider contractGasProvider = new DefaultGasProvider();
                 /**
                  * Deploying the contract Note: The Storage class is the abi file and bin file generated after sol compilation, and the contract java class generated by Command Line Tools
                  */
         
                 Storage contract = Storage.deploy(web3j, transactionManager, contractGasProvider).send();
                 System.out.println("contractAddress------->>>>>:" + contract.getContractAddress());
         
             }
         
         ```
      
      2. To get the contract address, subsequent operations need to use the contract address, test execution, and get the contract address as0xca7630e0df9b5cfed112da7587c3aa8177690641，The result is as follows
         1. ```java
            contractAddress------->>>>>:0xca7630e0df9b5cfed112da7587c3aa8177690641
            ```
         
      
   4. contract call
      1. ```java
         public static void loadContract(String contractAddress) throws Exception {
                 /**
                  * Create a certificate
                  */
                 Credentials credentials = getCredentials("", "", privateKey);
                 String chainId = getChainId();
                 /**
                  * Build Transaction Manager
                  */
                 TransactionManager transactionManager = new RawTransactionManager(
                         web3j, credentials, Long.parseLong(chainId));
                 /**
                  * Default gasPrice and gasLimit
                  */
                 ContractGasProvider contractGasProvider = new DefaultGasProvider();
                 //load contract
                 Storage contract = Storage.load(contractAddress, web3j, transactionManager, contractGasProvider);
                 if (contract.isValid()) {
                     /**
                      * Get the default variable value set by the contract
                      */
                     BigInteger retrive = contract.retrieve().send();
                     System.out.println("retrieve------->>>>>:" + retrive.toString());
                     /**
                      * Modify the default variable value set by the contract
                      * Note: There will be a delay after this method is called, and the value just set cannot be obtained immediately
                      */
                     TransactionReceipt send = contract.store(new BigInteger("999")).send();
         
                     Thread.sleep(8000);
         
                     BigInteger retrivetSecond = contract.retrieve().send();
                     System.out.println("retrieve second------->>>>>:" + retrivetSecond.toString());
                 }
             }
         ```
      
      2. In the above method, we implemented 2 methods, namely read and write
         1. After loadContract, you can perform some operations on the contract
         2. Get the default variable value set by the contract contract.retrieve() This is the read method
         3. contract.store resets the value in the contract, which is the writing method
         4. Note: In the middle sleep time, because the transaction needs to be confirmed, it is not possible to read directly after writing.
         5. The test results are as follows
            1. ```java
               retrieve------->>>>>:1000
               retrieve second------->>>>>:999
               ```
            
               
            
            2. It can be clearly seen that the default value is 1000, and the query after writing is 999



#### Summarize

​	The above is the simple process and method of using java to interact with the thinkium chain. I hope you have a happy programming!

​		

​								