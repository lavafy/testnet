# Lava火石机制指南

### 火石的基本概念:

1.火石

火石`Firestone`是Lava的贡献证明与权益证明。

火石是一种在链上动态生成、动态消耗的特殊凭证。

2.获得火石

目前阶段，用户可以通过向系统抵押LV获得火石。

获得火石的行为可通俗地理解为“使用LV购买火石”，但需注意这只是通俗的理解，并不是真正的“购买”行为。

用户实际上是通过发起一笔特殊的链上交易，向系统抵押一定数量的LV，得到对应的火石。

3.火石的“价格”

在发起“购买”火石的交易时，系统会定义一个“价格”，表示“抵押多少LV可以获得一个火石”。

火石的价格是由系统动态调整的。

4.火石周期（Slot）

Lava区块链根据固定块高划分周期，称为火石周期`Slot`。

在主网中，每2048个块高构成一个火石周期。

用户需要在第N-1周期购买可在第N周期生效可使用的火石，该火石在第N+1周期过期（如果没有被使用的话）。

如果用户在火石生效的周期内成功出块，就可以消耗一个火石，该块即双倍产出块奖励。

例如在第一个减半周期内，正常产出320LV每块，如果在消耗火石的情况下，即可产出640LV每块。

5.火石的过期和释放问题

在第N-1周期购买的火石，在该周期内是不可使用的状态；

到第N周期生效可使用；

如果用户恰好在第N周期内出块，系统可消耗火石（一个块对应消耗一个火石），如果火石被消耗，抵押的LV会自动释放；

如果用户在第N周期内没有出块，火石会在第N+1周期过期，用户需要手动释放过期未使用火石抵押的资金。

6.火石的价格调整问题

每个火石周期（Slot）都会由系统自动调整火石价格。

如果上一周期火石存量（即该周期内全网实际购买生成的火石数量）超过目标值2048，则本周期火石价格上调5%；

如果上一周期火石存量（即该周期内全网实际购买生成的火石数量）低于目标值2048，则本周期火石价格下降5%；

火石价格调整机制的目的是促进达到火石供需的动态平衡。


### 火石相关命令:

1.向系统抵押LV获得火石（即购买火石）：
```
.\lava-cli.exe -testnet=1 -rpcuser=test -rpcpassword=test buyfirestone "购买火石的地址"
```
成功执行返回交易ID。

需要注意，火石是关联到地址的。例如，您通过该命令给地址A购买了火石，未来只有地址A的私钥能够使用火石以及释放火石。

一般情况下，给挖矿地址购买火石即可，这样当您的挖矿地址出块时，火石也会被自动使用以获得双倍Coinbase收益。

2.查询当前周期（Slot）信息：
```
.\lava-cli.exe -testnet=1 -rpcuser=test -rpcpassword=test getslotinfo
```
返回结果如下：
```
{
  "index": 5,
  "price": 16716105000,
  "count": 10,
  "locktime": 767
}
```
说明：

index表示现在处于第几个周期（Slot），周期从0开始计，在测试网中每128块高构成一个周期。

ticketprice表示当前火石的价格，需要注意该价格是以satoshi为单位，除以100000000得到以LV计的价格。

ticketcount表示当前全网已经购买的火石数量。

locktime表示在当前周期购买火石的成熟块高，达到这个块高以后才可以使用现在购买的火石。

3.查询地址持有火石情况：
```
.\lava-cli.exe -testnet=1 -rpcuser=test -rpcpassword=test getfirestone “你要查询的地址”
```
返回结果如下：
```
[
  {
    "outpoint": "615fb809eb973667ea8523ecf11bf93eafdf7924521bc172abb09329d141a3e8:1",
    "address": "n4CpQvwua2NXnoq7rJbp41JzbcvUGDL1f1",
    "lockheight": 511,
    "state": "IMMATURATE",
    "isSpent": false
  }
]
```
说明：

outpoint表示购买火石的交易ID，即当时购买该火石所发起的交易记录。

address表示火石所关联的地址。

lockheight表示该火石在这个块高以后为可用状态。

state表示火石的状态，IMMATURATE表示还未成熟（请等待下一个周期成熟），USABLE表示现在可用，OVERDUE表示已经过期。

isSpent表示火石是否被使用。false表示未被使用。

4.释放过期的火石

如果火石在出块的时候消耗掉了，就不需要手动释放；如果没有被消耗掉，需要在过期后手动释放。
```
.\lava-cli.exe -testnet=1 -rpcuser=test -rpcpassword=test freefirestone "持有火石的地址" "接受释放资金的地址"
```
成功释放后返回交易ID。

如果您希望抵押的资金释放回原先持有火石的地址，两个地址填一样的即可。


绑定算力相关命令：

1.发起绑定
```
.\lava-cli.exe -testnet=1 -rpcuser=test -rpcpassword=test bindplotid "发起绑定地址" "接受绑定地址"
```
例如矿工甲（持有挖矿地址A）可以发起算力绑定到矿工乙（持有挖矿地址B）。绑定后，甲、乙都可正常挖矿。当甲的Plot ID出块时，对应的Coinbase奖励会发到乙的地址B。

绑定成功后，程序会返回绑定交易的ID。

2.查询绑定情况
```
.\lava-cli.exe -testnet=1 -rpcuser=test -rpcpassword=test listbindings 
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

3.解除绑定
```
.\lava-cli.exe -testnet=1 -rpcuser=test -rpcpassword=test unbindplotid "自己的地址"
```
执行此命令后，原有的绑定关系就解除了。

执行成功后，程序会返回解绑交易的交易ID。
