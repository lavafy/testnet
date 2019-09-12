# A Guide for Lava Firestone

<br />

## A Brief Introduction of Lava Firestone

<br />

### 1. Definition

`Firestone` is a special built-in credential which is dynamically and consistantly created, consumed, or expired on-chain. 

`Firestone` is

1) a semi-token like on-chain credential based on the "Virtual Layering" concept;

2) a representative of contribution to Lava's ecology;

3) a representative of governance rights to Lava's ecology;

4) a representative of specific economic rights to Lava's ecology;

5) a representative of occupying resources from the system;

6) a carrier of voting rights in the on-chain governance mechanism;

7) a credential that is non-permanent, customizable and non-fungible.

In different stages of Lava Roadmap, Firestone will play different roles and support Layer 2 applications.

<br />

### 2. Get a Firestone

In the current stage, Firestone can be acquired by staking LV to the system.

Simply put, any user can "buy" Firestone with his/her LV. Notice that it is not a real "purchase" behavior, but we would rather call it "buy" because we want to express the whole concept more familiar and understandable to all.  

Technically, the process of "buying a Firestone" is realized by creating an on-chain transaction which "stakes" a certain quantity of LV to the system.

<br />

### 3. the "Price" 

There is a certain staking ratio (Firestone `Price`) indicating that how many LV you need to stake to the system to get a Firestone.

The `Price` is dynamically adjusted according to an special adjustment algorithm, which is defined in the consensus level.

<br />

### 4. the "Slot"

A `Slot` is a period of time, whose length is defined by `Height` on the blockchain.

In this way, the Lava Blockchain is divided by every 2048 blocks, and each divided result is called a `Slot`.

For example, blocks from #0~#2047 constitute `Slot` #0, blocks from #2048~#4095 constitute `Slot` #1, and so on.

The `Firestone` obtained by the user in the N-1th `Slot` is valid only in the Nth (next) `Slot`. When the Nth `Slot` is over, the `Firestone` is automatically abolished (expired), and the frozen funds will be returned.

If a miner mines a block and he has a valid `Firestone`, he is allowed to consume a `Firestone` to get additional coinbase reward from this block, which is twice of the fundamental coinbase reward.

For example, a new mined block produce 1) 320 LV coinbase reward without `Firestone` consumed; 2) 640 LV coinbase reward with a `Firestone` consumed.

<br />

### 5. Firestone expiration:

As described above, the `Firestone` obtained by the miner in the N-1th `Slot` is valid only in the Nth (next) `Slot`.

If a `Firestone` is consumed in Nth `Slot` (of course the miner need to mine a block as a prerequisite), the corresponding fund (in terms of LV) that is staked in this `Firestone` will be released immediately.

If a `Firestone` is unable to be consumed in Nth `Slot` (say, if the miner is not lucky enough to mine a block), the `Firestone` will be expired automatically in N+1th `Slot`, and whose fund staked needs to be freed manually via a special transaction.

<br />

### 6. Firestone Price Adjustment Algorithm

The `Price` will be adjusted dynamically at the beginning of every new `Slot` coming. 

There is a `target quantity` for `Firestone` in each `Slot`, which is set to `2048` in the Lava Mainnet.

如果上一周期火石存量（即该周期内全网实际购买生成的火石数量）超过目标值2048，则本周期火石价格上调5%；
If the actual quantity of `Firestone` in the last `Slot` exceeds the `target quantity`, then the `Price` will increase by 5% in the coming `Slot`.

如果上一周期火石存量（即该周期内全网实际购买生成的火石数量）低于目标值2048，则本周期火石价格下降5%；
If the actual quantity of `Firestone` in the last `Slot` does not exceed the `target quantity`, then the `Price` will decrease by 5% in the coming `Slot`.

The objective of this adjustment algorithm is to strike a balance between market demand and 'Firestone' supply.

<br />
<br />

## Instructions

<br />

1.向系统抵押LV获得火石（即购买火石）：
```
.\lava-cli.exe -rpcuser=test -rpcpassword=test buyfirestone "购买火石的地址" "指定找零地址"
```
成功执行返回交易ID。

需要注意，火石是关联到地址的。例如，您通过该命令给地址A购买了火石，未来只有地址A的私钥能够使用火石以及释放火石。

一般情况下，给挖矿地址购买火石即可，这样当您的挖矿地址出块时，火石也会被自动使用以获得双倍Coinbase收益。

此外，buyfirestone命令目仅支持向`P2PKH`地址（Pay2PubkeyHash地址，主网1开头地址）购买火石，不支持向`P2SH`地址（隔离见证地址，主网3开头地址）购买火石。

找零地址是指购买火石交易引用了可用的TX Input余额后，向用户返回多余资金时接受找零资金的地址。

<br />

2.查询当前周期（Slot）信息：
```
.\lava-cli.exe -rpcuser=test -rpcpassword=test getslotinfo
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

`index`表示现在处于第几个周期（Slot），周期从0开始计，即第一个周期的index=0。

`ticketprice`表示当前火石的价格，需要注意该价格是以satoshi为单位，除以100000000得到以LV计的价格。

`ticketcount`表示当前全网已经购买的火石数量。

`locktime`表示在当前周期购买火石的成熟块高，达到这个块高以后才可以使用现在购买的火石。

<br />

3.查询地址持有火石情况：
```
.\lava-cli.exe -rpcuser=test -rpcpassword=test getfirestone “你要查询的地址”
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

`outpoint`表示购买火石的交易ID，即当时购买该火石所发起的交易记录。

`address`表示火石所关联的地址。

`lockheight`表示该火石在这个块高以后为可用状态。

`state`表示火石的状态，`IMMATURATE`表示还未成熟（请等待下一个周期成熟），`USABLE`表示现在可用，`OVERDUE`表示已经过期。

`isSpent`表示火石是否被使用。false表示未被使用。

<br />

4.释放过期的火石

如果火石在出块的时候消耗掉了，就不需要手动释放；如果没有被消耗掉，需要在过期后手动释放。
```
.\lava-cli.exe -rpcuser=test -rpcpassword=test freefirestone "持有火石的地址" "接受释放资金的地址"
```
成功释放后返回交易ID。

如果您希望抵押的资金释放回原先持有火石的地址，两个地址填一样的即可。
