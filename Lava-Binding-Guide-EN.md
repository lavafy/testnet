# A Guide for Lava Binding Mechanism

<br />

## Basic Concepts:

<br />

### 1.What is "Binding"?

`Binding` is a special on-chain agreement between two miners. It is a unique mechanism as an innovation from `Lava`.

`Binding` is an agreement (more exactly, a contract) that helps a miner authorize to entrust his mining capacity (and following block rewards) to another miner's `address`, as if the two miners are mining as a whole.

*A simple illustration:*

*Given that Alice has a mining address (Addr_A) and 1TB disk capacity available for mining, Bob has a mining address (Addr_B) and 300TB disk capacity available for mining.*

*Now, Alice submits a binding request (via a special transaction on-chain) to the network. This request turns to be valid as soon as the transaction is recorded on the blochchain.*

*When mining, Both Alice and Bob provides their own Plot files and participated in the mining process, just acts like a normal miner.*

*a) If Alice happens to mine a block, the block will be entitled with Alice's Plot ID, but the following mining reward goes to Bob's address (Addr_B);*

*b) IF Bob happens to mine a block, the block will be entitled with Bob's Plot ID, and the following mining rewards goes to Bob's address (Addr_B).*


<br />

### 2. What does it mean to a Lava miner?

Some miners would like to bind his capacity to someone else, because this agreement could provide some positive results.

Just imagine a miner with very limited capacity (like Alice). 

Think about that if this "small" miner binds him/herself to a "big" miner (just like Bob), his/her mining yield will be significantly "smoothed" and "flattened".

<br />

### 3. Yield distribution between miners:

It should be hightlighted that even though binding actions are proceeded on-chain (which means they are totally decentralized), the mining yield can be distributed between the two miners in a very subjective and customized way.

Think about the Alice and Bob case we just talked above. One reasonable solution is that Alice gets 1/300 of the total yields from Bob's address on a weekly basis, what ever how many blocks mined by Alice and how many by Bob during the period.

Actually, any distribution scheme is feasible as long as the two parties are cool with it.

<br />


## Instructions:

<br />

### 1. Submit a binding request:
```
.\lava-cli.exe -rpcuser=test -rpcpassword=test bindplotid "fromaddress" "targetaddress"
```
When executed, the `TxID` for the binding transaction will be returned.

In the Alice and Bob case, `fromaddress` should be Alice's address (Addr_A), and `targetaddress` should be Bob's address (Addr_B).

<br />

### 2.Inquery for existing binding relationship on-chain:
```
.\lava-cli.exe -rpcuser=test -rpcpassword=test listbindings 
```
When executed, a list with details which shows all the existing binding relationships recorded on-chain will be returned. 

The list looks like:
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

<br />

### 3. Remove or disable an one's existing binding relationship:
```
.\lava-cli.exe -rpcuser=test -rpcpassword=test unbindplotid "one's address"
```
Notice that every address is allowed to bind to only one miner address at a time. So if a miner would like to disable his existing binding, or change a binding target, he/she should in the first place unbind the former one.

When executed, a `TxID` for the unbinding transaction will be returned. After the transaction is recorded on-chain, the binding relationship is formally (technically) removed or disabled.



