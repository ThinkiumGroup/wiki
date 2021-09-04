## app.ini Configuration



```shell
[http]
port = ":8101"


[rpc]
;use rpcproxy.thinkium.org in production environment
rpc = "rpctest.thinkium.org"

[encrypt]
;key must 16, 24, 32 bit
;The encryption password of the private key is passed in api, and the businessId parameter in the interface is passed 1, which means that key1 is used
key1="yitawzdk3ueqarfq"
key2="azrtiabarda3ufgq"


[mysql]
; The results returned when hash checking transactions need to be reversed through the contract table of the library, and will be inserted into the contract table when the contract is released
; If you do not configure the database , the data will be saved in the embedded database sqlite
url = "username:password@tcp(ip:port)/dbName?charset=utf8&parseTime=true&loc=Local"
```



You need to replace the above five variables with your own configuration

**username**: account name with database read and write permissions

**password**: the password corresponding to useranme

**ip**: The ip of the machine where the database is located

**port**: mysql service port

**dbName**: database name

