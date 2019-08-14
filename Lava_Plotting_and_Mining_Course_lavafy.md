# Lava Plotting & Mining Instruction

### Basics

>Plotting stands for the process where Plot files are produced and filled into disks. Plot files are fundamental data arrays that are stored in disks statically and fetched during the PoC mining. The more storage capacity you possess, the more Plot files you can fill into the disk, and finally the more chance to produce a block. It is necessary to prepare Plot files before you start mining Lava!

#### Step 1：Download Plotting Softwares

We recommand a free plotting software --TurboPlotter from [https://blackpawn.com/tp/](https://blackpawn.com/tp/)

The basic version (which is totally free) supports only single plotting process at one time.

The Pro version and Unlimited version support multiple processes，for details please go to the official website  [https://blackpawn.com/tp/](https://blackpawn.com/tp/) . 

Please download the software accroding to mines's demand.



#### Step 2: Pre-settings

The enter page will ask if you already have existing Plot files; For new user, please click "No".

![img2.png](https://github.com/lavafy/testnet/blob/master/imgs/img2.png)

In the next page, you will be required to enter "address" or "Account ID", which is actually your Lava Plot ID. If you don't have one, please go to the next step.

![img3.png](https://github.com/lavafy/testnet/blob/master/imgs/img3.png)



#### Step 3: Get a new Lava Plot ID

You can get a new Lava Plot ID on your own in Lava Core (Lava full node wallet)

Please go to Lava official website ([www.lavatech.org](www.lavatech.org)) -> Download-> Full Node Wallet and choose your platform version.

Run lava-cli.exe in Powershell (please ganrantee that lavad.exe server is updated to the latest blocks), and type in command:
```
.\lava-cli.exe –testnet=1 -rpcuser=test -rpcpasword=test -getmineraddress
```
![img4.png](https://github.com/lavafy/testnet/blob/master/imgs/img4.png)

lava-cli will return an `address` and `plot id`. `address` stands for the Lava address that being used to mine Lava and receive corresponding block rewards; `plot id` stands for the Plot ID related with the mining address.


#### Step 4: Plotting Settings

Enter the page for Plotting settings:

![img5.png](https://github.com/lavafy/testnet/blob/master/imgs/img5.png)


`Processor`: Choose CPU or GPU to process plotting tasks. We suggest suing a decent GPU because this would evidently enhance the plotting process.

`SSD path`: Only available for SSD disks. If you use SSD to store Plot files, please define a file path here.

`Target disk path`: For HDD disks (not SSD), please define a file path here. Notice: the free version does not support multiple paths.

`Start nonce`: default start from '0'. Please set to automatic mode for normal usage. 

![img6.png](https://github.com/lavafy/testnet/blob/master/imgs/img6.png)

`Max file size`: Define the maximum size for a single Plot file (default: max size will fit into your disk size). We suggest an max size no more than 1 TB, because it takes too long to re-plot a file in contigencies.

`RAM to use`: indicates the system RAM available for the plotting process.



#### Step 5: Start Plotting!

![img7.png](https://github.com/lavafy/testnet/blob/master/imgs/img7.png)


After all the parameters are properly set, you can start plotting.

If you want to pause the plotting process, please click the "Pause" button. Warning: the plotting process can only be continued from "Pause", which means if you quit the process you have to start plotting from the beginning. Anyway, we do not recommand pausing, hanging, or stopping the plotting process. 

![img8.png](https://github.com/lavafy/testnet/blob/master/imgs/img8.png)


When the Plotter is running, a monitor page will occur. Calculating speed, write speed and an estimated remaining time will be displayed in this page. 


#### Start Mining!

Please go to the Lava official website ([www.lavatech.org](www.lavatech.org)) -> Download -> Lava Miner to download the latest mining software.

Please set the configuration file `miner.conf` before mining.

```
{ "Mode" :  "pool",
"Server" : your full node server, if local: "127.0.0.1"
"Port": 18332, 
"OwnerAddr" : your mining address ，
"HttpAccount" : "test",
"HttpPassWord" : "test",
"AccountKey" : "sss",
"UpdaterAddr" : your full node server, if local: "127.0.0.1"
"UpdaterPort": “18332”, 
"InfoAddr" : "100pb.online",
"InfoPort": "8124", 
"EnableProxy": false, 
"ProxyPort": 8126, 
"Paths": Path where you store your plot files, like：["E:\\","C:\\"], 
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
"MinerName": "sun", Name of the mining machine 
"WinSizeX": 76, 
"WinSizeY": 60 }
```

##### Notice:
1. the RPC port for Lava Testnet is: 18332;
2. Necessary fields in the configuration file：

```
("Server" ,"Port","OwnerAddr" ,"HttpAccount" ,"HttpPassWord" ,"UpdaterAddr" ,"UpdaterPort",  "Paths":["K:\\plots"] )
```
3. The address and plot id should be related (which means the plot id should be exactly produced from the mining address).

Save, and make sure the config file is under the same path with lava-miner.exe. Double-click lava-miner.exe to start mining!

