# A Guide for Lava Firestone

<br />

## A Brief Introduction to Lava Firestone

<br />

### 1. Definition

`Firestone` is a special built-in credential which is dynamically and consistantly created, consumed, or expired on-chain. 

a Firestone is:

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

In the current stage, Firestone can be acquired by **staking LV to the system**.

Simply put, any user can "buy" Firestone with his/her LV. Notice that it is not an one-time, irreversable "purchase" behavior, we would rather call it "buy" because we want to express the whole concept more familiar and understandable to all.  

Technically, the process of "buying a Firestone" is realized by **creating an on-chain transaction which "stakes" a certain quantity of LV to the system**.

<br />

### 3. the "Price" 

There is a certain staking ratio (which is call the `Price`) indicating that how many LV you need to stake to the system to get a Firestone.

The `Price` is **dynamically adjusted** according to an special adjustment algorithm, which is defined in the consensus level.

<br />

### 4. the "Slot"

A `Slot` is a period of time, whose length is defined by `Height` on the blockchain.

In this way, the Lava Blockchain is divided by every **2048 blocks**, and each divided result is called a `Slot`.

For example, blocks from #0~#2047 constitute `Slot #0`, blocks from #2048~#4095 constitute `Slot #1`, and so on.

The Firestone obtained by the user in the `N-1th Slot` is valid only in the `Nth Slot`. When the `Nth Slot` is over, the Firestone is automatically abolished (expired), and the staked funds will be returned.

If a miner mines a block and he has a valid (which means consumable or usable) Firestone, he is allowed to consume a Firestone to get additional coinbase reward from this block, which is twice of the fundamental coinbase reward.

For example, a new mined block produce 1) **320 LV** coinbase reward without Firestone consumed; 2) **640 LV** coinbase reward with a Firestone consumed.

<br />

### 5. Firestone expiration:

As described above, the Firestone obtained by the miner in the `N-1th Slot` is valid only in the `Nth Slot`.

If a Firestone is consumed in `Nth Slot` (of course the miner need to mine a block as a prerequisite), the corresponding fund (in terms of LV) that is staked in this Firestone will be released immediately.

If a Firestone is unable to be consumed in `Nth Slot` (say, if the miner is not lucky enough to mine a block), the Firestone will be expired automatically in `N+1th Slot`, and whose fund staked needs to be freed manually via a special transaction.

<br />

### 6. Firestone Price Adjustment Algorithm

The `Price` will be adjusted dynamically at the beginning of every new Slot coming. 

There is a `target quantity` for Firestone in each Slot, which is set to `2048` in the `Lava Mainnet`.

If the actual quantity of Firestone in the last Slot exceeds the `target quantity`, then the `Price` will increase by 5% in the coming Slot.

If the actual quantity of Firestone in the last Slot does not exceed the `target quantity`, then the `Price` will decrease by 5% in the coming Slot.

The objective of this adjustment algorithm is to strike a balance between market demand and Firestone supply.

<br />
<br />

## Instructions

<br />

### 1.Buy a Firestone
```
.\lava-cli.exe -rpcuser=test -rpcpassword=test buyfirestone "FirestoneAddress" "ReceiveChangeAddress"
```
When executed, the corresponding `Tx ID` will be returned.

Important Tips:

1) `FirestoneAddress` is the very address that carries the Firestone. After the purchase, only with the `PrivKey` to THIS address can you consume the Firestone (or free the Firestone if not consumed）.

2) In normal situations, `FirestoneAddress` should be your mining address. In this way, your Full Node will automatically consume a Firestone if a new block is mined and benefit this mining address with additional reward.

3) a `P2SH Address` CANNOT be the `FirestoneAddress` when buying a Firestone.

4)`ReceiveChangeAddress` is the address that will receive the change fund from the transaction.


<br />

### 2. Get Current Slot's Infomation
```
.\lava-cli.exe -rpcuser=test -rpcpassword=test getslotinfo
```
which returns results like:
```
{
  "index": 5,
  "price": 16716105000,
  "count": 10,
  "locktime": 767
}
```
Explanations:

`index` indicates which Slot you are currently at. index starts from #0, which means the first Slot is #0 Slot, and the second Slot is #1 Slot, and so on.

`ticketprice` indicates the current Price for a Firestone. The unit is `satoshi` (which is 10^-8 LV).

`ticketcount` indicates how many Firestones are created in this Slot (till the inquery time). 

`locktime` indicated the height where the Firestone bought will turn to be valid. In other words, it is also the end height for the current Slot.

<br />

### 3. Inquery for a Specific Address:
```
.\lava-cli.exe -rpcuser=test -rpcpassword=test getfirestone “Address”
```
which returns results like:
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
Explanations:

`outpoint` indicates the `Tx ID` for the very transaction that "buy the Firestone".

`lockheight` indicated the height where the Firestone will turn to be valid.

`state` indicates the status of the Firestone: `IMMATURATE` means not valid yet (need wait for the next Slot); `USABLE` means valid and consumable; `OVERDUE` means already expired.

`isSpent` indicates whether the Firestone is consumed or not. `FALSE` means not consumed. 

<br />

### 4. Free Expired Firestone

If a Firestone is unable to be consumed in `Nth Slot` (say, if the miner is not lucky enough to mine a block), the Firestone will be expired automatically in `N+1th Slot`, and whose fund staked needs to be freed manually via a special transaction.
```
.\lava-cli.exe -rpcuser=test -rpcpassword=test freefirestone "FirestoneAddress" "ReceiveRefundAddress"
```
When executed, a `Tx ID` will be returned.

`FirestoneAddress` and `ReceiveRefundAddress` can be the same address, which means you will get refund to your Firestone Address (usually your mining address).
