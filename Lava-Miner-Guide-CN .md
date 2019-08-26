###Lava挖矿教程（Lava Miner使用教程）

# 步骤一：下载Lava Miner

首先下载挖矿软件（Lava Miner），可前往Lava官网（www.lavatech.org）  顶部的下载栏目->Miner进行最新版本的下载。

![abc1.png](https://github.com/lavafy/testnet/blob/master/imgs/abc1.png)

# 步骤二：设置配置文件

完成下载后，首先需要配置好`miner.conf` 文件：  
![abc2.png](https://github.com/lavafy/testnet/blob/master/imgs/abc2.png)


按照如下配置设置：
 
 { "Mode" :  "pool",

"Server" : 目标服务器地址，如"192.168.3.86", 即钱包节点所在的地址

"Port": 8332, （主网为8332、测试网为18332）

"OwnerAddr" : 即矿工的挖矿地址,

"HttpAccount" : "test",

"HttpPassWord" : "test",

"AccountKey" : "sss",

"UpdaterAddr" : 目标服务器地址，如"192.168.3.86", 即钱包节点所在的地址

"UpdaterPort": “8332”, （主网为8332、测试网为18332）

"InfoAddr" : "100pb.online",

"InfoPort": "8124", 

"EnableProxy": false, 

"ProxyPort": 8126, 

"Paths": P 盘的盘符数组，形如：["E:\\","C:\\"], 如果有多个盘符，就输入多个，中间以逗号隔开

"CacheSize" : 16384, 

"CacheSize2" : 262144, 

"Debug": true, 

"UseHDDWakeUp": true, （如果不想看到HDD WAKEUP提示，可以设定为“false”）

"TargetDeadline": 80000000, 

"SendInterval": 100, 

"UpdateInterval": 950, 

"UseLog" : true, 

"ShowWinner" : false, 

"UseBoost" : false, 

"MinerName": "sun", （单台矿机的识别名字） 

"WinSizeX": 76, 

"WinSizeY": 60 }

a.主网RPC端口为8332，测试网RPC端口为18332；

b. 挖矿启动一定要加rpcuser与rpcpassword；

c. 挖矿配置文件需要配置("Server" ,"Port","OwnerAddr" ,"HttpAccount" ,"HttpPassWord" ,"UpdaterAddr" ,"UpdaterPort",  "Paths")

d.挖矿地址要与Plot ID相对应。


# 步骤三：开始挖矿

配置完成后，保存，并将该文件放在 lava-miner.exe 相同的目录下，然后启动lavad,并等待钱包成功同步：

![abc3.png](https://github.com/lavafy/testnet/blob/master/imgs/abc3.png)

钱包成功同步后，双击 lava-miner.exe 即可开启挖矿：
![abc5.png](https://github.com/lavafy/testnet/blob/master/imgs/abc5.png)
