### Lava全节点钱包使用教程


# 步骤一：下载最新版全节点钱包

首先下载最新版本的钱包（windows全节点钱包），可前往Lava官网（www.lavatech.org）  顶部的下载栏目进行下载：

![abc6.png](https://github.com/lavafy/testnet/blob/master/imgs/abc6.png)

# 步骤二：解压缩

解压下载后的压缩包，解压后有lavad.exe和lava-cli.exe。

# 步骤三：运行lavad并完成同步

在执行文件目录下，按住shift右击打开powershell,如下图：

![abc7.png](https://github.com/lavafy/testnet/blob/master/imgs/abc7.png)

a.在打开的powershell界面中输入`.\lavad -rpcuser=test -rpcpassword=test`，然后回车，启动钱包。如下图：

![abc22.png](https://github.com/lavafy/testnet/blob/master/imgs/abc22.png)

lavad启动后，请等待程序自动同步至最新块高（最新块高信息可以在区块链浏览器中获得，同步过程可能需要消耗一定时间）。

# 步骤四：在钱包客户端（lava-cli.exe）内进行钱包操作

b.在执行目录下打开一个新的powershell（原lavad的窗口保留即可，无需再进行任何操作），输入`.\lava-cli -rpcuser=test -rpcpassword=test getblockchaininfo`可以查询链当前信息，chain值表示连接的区块链是主网（main）还是测试网（test）；blocks值表示当前已经同步到的区块高度。如下图：

![abc9.png](https://github.com/lavafy/testnet/blob/master/imgs/abc9.png)

c.如果需要查询帮助（会展示所有可用的命令列表）,输入`.\lava-cli -rpcuser=test -rpcpassword=test help`。如下图：

![abc10.png](https://github.com/lavafy/testnet/blob/master/imgs/abc10.png)

d.生成挖矿地址与Plot ID，输入`.\lava-cli -rpcuser=test -rpcpassword=test getmineraddress`获取。如下图：

![abc11.png](https://github.com/lavafy/testnet/blob/master/imgs/abc11.png)

e.备份钱包文件 ，输入`.\lava-cli -rpcuser=test -rpcpassword=test dumpwallet "filename"`。filename为文件名，可以自己另取。如下图：

![abc12.png](https://github.com/lavafy/testnet/blob/master/imgs/abc12.png)

f.导入钱包文件，输入`.\lava-cli -rpcuser=test -rpcpassword=test importwallet  "filename"`。”filename”为前面备份的钱包文件，需要带上路径。如下图：

![abc13.png](https://github.com/lavafy/testnet/blob/master/imgs/abc13.png)

g.停止钱包，输入`.\lava-cli -rpcuser=test -rpcpassword=test stop`。如下图：

![abc14.png](https://github.com/lavafy/testnet/blob/master/imgs/abc14.png)

h.导出私钥，输入`.\lava-cli -rpcuser=test -rpcpassword=test dumpprivkey "address"`。 其中address为钱包地址。如下图：

![abc15.png](https://github.com/lavafy/testnet/blob/master/imgs/abc15.png)

i.导入私钥 ,输入`.\lava-cli -rpcuser=test -rpcpassword=test importprivkey "key" true`。 其中key为需要导入的私钥。如下图:

![abc16.png](https://github.com/lavafy/testnet/blob/master/imgs/abc16.png)

j.设置交易费，输入`.\lava-cli -rpcuser=test -rpcpassword=test settxfee 0.00001`。如下图:

![abc17.png](https://github.com/lavafy/testnet/blob/master/imgs/abc17.png)

k.查询钱包余额，输入`.\lava-cli -rpcuser=test -rpcpassword=test getbalance`。如下图：

![abc18.png](https://github.com/lavafy/testnet/blob/master/imgs/abc18.png)

l.绑定算力，输入`.\lava-cli -rpcuser=test -rpcpassword=test  bindplotid "fromaddress" "targetaddress"`。其中fromaddress为p盘的plotid对应的那个地址，targetaddress为接受出块币奖励的地址。如下图：

![abc19.png](https://github.com/lavafy/testnet/blob/master/imgs/abc19.png)

m.查询绑定关系，输入`.\lava-cli -rpcuser=test -rpcpassword=test  listbindings `。如下图：

![abc20.png](https://github.com/lavafy/testnet/blob/master/imgs/abc20.png)

n.解绑算力，输入`.\lava-cli -rpcuser=test -rpcpassword=test unbindplotid "address"`。如下图：

![abc21.png](https://github.com/lavafy/testnet/blob/master/imgs/abc21.png)




