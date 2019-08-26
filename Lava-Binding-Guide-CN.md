# Lava算力绑定机制指南

<br />

### 算力绑定的基本概念:

<br />

1.什么是算力绑定？

算力绑定是Lava特有的算力调配机制。

算力绑定允许用户将自身硬盘容量算力绑定到另一用户，使得双方出块Coinbase收益都转入被绑定放地址。

一个简单例子：Alice有挖矿地址（Address A）与1TB硬盘容量算力，Bob有挖矿地址（Address B）与300TB硬盘容量算力。

Alice可发起一笔绑定交易，将自身算力绑定到Bob身上。

挖矿时，如果Alice出块，该块会记录Alice的Plot ID（即认为是Alice出块），但Coinbase交易的收益地址是Bob的地址（Address B）；

如果Bob出块，该块会记录Bob的Plot ID（即认为是Bob出块），且Coinbase交易的收益地址仍是Bob的地址（Address B）。

<br />

2.算力绑定的意义

算力绑定的目的是，出块较少的小型算力单位（如本例中的Alice）可以通过绑定更大型的算力单位（如本例中的Bob），达到增强算力单位以平滑挖矿收益的目的。

<br />

3.收益分配问题

需要注意的是，绑定发起方与被绑定方需要约定收益的分配规则。

这一分配方式是私下达成的，没有客观标准。

例如，上例中，Alice可以要求无论双方实际出块多少，Alice都固定分得Bob的地址（Address B）中奖励总金额的1/300。

无论何种分配规则，只需绑定发起方与被绑定方达成约定即可。奖励分配的具体操作行为也完全由双方私下约定并实施，并非链上行为。

<br />


### 算力绑定相关命令:

<br />

1.发起绑定
```
.\lava-cli.exe -rpcuser=test -rpcpassword=test bindplotid "发起绑定地址" "接受绑定地址"
```
例如矿工甲（持有挖矿地址A）可以发起算力绑定到矿工乙（持有挖矿地址B）。绑定后，甲、乙都可正常挖矿。

当甲的Plot ID出块时，对应的Coinbase奖励会发到乙的地址B。

绑定成功后，程序会返回绑定交易的ID。

<br />

2.查询绑定情况
```
.\lava-cli.exe -rpcuser=test -rpcpassword=test listbindings 
```
查询后程序会展示全网目前的绑定关系。

例如：
```
[
  {
    "from": {
      "address": "nfmJmsGPgoJGPYsDj4Z5CfpWUQQHHD",
      "plotid": 41940084074803714
    },
    "to": {
      "address": "n2sGZMd2K38SS4yPwEL7NDTJ3pvST6G",
      "plotid": 862315404337908960
    }
]
```
from项表示发起绑定人的信息（包括地址与Plot ID）、to项表示接受绑定人的信息（Plot ID）。

<br />

3.解除已有的绑定关系
```
.\lava-cli.exe -rpcuser=test -rpcpassword=test unbindplotid "自己的地址"
```
执行此命令后，原有的绑定关系就解除了。

执行成功后，程序会返回解绑交易的交易ID。



