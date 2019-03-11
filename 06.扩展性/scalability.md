##  扩展性

性能，或者说是扩展性，是去中心化信任系统的必然代价，其根源在于去中心化的共识机制。

增大区块容量是一个简单直接的办法，但限制于网络容量和传播速度，这个方法效果有限。

另一个直接的方法是缩短出块间隔。

扩展性的主要问题：
> 1. 交易吞吐量不足
> 2. 链与链之间的资产难以交互


文献《On or Off the Blockchain? Insights on Off-Chaining Computation and Data》也有不错的综述。


下面介绍当前3类主流的、提升区块链交易吞吐量的方案。总体来说，通过修改共识算来提高扩展性不是实践中可以考虑的方法。
基于区块链的广域网模型，通过PoS/或者algrand类似的算法来提高出块速度，出块速度太快，不无法抵御广域网的传播延迟，
如果限制网络的规模，则又回到传统的集群模型，可以适用于联盟链的规模。所以我认为通过修改共识算法来提高扩展性在公链中是不可行的。

那么共识的发展，应该是从无用共识到有用共识，或者是基于PoS的有用共识。这个才是共识研究的方向。

而提高扩展性，可以在下面三个方向上继续深入。
 
##  bitcoin-NG      （onchain）

Onchain的一个基本提高扩展性的方法是：将领导者选举（通过工作量证明随机且偶尔执行）与交易序列化(交易打包)解耦。  
+ Bitcoin-NG：
> 文献《Bitcoin-NG:A Scalable Blockchain Protocol》提出了单个leader多个块的扩展模型。整个信任模型与比特币类似，但与比特币不同的是（比特币领导者节点只能提出一个区块来追加区块链），Bitcoin-NG将时间划分为epoch，领导者节点可以在其epoch期间单方面向区块链追加多笔交易，直到新领导者节点被选出。 Bitcoin-NG中有两种区块：关键区块和微区块。 关键区块包含一个难题答案，用于领导者选举。关键区块还包含一个公钥，用于签署由领导者节点生成的后续微区块。每个区块都包含对前一个微区块和关键区块的引用。费用会在当前领导者（40％）和下一个领导者（60％）之间分配。与比特币类似，通过增长（聚合所有关键区块的）最长分支来解决分叉问题。请注意，由于这些微块不包含工作量证明，所以微区块不会影响分支的长度。为了对微区块中创建分叉的领导者节点进行惩罚，后续的领导者节点可以在其关键块（包含被剪枝分叉中的第一个块的头部）之后插入特殊的有毒交易作为欺诈证据。这使恶意领导者节点的报酬无效，报酬的一小部分支付给告发领导者。当一位新领导者选出但前任领导者还没有收到，并继续产生微区块时，分叉也会出现。然而，一旦新领导者选举的宣布达到所有节点，这些分叉就会得到解决。
+ ByzCoin：
> 文献《Enhancing Bitcoin Security and Performance with Strong Consistency via Collective Signing》采用多个领导者共同快速决定是否应该将区块添加到区块链中。ByzCoin 通过扩展Bitcoin-NG（参见前面的章节）取代比特币的概率性交易一致性保证（具有强一致性），以实现高交易吞吐量。这有一个好处，即客户提交的交易将被添加到区块链中，区块链仍然是无分叉的，因为所有领导者都立即就区块有效性达成一致。 ByzCoin修改了Bitcoin-NG的关键区块生成机制：一组领导者，而不是单个领导者，产生一个关键区块，然后是微区块。领导者小组由近期时间窗口的矿工动态组成。每个矿工的投票能力与其在当前时间窗口的挖矿区块数量成正比，这是其哈希能力。当一位新矿工解决难题之后，它将成为现任领导小组的一员，更进一步，替换出最老的矿工。 ByzCoin使用与比特币相同的激励模式，但报酬由领导者小组成员按其比例分摊。

bitcoin-NG的关键在于：
+ The protocol divides time into epochs.    
+ In each epoch, a single leader is in charge of serializing state machine transitions.    
+ To facilitate state propagation, leaders generate blocks.   
+ The protocol introduces two types of blocks: key blocks for leader election and microblocks that contain the ledger entries. 
+ Each block has a header that contains, among other fields, the unique reference of its predecessor; namely, a cryptographic hash of the predecessor header.  

 bitcoin-NG的leader选举仍然采用原来的工作量证明算法。


