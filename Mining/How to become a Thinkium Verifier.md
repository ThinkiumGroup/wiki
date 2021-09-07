### How to become a Thinkium verifier

To become a Thinkium verifier and participate in Thinkium mining, you need to complete the following steps

**1、Prepare AWS account**

You need to prepare:

1. An email account. This email address will be used as the AWS account name

2. A mobile phone number or fixed line number (which can be a domestic mobile phone number)

3. A credit card that can pay US dollars can be visa, MasterCard and other credit cards.

Registration website:

https://portal.aws.amazon.com/billing/signup?redirect_url=https%3A%2F%2Faws.amazon.com%2Fregistration-confirmation&language=zh_cn#/start

Register the account number according to relevant requirements

**2、Configuring Amazon VPC**

1) Create VPC

2) Create subnet

3) Create Internet Gateway

4) Add fixed label peerd to VPC, Internet gateway and routing table respectively_ eligible true

5) Create IAM role

6) Submit the work order and increase the number of VPCs and routes to 150+

**3、Server configuration**

Configuration requirements:

Consensus node requirements: CPU 2C, memory 4G ,  SSD 100G

1) Purchase reserved instance
2) Start the instance and select the thinkium-arm64 image
3) Start instance
4) Submit the work order and increase the number of servers to 50

**4、Start Node**

1. Log in to the server using software such as SecureCRT

2. Enter the configuration folder 

   cd thinkium/conf/ 

3. Obtain the private key of the random node and put it into the configuration file genkey (if you need to modify, please use vi dvpp0.yaml to enter the configuration file for modification)

4. Start node 

   docker run -itd -e CONFNAME=dvpp0.yaml --network host --name thinkium  -v /home/ubuntu/thinkium/data:/home/ubuntu/thinkium/data  -v /home/ubuntu/thinkium/conf:/srv/chain/config -v /home/ubuntu/thinkium/log:/home/ubuntu/thinkium/log thinkium/go-thinkium:latest

5. Configure node information and complete voting information in Tuke