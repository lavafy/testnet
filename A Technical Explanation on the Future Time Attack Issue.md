# 未来时间戳出块问题成因，分析与解决
北京时间2019年8月18早上9点03分，lava测试网出现数据异常，具体表现为当前出块出现了未来的时间戳。

lava技术团队第一时间介入调查，向社区收集数据，分析和定位问题成因。当日上午10点，确认问题原因。以下是本问题的详细分析：

* #### 问题定义
在POC共识中，本问题可以被定义为未来时间攻击（FTA，future time attack)。具体表现为，在当前时间N下，全网出现N+t时间的块，t>0。

* #### 问题分析
在PoW和PoC共识中，全网难度D都会随着出块间隔进行相应的增减，但两者的区别在于：在PoW中，出块时间的远近最终由硬件计算能力决定，最终表现为nonce，而nonce是无法伪造的；虽然 PoC的出块时间也由硬件属性（硬件容量）决定，但其最终表现为时间，时间显然是可以伪造的。
本次测试活动中，由于钱包验证逻辑的不严谨以及验证余量过大，有人通过将本地时间向未来调整1~2小时的方法，使原本矿工应该等待的时间被抹去，钱包超前出块，并利用钱包的验证漏洞将块入链，至此，链上出现了存在未来时间的区块。
钱包验证存在的具体缺陷如下：
* ###### 钱包时间容忍量过大
测试网钱包时间容忍量为2小时，也即，钱包容忍新块的时间戳超过当前时间2小时。这直接导致节点对区块的时间不敏感，作恶节点仅通过修改出块的时间戳，即可出块，同时被其他节点接受。
* ###### 钱包出块并无缓存机制
测试网钱包在接到其他miner提供的区块时，进行验证，当区块通过验证后，钱包立即将其放入区块链顶端，并将同高度的其他区块结果拒绝。这导致作恶节点利用小算力，修改出块即可将大算力驱逐的情况，同时也导致了算力的浪费。

* #### 问题解决
* ##### 降低钱包时间容忍至15秒。
* ##### 新增钱包的本地时间与区块时间两者间的时间比对，目前未来时间区块已无法通过钱包的本地时间验证。
* ##### 新增钱包内的miner相关的区块缓存以及DeadLine缓存，目前钱包会正确存储最新高度的DeadLine和对应的区块，钱包等待正确的时间到来，才会将相应的区块放入链上。