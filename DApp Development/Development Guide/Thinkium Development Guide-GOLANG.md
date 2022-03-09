# Thinkium chain web3 development tutorial - GOLANG

### Target

 	1. Understand the basic operation process of the chain
 	2. Understand contracts and perform contract-related operations on the chain
 	3. Interact with the chain using golang

Note: 
	1.The testrpc in this article is https://test1.thinkiumrpc.net, also has other available test RPCs as follows https://test2.thinkiumrpc.net、https://test103.thinkiumrpc.net ,Readers can choose by themselves.
	2.The source code clone address of this article is https://github.com/ThinkiumGroup/web3go-demo.git

#### Basic Environment and Tools

1. The basic golang environment, I won't go into details here
2. Basic git environment
3. Basic abigen compilation environment
4. Basic solc compilation environment (installation on the Internet by yourself)
5. [Blockchain browser](https://browser.thinkiumdev.net/)
6. [Tap Link](https://www.thinkiumdev.net/DApp%20Development/Faucet.html)

#### Project construction

1. Clone the base project with git

2. configure abigen
   
   ```shell
   go get -u github.com/ethereum/go-ethereum
   cd $GOPATH/src/github.com/ethereum/go-ethereum/
   make
   make devtools
   ```
   
   Note: protoc needs to be installed in advance. The tools generated after make devtools are completed are in $GOPATH/bin/abigen, and the path is introduced into the system variable PATH to test the command
   
3. Initialize the project

4. Project Structure Analysis
   1. The RPC_URL in the const of eth in eth is the RPC address
   2. examples
      1. account contains test methods for creating wallets and main currency transfers
      2. chain contains the test method for querying the current block height
      3. contract
         1. Contains deploy and call contract test methods
         2. storage.go is the generated file (details can be viewed below)
   3. lib is the go file generated using bin and abi
   4. The bin and abi in the storage in resources use solc to compile the sol file, which is the source file for this test

#### test preparation

1. First prepare a Solidity source code file, this test file - Storage.sol in Storage in the project resource

2. Then use solc to compile the file to generate data (refer to the command: sudo solc --bin --abi Storage.sol), the results are as follows
    ```shell
       solc --bin  --abi Storage.sol
      ======= Storage.sol:Storage =======
      Binary:
      608060405234801561001057600080fd5b50610150806100206000396000f3fe608060405234801561001057600080fd5b50600436106100365760003560e01c80632e64cec11461003b5780636057361d14610059575b600080fd5b610043610075565b60405161005091906100a1565b60405180910390f35b610073600480360381019061006e91906100ed565b61007e565b005b60008054905090565b8060008190555050565b6000819050919050565b61009b81610088565b82525050565b60006020820190506100b66000830184610092565b92915050565b600080fd5b6100ca81610088565b81146100d557600080fd5b50565b6000813590506100e7816100c1565b92915050565b600060208284031215610103576101026100bc565b5b6000610111848285016100d8565b9150509291505056fea26469706673582212205fd13809e018341b527cfb6c32c0bb14338d2116c0487c547c4faea7f246e16464736f6c63430008090033
      Contract JSON ABI
      [{"inputs":[],"name":"retrieve","outputs":[{"internalType":"uint256","name":"","type":"uint256"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"uint256","name":"num","type":"uint256"}],"name":"store","outputs":[],"stateMutability":"nonpayable","type":"function"}]
    ```
   
   Below Binary is the bin of the contract, which is bytecode, and after ABI is the abi compiled by the contract.
   
3. After the result is obtained, the bytecode is stored in a file, and the abi is also stored in another file (note that it is an empty file), such as Storage.bin and Storage.abi in the project

4. Use abigen to compile the file to generate the go class file, the command is as follows
    ```shell
      sudo abigen --abi=Storage.abi --bin=Storage.bin --pkg=main --out=storage.go
    ```
   
6. At this point, the preparation work is complete, and then start the test

#### test process

1. First determine the Rpc address in the calling package

2. included in the project
   1. wallet creation
      1. ```go
         func TestAccount(t *testing.T) {
         	//get account
         	pv, err := crypto.GenerateKey()
         	if err != nil {
         		panic(err)
         	}
         	privateKey := hex.EncodeToString(crypto.FromECDSA(pv))
         	//c1f14e4132c1858b390ff169dd045082b9ba1ca022de641e7aa24b0322510499
         	fmt.Println("privateKey: ", privateKey)
         	// change to your rpc provider
         	web3, err := web3.NewWeb3(eth.RPC_URL)
         	if err != nil {
         		panic(err)
         	}
         	err = web3.Eth.SetAccount(privateKey)
         	if err != nil {
         		panic(err)
         	}
         	//get address
         	//0x901F21a0a09536F24feF8f5565eBcacB7aC5DE31
         	fmt.Println("address: ", web3.Eth.Address())
         }
         ```
         
      2. The result is as follows
      
         1. ```go
            API server listening at: [::]:41549
            === RUN   TestAccount
            privateKey:  50014d49478a00f62f775e015e389bd73dede68726a14d4f8b28253165bff23a
            address:  0x2aE433ae1C9e34BdD48296fB7BCFE8a6E60c7d38
            ```
      
      3. After the address is created go to [Tap Link](https://www.thinkiumdev.net/DApp%20Development/Faucet.html)take the test
      tkm
      
   2. Transfer function (main currency tkm transfer)
      1. ```go
         func TestSendTransaction(t *testing.T) {
         	// change to your rpc provider
         	web3, err := web3.NewWeb3(eth.RPC_URL)
         	if err != nil {
         		panic(err)
         	}
         	web3.Eth.SetAccount("c1f14e4132c1858b390ff169dd045082b9ba1ca022de641e7aa24b0322510499")
         	balance, err := web3.Eth.GetBalance(web3.Eth.Address(), nil)
         	if err != nil {
         		panic(err)
         	}
         	fmt.Println("balance: ", balance)
         	nonce, err := web3.Eth.GetNonce(web3.Eth.Address(), nil)
         	if err != nil {
         		panic(err)
         	}
         	fmt.Println("Latest nonce: ", nonce)
         	//transfer
         	//set chainId
         	web3.Eth.SetChainId(50001)
         	// transfer 1 tkm from 0x901F21a0a09536F24feF8f5565eBcacB7aC5DE31 to 0x90021a2CcA84a0611363ec1f9ccb36B4761DE08E
         	hash, err := web3.Eth.SendRawEIP1559Transaction(common.HexToAddress("0x90021a2CcA84a0611363ec1f9ccb36B4761DE08E"),
         		new(big.Int).SetInt64(1000000000000000000),300000,new(big.Int).SetInt64(300000),new(big.Int).SetInt64(300000),nil)
         	if err != nil {
         		panic(err)
         	}
         	fmt.Println("hash: ", hash)
         }
         ```
         
      2. The result is as follows:
         1. ```go
            API server listening at: [::]:38469
            === RUN   TestSendTransaction
            balance:  97315968400000000000
            Latest nonce:  24
            hash:  0x3c781964d927a2194897830cce8d89bdf2e20a9ff3ddd0fa3cda7b3f3f6adc39
            --- PASS: TestSendTransaction (0.05s)
            PASS
            ```
      
   3. deploy contract
      
      1. 
      
         ```go
          func TestDeployContract(t *testing.T)  {
         	// change to your rpc provider
         	web3, err := web3.NewWeb3(eth.RPC_URL)
         	if err != nil {
         		panic(err)
         	}
         	privateKey, err := crypto.HexToECDSA("c1f14e4132c1858b390ff169dd045082b9ba1ca022de641e7aa24b0322510499")
         	if err != nil {
         		panic(err)
         	}
         
         	publicKey := privateKey.Public()
         	publicKeyECDSA, ok := publicKey.(*ecdsa.PublicKey)
         	if !ok {
         		fmt.Println("error casting public key to ECDSA")
         	}
         
         	fromAddress := crypto.PubkeyToAddress(*publicKeyECDSA)
         	nonce, err := client.PendingNonceAt(context.Background(), fromAddress)
         	if err != nil {
         		panic(err)
         	}
         
         	gasPrice, err := client.SuggestGasPrice(context.Background())
         	if err != nil {
         		panic(err)
         	}
         	//set chainID
         	auth, err  := bind.NewKeyedTransactorWithChainID(privateKey,new(big.Int).SetInt64(50001))
         	if err != nil {
         		panic(err)
         	}
         	auth.Nonce = big.NewInt(int64(nonce))
         	auth.Value = big.NewInt(0)     // in wei
         	auth.GasLimit = uint64(300000) // in units
         	auth.GasPrice = gasPrice
         	address, tx, instance, err :=DeployMain(auth,client)
         	if err != nil {
         		panic(err)
         	}
         	fmt.Println("contract:"+address.Hex())
         	fmt.Println("deploy hash:"+tx.Hash().String())
         	_, _ = instance, tx
         }
         ```
      
      2. To get the contract address, subsequent operations need to use the contract address, test execution, and get the contract address as0x63C21800Fc7970D796811ac21d5ca42688382195，The result is as follows
         1. ```go
            API server listening at: [::]:38869
            === RUN   TestDeployContract
            contract:0x63C21800Fc7970D796811ac21d5ca42688382195
            deploy hash:0x59fe057a32e6650ae5134ae2d9a61d884d05f5f687828ea79d146f4fc747f6d8
            --- PASS: TestDeployContract (0.04s)
            PASS
            ```
      
   4. contract call
      1. ```go
         func TestCallContract(t *testing.T) {
         
         	// change to your rpc provider
         	web3, err := web3.NewWeb3(eth.RPC_URL)
         	if err != nil {
         		panic(err)
         	}
         	//load contract 0x771B03a85843907B89B66dbbCD90E1b8761a4fa3
         	main, err := NewMain(common.HexToAddress("0x797C88225547126879aA4EF444A66D627E402366"), client)
         	if err != nil {
         		panic(err)
         	}
         	num, err := main.Retrieve(nil)
         	if err != nil {
         		panic(err)
         	}
         	fmt.Printf("num:%d", num)
         	fmt.Println("")
         
         	//write contract
         	privateKey, err := crypto.HexToECDSA("c1f14e4132c1858b390ff169dd045082b9ba1ca022de641e7aa24b0322510499")
         	if err != nil {
         		panic(err)
         	}
         	publicKey := privateKey.Public()
         	publicKeyECDSA, ok := publicKey.(*ecdsa.PublicKey)
         	if !ok {
         		fmt.Println("error casting public key to ECDSA")
         	}
         
         	fromAddress := crypto.PubkeyToAddress(*publicKeyECDSA)
         	nonce, err := client.PendingNonceAt(context.Background(), fromAddress)
         	if err != nil {
         		panic(err)
         	}
         
         	gasPrice, err := client.SuggestGasPrice(context.Background())
         	if err != nil {
         		panic(err)
         	}
         	chainId,err := client.ChainID(context.Background())
         	//set chainID
         	auth, err := bind.NewKeyedTransactorWithChainID(privateKey, chainId)
         	if err != nil {
         		panic(err)
         	}
         	auth.Nonce = big.NewInt(int64(nonce))
         	auth.Value = big.NewInt(0)     // in wei
         	auth.GasLimit = uint64(300000) // in units
         	auth.GasPrice = gasPrice
         
         	main.Store(auth,new(big.Int).SetInt64(1000))
         
         }
         
         ```
         
      2. In the above method, we implemented 2 methods, namely read and write
         1. After NewMain, you can perform some operations on the contract
         
         2. Get the default variable value set by the contract main.Retrieve(nil) This is the read method
         
         3. main.Store(auth, new(big.Int).SetInt64(10)) resets the value in the contract, which is the writing method
         
         4. Note: In the middle sleep time, because the transaction needs to be confirmed, it is not possible to read directly after writing.
         
         5. The result is as follows
            1. ```go
               API server listening at: [::]:40991
               === RUN   TestCallContract
               num:100
               newNum:1000
               --- PASS: TestCallContract (5.06s)
               PASS
               ```
            
               
            
            2. It can be clearly seen that the default value is 100, and the query after writing is 1000



#### Summarize

The above is the simple process and method of using golang to interact with the thinkium chain. I hope you have a happy programming!

​		

​								