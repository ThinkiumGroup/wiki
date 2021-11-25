## 1. Config File config.yaml

**firstly, to create the config file  with the content below, name it*[config.yaml]***

```yaml
dataNodes:
  - {chainId: 60000, address: "192.168.1.11:23021"}
  - {chainId: 60001, address: "192.168.1.11:23026"}
  - {chainId: 60002, address: "192.168.1.12:23021"}
  - {chainId: 60103, address: "192.168.1.12:23026"}
```

dataNodes : which the proxy to connect, least one or more nodes required



## 2. Deployment-script file deploy.sh

***require docker installed***

```shell
# get version from input
version=$1
echo "version=${version}"

docker pull thinkium/rpcproxy:${version}

docker stop rpc-proxy
docker rm rpc-proxy

# notice
docker run -itd  -v your-config-file-location:/opt/rpc-proxy/config  -p 0.0.0.0:8080:8080 --name rpc-proxy thinkium/rpcproxy:${version}
```

you need replace *[your-config-file-location]* with your own directory which the file [*config.yaml*] located such as *[~/conf]*



## 3 Versions for different sdks

### 3.1 for java sdk, use *2.6.1* 

```shell
# to deploy
sh deploy.sh 2.6.1 
```

### 3.2 otherwise, for go、javascript and python, use *2.3.16*

```shell
# to deploy
sh deploy.sh 2.3.16
```



## 4 Use

After the container running successfully, you can use the service at default port 8080.

