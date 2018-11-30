# research for blockchainNG


Note : the format of this doc refer from :https://markdown-it.github.io/


##  中文综述

在中文综述方面，有几篇文章值得推荐。   
+ 邵奇峰 等《区块链技术:架构及进展》
+ 袁勇 等 《区块链技术发展现状与展望》



##  扩展性
+ SHEHAR BANO 等 《The Road to Scalable Blockchain Designs》
+ 潘晨 等 《区块链可扩展性研究：问题与方法》
+ 喻辉 等 《比特币区块链扩容技术研究》

#### takeaway

性能，或者说是扩展性，是去中心化信任系统的必然代价，其根源在于去中心化的共识机制。

增大区块容量是一个简单直接的办法，但限制于网络容量和传播速度，这个方法效果有限。

扩展性的主要问题：
> 1. 交易吞吐量不足
> 2. 链与链之间的资产难以交互

当前3类主流的、提升区块链交易吞吐量的方案:
1. payment channel （offchain） 
2. bitcoin-NG      （onchain）
3. sharding        （onchain）

offchain 的支付通道通过将大量交易离线处理，同时将区块链作为仲裁平台，处理通道支付过程中的异常情况。双向通道支付过程可分为3个阶段：
> 1. 初始阶段，用于双方建立通道
> 2. 支付阶段，通道双方完成支付，即通道状态的更新
> 3. 关闭通道阶段，双方关闭通道，赎回通道中自己的资金，在关闭通道的过程中，一旦某一方作恶，即利用之前的通道状态来牟利，将会触发提交阶段。在提交阶段中，双方提交证据（交易）使得外界（区块链）确定通道内的真是状态。

闪电网络：RSMC和HTLC。

bitcoin-NG的关键在于：
+ The protocol divides time into epochs.    
+ In each epoch, a single leader is in charge of serializing state machine transitions.    
+ To facilitate state propagation, leaders generate blocks.   
+ The protocol introduces two types of blocks: key blocks for leader election and microblocks that contain the ledger entries. 
+ Each block has a header that contains, among other fields, the unique reference of its predecessor; namely, a cryptographic hash of the predecessor header.  

 bitcoin-NG的leader选举仍然采用原来的工作量证明算法。





