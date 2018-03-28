
## 外部账户VS合约账户
账户是以太坊的一个核心概念，以太坊的所有交易都依赖于账户而展开，所谓交易即一个带有签名的数据包从一个账户发送至另一个账户的过程，没有了账户的概念，交易也无从成立。狭义上的账户，典型的例子就是我们平时所接触的银行账户，拥有账号、密码、以及余额，可以转账、收款，作为个人财产信息的载体。广义上的账户则是根据业务和场景不同各有特点，不可同日而语。以太坊系统中拥有两种账户概念，即外部账户（externally owned accounts,EOAs ）和合约账户（contract accounts）。

#### 外部账户
一个外部账户由一对公私钥对唯一标示，密钥文件存储于数据目录（datadir指向或默认目录）下，对应的目录为keystore，私钥文件都经过加密之后存储于此目录下。密钥文件为JSON格式的文本文件，可以使用文本编辑器打开查看，格式如下：

```
{
	"address": "8536dbbefa49f3c25258ad06a4bc124948327e7b",
	"crypto": {
		"cipher": "aes-128-ctr",
		"ciphertext": "7fb0f0ea54dcd7f8e902c2ee34d4c1c6abb508f1bd06c887f1c8980f6acad739",
		"cipherparams": {
			"iv": "44ae1e13af53b849535a583d7a96bf6b"
		},
		"kdf": "scrypt",
		"kdfparams": {
			"dklen": 32,
			"n": 262144,
			"p": 1,
			"r": 8,
			"salt": "ca1fce58ee8d2254cbed4a68c43ba4dd96537f7d04ae98880692e4553417473f"
		},
		"mac": "3b4a85b3b4c0e65e0996c6f4a642d417d7d184d9b6f7240d4afe9bb9d25af6a9"
	},
	"id": "c0916ec8-8584-47ef-b478-8073afeda94b",
	"version": 3
}
```
keystore里面包含了此秘钥对应的地址和加密相关的一些信息，包括账户地址address、加密算法cipher、加密后的明文ciphertext等，客户端读取密钥文件和加密密码，对私钥进行解密，然后使用私钥对发送的交易进行签名。    

外部账户特征如下：  

* 有一个账户余额  
* 由私钥控制    
* 能发送交易(转账和收款)   
* 没有相关联的代码

#### 合约账户   
合约账户是一个由代码控制的账户，账户地址在智能合约被创建时生成，合约账户的交易不由某个私钥控制，而是通过交易或者其他智能合约的调用来触发合约代码，从而产生相关交易。    

合约账户的相关特征如下：    
* 有一个账户余额    
* 能产生交易    
* 有关联的合约代码  
* 通过交易或者其他合约调用来触发合约代码执行    

#### 创建外部账户
创建外部账户方式很多，通过各种以太坊客户端都能很简单创建，这里通过geth的console方式演示创建账户：
###### 查看账户列表 
     
    > eth.accounts  
    > ["0xb9d815e091fbc7c4d2af7b87c82a22860cb8f517", "0xf33819afbfbec0ff2287b0ee541a421d56e89646"]
以上是我搭建的私链上的两个账户地址

###### 新增账户

    > personal.newAccount("123456")
    "0x8536dbbefa49f3c25258ad06a4bc124948327e7b"
    > 
新增账户命令为  personal.newAccount("password")，以上我创建了一个新的账户，密码是123456。  
再次查看账户列表，就会发现多了一个账户

    > eth.accounts  
    ["0xb9d815e091fbc7c4d2af7b87c82a22860cb8f517", "0xf33819afbfbec0ff2287b0ee541a421d56e89646", "0x8536dbbefa49f3c25258ad06a4bc124948327e7b"]
    > 

###### 查看账户余额

    > eth.getBalance("0xb9d815e091fbc7c4d2af7b87c82a22860cb8f517")
    4.4293008390556e+22
    > eth.getBalance("0xf33819afbfbec0ff2287b0ee541a421d56e89646")
    1991609444000000000
    > eth.getBalance("0x8536dbbefa49f3c25258ad06a4bc124948327e7b")
    0
    > 
查看账户余额命令为：eth.getBalance("账户地址")，以上分别查看了当前三个账户的余额，前两个账户都拥有大量余额，最后一个账户是刚新建的，因此余额为0.


#### 创建合约账户
合约账户在智能合约部署时生成，因此创建合约账户需要部署一个智能合约，以下简单演示通过一个简单的智能合约部署来尝试创建智能合约账户    
合约只有一个get和set方法，代码如下：

```
pragma solidity ^0.4.0;
contract SimpleStorage {
    uint storeddata; // 数据
    
    function set(uint x) public{
        storeddata = x;
    }
    function get() public constant returns(uint retVal)  {
        return storeddata;
    }
}
```

通过本地Remix，连接本地私链创建智能合约，使用上述账户列表中第一个账户创建合约，如下图所示：    
![image](http://oali3a9nv.bkt.clouddn.com/images/2018/03/29/1521521987733.jpg)


点击create，部署合约，合约部署后便会生成合约地址，如图：    
![image](http://oali3a9nv.bkt.clouddn.com/images/2018/03/29/1531521988096.jpg)

上图地址中间部分被隐藏来，复制下来如下：

    "0x9820895330aaa75e1e067f859bad88343a5fcf20"


#### 后记
准备得匆忙，以上简单介绍来以下外部账户和合约账户的概念，还有很多东西值得深究，后续有安排解读源码的时候还可以从以太坊源码剖析账户概念。上述创建账户相关的演示可作为大致了解，具体的步骤没有详细说明，geth的命令、本地私链搭建、搭建本地Remix等都可以安排任务细化成教程，往后续有相关任务安排。