##  sharding & DAG        （onchain）
Onchain的第二个想法是：改变区块链线性增长链的方式。
+ 通过放弃“区块”和“链”的概念来并行化出块过程。
> 文献《Blockchain-Free Cryptocurrencies A Rational Framework for Truly Decentralised Fast Transactions》 提出的框架通过放弃“区块”和“链”的概念来并行化这个过程（支持交易的图式交叉验证，而不是线性，可以理解为“区块图”）。每笔交易确认两笔交易（其双亲）并包含一些有效负荷（例如，加密货币）和工作量证明。

Onchain的第三个想法：在一致性协议所需的消息与添加到区块链的最终区块的计算和广播之间解耦
> 文献《A Secure Sharding Protocol For Open Blockchains》将节点分成称为“委员会”的组，每个委员会管理交易的一个子集（分片）。在委员会内，节点运行拜占庭一致性协议（例如，PBFT）以协定交易区块。如果该区块已被足够的节点签名，委员会将其发送给最终委员会。最终委员会将从委员会收到的一系列交易整理到一个最终区块中，然后在其成员之间运行拜占庭一致协议以增长区块链，并将附加区块广播给其他委员会。系统按epoch运行：分配给委员会的节点仅在epoch期间内有效。在这个epoch结束时，这些节点解决当前最终委员会产生的随机字符串难题，并将求解答案发送给下一个最终委员会。因此，在每个epoch，一个节点与委员会中的不同节点搭档，管理一组不同的交易。委员会数量与系统中可用算力成线性比例关系，但一个委员会内的节点数量是固定的。因此，随着更多节点加入网络，交易吞吐量增加而延迟不会增加，因为这里有一个解耦：一致性协议所需的消息与添加到区块链的最终区块的计算和广播之间的解耦。

##  payment channel （offchain）
offchain 的支付通道通过将大量交易离线处理，同时将区块链作为仲裁平台，处理通道支付过程中的异常情况。双向通道支付过程可分为3个阶段：
> 1. 初始阶段，用于双方建立通道
> 2. 支付阶段，通道双方完成支付，即通道状态的更新
> 3. 关闭通道阶段，双方关闭通道，赎回通道中自己的资金，在关闭通道的过程中，一旦某一方作恶，即利用之前的通道状态来牟利，将会触发提交阶段。在提交阶段中，双方提交证据（交易）使得外界（区块链）确定通道内的真是状态。

闪电网络：RSMC和HTLC。


文献：《Off-chaining Models and Approaches to Off-chain Computations》首次提出off-chain的概念模型分类。主要包括off-chain计算、off-chain存储、和混合off-chain模式。
文章重点讨论了off-chain计算及其分类：
+ categories Verifiable Computation
+ Secure Multiparty Computation
+ Enclave-based Computation
+ Incentive-driven Computation


收到《Scaling Nakamoto Consensus to Thousands of Transactions per Second》，辅助一些资料看一下：
+ https://cloud.tencent.com/developer/news/296106
+ https://www.jianshu.com/p/8627df6f911d


https://raiden.network/101.html


## 参考文献
+ SHEHAR BANO 等 《The Road to Scalable Blockchain Designs》
+ 潘晨 等 《区块链可扩展性研究：问题与方法》
+ 喻辉 等 《比特币区块链扩容技术研究》
+ Chenxing Li等 《Scaling Nakamoto Consensus to Thousands of Transactions per Second》

## to read

+ 《Sidechains: Decoupled Consensus Between Chains》
[A Fast and Scalable Payment Network with Bitcoin Duplex Micropayment Channels](https://www.tik.ee.ethz.ch/file/716b955c130e6c703fac336ea17b1670/duplex-micropayment-channels.pdf)   
[On Trees, Chains and Fast Transactions in the Blockchain](https://eprint.iacr.org/2016/545.pdf)     
[Teechan: Payment Channels Using Trusted Execution Environments](http://www.cs.cornell.edu/People/egs/papers/teechan.pdf)   
[Extending Existing Blockchains with Virtualchain](https://www.zurich.ibm.com/dccl/papers/nelson_dccl.pdf)   
[比特币区块链扩容技术研究]()   
[]()   
[]()   
[]()   
[]()   
[]()   
[]()   
