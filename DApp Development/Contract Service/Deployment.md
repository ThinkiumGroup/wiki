## Test Contract Service address

For testing environment only! For testing only!

Service address: **contract-test.thinkium.org**

rpc address: **test.thinkiumrpc.net**

AES encryption password: **key1="yitawzdk3ueqarfq" ;key2="azrtiabarda3ufgq"**

(Encryption password is used to symmetrically encrypt and sign the private key, and then pass it to the Contract Service to resist the risk of private key leakage)





## Self-Deploy Contract Service

Developers deploy **Contract Service** on their own servers, so that developers' own Dapp servers can directly access the **Contract Service** built by themselves in the local area network. Thus, the purpose of safe transmission and high performance is achieved.

1. The purpose of configuring the mysql database is that all smart contracts sent to the chain through the Contract Service will register an abi file in the database, so that all transactions related to this contract can be checked through the Hash transaction interface, and the specific content of the transaction parameters can be seen in this way.
2. It is not necessary to configure MySql, the Contract Service will automatically create an embedded **sqlite database**



### 1. Mysql configuration file app.ini

#### mysql configuration

```mysql
[mysql]

url="username:password@tcp(ip:port)/dbName?charset=utf8&parseTime=true&loc=Local"
```

You need to replace the above five bold marked variables with your own configuration

**username**: account name with database read and write permissions

**password**: the password corresponding to useranme

**ip**: The ip of the machine where the database is located

**port**: mysql service port

**dbName**: database name

 

#### Create database and contract table, sql:

```sql
CREATE TABLE `contract` (
 `id` int(11) unsigned NOT NULL AUTO_INCREMENT,
 `url` varchar(500) NOT NULL DEFAULT '',
 `chain_id` varchar(10) NOT NULL,
 `owner_address` varchar(128) NOT NULL DEFAULT '' COMMENT 'contract publiser address',
 `contract_name` varchar(50) NOT NULL DEFAULT '' COMMENT 'contract name',
 `contract_address` varchar(128) NOT NULL DEFAULT '' COMMENT 'contract address',
 `hash` varchar(128) NOT NULL DEFAULT '' COMMENT 'hash',
 `tx_info` longtext NOT NULL COMMENT 'transaction',
 `status` int(11) NOT NULL DEFAULT '0' COMMENT '1 success 2 failure',
 `contract_json` text NOT NULL COMMENT 'contract abi json',
 `create_time` datetime NOT NULL DEFAULT '',
 `update_time` datetime NOT NULL DEFAULT '',
 PRIMARY KEY (`id`) USING BTREE,
 UNIQUE KEY `unique_contract_address` (`chain_id`,`contract_address`)
) ENGINE=InnoDB  DEFAULT CHARSET=utf8 ROW_FORMAT=DYNAMIC COMMENT='contract';
```

 

### 2. Start

1. Pull docker image from hub.docker.com:

```shell
sudo docker pull thinkium/contract:xxxxx
```

2. After creating the database, enter this command to start the service

```shell
sudo docker run -i -t \
-v ~/conf:/root/conf \
-v ~/solc/solc-linux-amd64-v0.4.15+commit.8b45bddb:/usr/local/bin/solc \
-v ~/sqlite:/root/sqlite\
-v ~/contracts:/root/contracts\
-p 8101:8101 \
--restart=always \
-d --name=contract \
thinkium/contract:xxxxx
```

Replace xxxxx with the corresponding latest version number



Command analysis:

~/conf: Configure the app.ini file path at the host.

~/solc/solc-linux-amd64-v0.8.7+commit.8b45bddb: mount a specific version of the solc compiler, note that **you need to grant its executable permission**, if you do not mount the mirror, the default version is 0.5.

~/sqlite: sqlite database directory.
~/contracts: Store the compiled contracts.

 

solc compiler download address:

https://github.com/ethereum/solc-bin/tree/gh-pages/linux-amd64



After modifying the host's app.ini configuration file, restart the container to take effect.

```shell
docker restart contract
```



### 3. Check

Command in console.

```shell
docker  logs  --tail 200 -f contract 
```

We can see this in console.

```shell
[GIN-debug] Listening and serving HTTP on :8101
```

Success

 