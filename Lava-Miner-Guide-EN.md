### Lava mining guide (Lava Miner)

# STEP 1: Download Lava Miner

Please go to Lava official site(lavatech.org)->Top Bar->Download to get the latest release of `Lava Miner`.

![abc1.png](https://github.com/lavafy/testnet/blob/master/imgs/abc1.png)

# STEP 2: SET CONFIG
 
Open `miner.conf` file:
![abc2.png](https://github.com/lavafy/testnet/blob/master/imgs/abc2.png)


Configurations should be set like below：
 
 { "Mode" :  "pool",

"Server" :, Target server (where full node runs) address, like "192.168.3.86"; if your full node and miner are both local: “127.0.0.1”

"Port": 8332, (Mainnet:8332; Testnet:18332)

"OwnerAddr" : ,(your mining address)

"HttpAccount" : "test",(identical to your full node settings--rpcuser)

"HttpPassWord" : "test",(identical to your full node settings--rpcpassword)

"AccountKey" : "sss",

"UpdaterAddr" : ,Target server (where full node runs) address, like "192.168.3.86"; if your full node and miner are both local: “127.0.0.1”

"UpdaterPort": “8332”,  (Mainnet:8332; Testnet:18332)

"InfoAddr" : "127.0.0.1", default set to local if not specified.

"InfoPort": "8124", 

"EnableProxy": false, 

"ProxyPort": 8126, 

"Paths": Indicate the disk(s) where your plot file lies, like ["E:\\","C:\\"], 

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

"MinerName": "sun", (an recognition name for your mining equipment)

"WinSizeX": 76, 

"WinSizeY": 60 }

Special Tips:

a.Mainnet port:8332; Testnet port:18332

b.Must have:("Server" ,"Port","OwnerAddr" ,"HttpAccount" ,"HttpPassWord" ,"UpdaterAddr" ,"UpdaterPort",  "Paths")

c.Mining `address` and `Plot ID` should be RELEVANT (they should be created from a sole `getmineraddress` instruction).


# STEP 3: Start Mining

Save the config file and make sure that the file is under the same path with your `lava-miner.exe`.
Run `lavad.exe` (which is your full node that supports your mining progress) and make sure your full node syncs to the latest height.
PLEASE PAY EXTRA ATTENTION TO THE SYNC STATUS, because you will be mining IN VAIN if your full node NOT in sync with the blockchain.

![abc3.png](https://github.com/lavafy/testnet/blob/master/imgs/abc3.png)

After sync, double click `lava-miner.exe` to start mining!
![abc5.png](https://github.com/lavafy/testnet/blob/master/imgs/abc5.png)
