### Lava Full Node (Lava Core) Guide


# STEP 1: Download Lava Full Node Wallet

Please go to Lava official website(lavatech.org)->Top Bar->Downlaod to get latest releases.

![abc6.png](https://github.com/lavafy/testnet/blob/master/imgs/abc6.png)

# STEP 2: Unarchive

Unarchive to get `lavad.exe` and `lava-cli.exe`

# STEP 3: Run lavad.exe and sync the blockchain data.

Long press SHIFT key and right-click, choose Powershell from right-click menu and click to start a Powershell interface.

![abc7.png](https://github.com/lavafy/testnet/blob/master/imgs/abc7.png)

a. start sync:
```
.\lavad -rpcuser=test -rpcpassword=test
```

![abc22.png](https://github.com/lavafy/testnet/blob/master/imgs/abc22.png)

Please wait up to several minutes to let the Full Node sync the blockchain data from the network and make sure it has already updated to the latest height from the blockchain.
You can get the current height and more info from our blockchain explorer (https://explorer.lavatech.org).

# STEP 4: Operate your full node wallet in the client(lava-cli).

b. Open a new Powershell interface (Notice: always keep the lavad interface running) and type:
```
.\lava-cli -rpcuser=test -rpcpassword=test getblockchaininfo
```
which returns an overview of the current blockchain status.

![abc9.png](https://github.com/lavafy/testnet/blob/master/imgs/abc9.png)

c. To get a full list of available instructions:
```
.\lava-cli -rpcuser=test -rpcpassword=test help
```

![abc10.png](https://github.com/lavafy/testnet/blob/master/imgs/abc10.png)

d. To create a new mining `address` and `Plot ID`:
```
.\lava-cli -rpcuser=test -rpcpassword=test getmineraddress
```

![abc11.png](https://github.com/lavafy/testnet/blob/master/imgs/abc11.png)

e. To backup your wallet:
```
.\lava-cli -rpcuser=test -rpcpassword=test dumpwallet "filename"
```

![abc12.png](https://github.com/lavafy/testnet/blob/master/imgs/abc12.png)

f. To import an existing wallet backup:
```
.\lava-cli -rpcuser=test -rpcpassword=test importwallet  "filename"
```
Please notice that filename should include a path.

![abc13.png](https://github.com/lavafy/testnet/blob/master/imgs/abc13.png)

g. To stop the full node:
```
.\lava-cli -rpcuser=test -rpcpassword=test stop
```

![abc14.png](https://github.com/lavafy/testnet/blob/master/imgs/abc14.png)

h. To export Private Keys:
```
.\lava-cli -rpcuser=test -rpcpassword=test dumpprivkey "your address"
```

![abc15.png](https://github.com/lavafy/testnet/blob/master/imgs/abc15.png)

i. To import Private Keys:
```
.\lava-cli -rpcuser=test -rpcpassword=test importprivkey "your privkey" true
```

![abc16.png](https://github.com/lavafy/testnet/blob/master/imgs/abc16.png)

j. To set transaction fee:
```
.\lava-cli -rpcuser=test -rpcpassword=test settxfee 0.00001
```

![abc17.png](https://github.com/lavafy/testnet/blob/master/imgs/abc17.png)

k. To get the balance from the wallet:
```
.\lava-cli -rpcuser=test -rpcpassword=test getbalance
```

![abc18.png](https://github.com/lavafy/testnet/blob/master/imgs/abc18.png)

l. To initiate a `Binding`:
```
.\lava-cli -rpcuser=test -rpcpassword=test  bindplotid "fromaddress" "targetaddress"
```
After the initiation, `targetaddress` will receive all the mining rewards from new blocks, whatever it is mined by `fromaddress` or `targetaddress`.

![abc19.png](https://github.com/lavafy/testnet/blob/master/imgs/abc19.png)

m. To inquire your existing `Binding` relation:
```
.\lava-cli -rpcuser=test -rpcpassword=test  listbindings 
```

![abc20.png](https://github.com/lavafy/testnet/blob/master/imgs/abc20.png)

n. To end an existing `Binding` relation:
```
.\lava-cli -rpcuser=test -rpcpassword=test unbindplotid "address"
```

![abc21.png](https://github.com/lavafy/testnet/blob/master/imgs/abc21.png)




