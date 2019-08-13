# P盘+挖矿教程完整总结版

### 概念介绍

>“P盘”是Plotting的俗称，指生成Plot文件并填入硬盘的过程。Plot文件是PoC挖矿所必须的基础数据，矿工的硬盘空余容量越大，即可填入更多Plot文件，增加成功出块的概率。如果您想参与Lava挖矿，必须在挖矿前预先完成P盘工作。

#### 步骤一：下载P盘软件

>我们推荐下载免费P盘软件TurboPlotter的最新版本，下载地址：[https://blackpawn.com/tp/](https://blackpawn.com/tp/)

>该软件的免费版仅支持同时P一块盘；

>付费版本（PRO版本以及UNLIMITED版本）则可以支持同时P更多盘，具体性能请参考blackpawn官网说明（以下为截图，仅供参考）。

>用户请根据个人需求选择并下载。

![img1.png](https://github.com/lavafy/testnet/blob/master/imgs/img1.png)


##### *下载链接参考*：

PRO版：[https://www.kuangjiwan.com/goods-58.html](https://www.kuangjiwan.com/goods-58.html)

UNLIMITED版：[https://www.kuangjiwan.com/goods-60.html](https://www.kuangjiwan.com/goods-60.html)



#### 步骤二、启动P盘软件

>第一次打开TurboPlotter时，界面会提示是否已有Plot文件。对于第一次使用并P盘的用户，请选择No。

![img2.png](https://github.com/lavafy/testnet/blob/master/imgs/img2.png)

>在进行P盘前，软件会要求用户填写“address”或“account ID”，此处实际是指您的==Plot ID==。请正确填写您准备好的Lava Plot ID；如果没有准备，请跳转后一步骤准备Plot ID。

![img3.png](https://github.com/lavafy/testnet/blob/master/imgs/img3.png)



#### 步骤三、生成Plot ID

>用户可以在全节点钱包内自行生成Plot ID。

>欲获取Lava全节点钱包，请前往Lava官网([www.lavatech.org](www.lavatech.org))顶部的下载栏目选择适用的环境版本进行下载。

>运行全节点钱包（请先确认lavad成功同步到区块链），输入命令: 
```
.\lava-cli.exe –testnet=1 -rpcuser=test -rpcpasword=test -getmineraddress
```
![img4.png](https://github.com/lavafy/testnet/blob/master/imgs/img4.png)

>Lava-cli 会返回 ==address== 和 ==plot id== 两个数据。Address就是用于挖矿并接受出块奖励的地址，Plot ID为对应此地址的Plot ID。


#### 步骤四、P盘参数设定

>在上文步骤二提及的界面中输入Plot ID后，就可以进入P盘主界面。

![img5.png](https://github.com/lavafy/testnet/blob/master/imgs/img5.png)


##### Processor选项:

>请选择使用CPU或GPU进行P盘。我们推荐使用性能优秀的GPU进行P盘，可大幅提升P盘效率。

##### SSD path选项:
>仅适用于SSD（固态硬盘）的情况，如果您使用固态硬盘存放Plot文件，则在此选项下填写存放路径，否则不需理会。

##### Target disk path选项: 
>对于非SSD的情况，请在此填写P盘的目标路径（即存放Plot文件的位置）。对于免费版，软件仅支持单个路径。

##### Start nonce选项：
>默认从0开始，如无特殊要求可直接选择自动模式（automatic）。Choose from file 表示继续P上次暂停的文件。

![img6.png](https://github.com/lavafy/testnet/blob/master/imgs/img6.png)

##### Max file size选项：
>定义您想要生成的单个Plot文件的体积；默认情况下软件会根据目标盘的可用剩余空间自适配。但我们建议不要超过1T，以防因P盘意外中断导致重新P盘耗时过多。
RAM to use选项：显示可用于P盘的系统内存。

##### RAM to use选项：
>显示可用于P盘的系统内存。



#### 步骤五、开始P盘

![img7.png](https://github.com/lavafy/testnet/blob/master/imgs/img7.png)


>完成以上设定后，点击Start plotting就可以开始P盘了。

>P盘中途如想暂停P盘，可点击pause（暂停）按钮 ==（警告：P盘程序可以暂停，但是不能退出。如果退出程序再进入，只能重新开始P盘。一般情况下，我们建议不要随意中断P盘进程。==）

![img8.png](https://github.com/lavafy/testnet/blob/master/imgs/img8.png)


>开始P盘后，程序显示以上界面，展示计算nonce和写入硬盘的速度，以及预计的剩余时间。


#### 完成P盘、开始挖矿

>请下载挖矿软件（Lava Miner） ，可前往Lava官网([www.lavatech.org](www.lavatech.org))顶部的下载栏目 -> Miner 进行最新版本的下载。

>完成下载后，按照如下配置设置==miner.conf== 文件：

```
{ "Mode" :  "pool",
"Server" : 目标服务器地址，如"127.0.0.1", 钱包节点在哪，就输入哪
"Port": 18332, 
"OwnerAddr" : 矿 工 lava 地 址 ，
"HttpAccount" : "test",
"HttpPassWord" : "test",
"AccountKey" : "sss",
"UpdaterAddr" : 目标服务器地址，如"127.0.0.1", 钱包节点在哪，就输入哪
"UpdaterPort": “18332”, 
"InfoAddr" : "100pb.online",
"InfoPort": "8124", 
"EnableProxy": false, 
"ProxyPort": 8126, 
"Paths": P 盘的盘符数组，形如：["E:\\","C:\\"], 
"CacheSize" : 16384, 
"CacheSize2" : 262144, 
"Debug": true, 
"UseHDDWakeUp": true, 
"TargetDeadline": 80000000, 
"SendInterval": 100, 
"UpdateInterval": 950, 
"UseLog" : true, 
"ShowWinner" : false, 
"UseBoost" : false, 
"MinerName": "sun", （单台矿机的识别名字） 
"WinSizeX": 76, 
"WinSizeY": 60 }
```

##### 其他注意事项：
1. 测试网rpc端口18332；
2. 配置文件必须配置以下字段：

```
("Server" ,"Port","OwnerAddr" ,"HttpAccount" ,"HttpPassWord" ,"UpdaterAddr" ,"UpdaterPort",  "Paths":["K:\\plots"] )
```
3. 挖矿地址一定要与plotid对应；

保存，将其放入 lava-miner.exe 相同的目录下，双击 lava-miner.exe 开启挖矿。

