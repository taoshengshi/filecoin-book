##   架构设计



架构思考：
目前，我们处于区块链演进的一个关键节点上。

比特币的核心创新是什么？

在开放，去中心的成员关系环境下，基于工作量证明的leader选举。


Principle
* Local Storage vs. Outsourced Storage
* Centralized vs. Decentralized
* Mutable vs. Immutable 
* P2P vs. Enterprise
* Blockchain vs. Cloud

Philosophy
* Contract is for resource（Storage & Computing）
* Coin is for Contract
* Chain is for Coin


区块链，作为一个支持多方交易的网络，可以支持创新型的交易应用。

区块链作为软件连接器：《A Review Of Blockchain》

区块链作为可验证市场：以为filecoin为代表。

验证驱动的交易：《Research Directions in Blockchain Data Management and Analytics》

机器验证的安全（Machine-checked security）：《Proving confidentiality in a file system using DISKSEC》


##   开放系统和封闭系统
因为在数据库事务处理领域的杰出贡献而获得图领奖的Jim Gray是一位值得尊敬的科学家。他在1995年10月的一篇文章《Jim Gray’s NTclusters Research Agenda》，指出了集群和分布式系统区别：
集群与分布式系统有何不同?
看起来，一个集群是分布式计算系统的一种——万维网、Solaris系统组成网络，等等。当然，集群是一种简化的分布式系统。但是，这些简化带来的本质差异足以使集群算法显著不同。
* 同质性：集群是一个同质系统：它有一个相同的安全策略、审计政策、一个命名方案，并且可能运行在单一的处理器或操作系统之上。不同节点可能有不同速度和版本的软件和硬件，但它们都非常相似。而一个分布式系统是一个计算机的动物园，有许多不同种类的计算机。
* 局部性：集群的所有节点都在附近，通过本地高速网络连接。网络带宽很高，因为网络是由现代的硬件和软件组成。网络带宽很便宜，因为网络不经过电信公司。集群是高可靠的，因为集群在一个受控的环境中。而且集群是高效的，因为集群可以使用专门的协议栈来优化本地通信。而分布式系统中的通信是相对缓慢、不可靠和昂贵的。
* 信任：集群中的节点彼此信任。它们为彼此进行身份验证、共享负载、提供故障转移，总之，集群是一个联邦。而分布式系统通常是相互怀疑节点的自治集合。

> How does a Cluster Differ From a Distributed System?
   It may seem that a cluster is just a kind of distributed computing system -- like the world wide web or a network of Solaris systems or....  Certainly, a cluster is a simplified kind of distributed system.  But, the differences are substantial enough to make cluster algorithms significantly different.    
   Homogeneity: A cluster is a homogeneous system: it has one security  policy, on accounting policy, one naming scheme and probably is running a single brand of processor and operating system.   There may be different speeds and versions of software and hardware from node to node, but they are all quite similar.  A distributed system is a computer zoo -- lots of different kinds of computers.
   Locality:   All the nodes of the cluster are nearby and are connected via a high-speed local network.   This network has very high bandwidth since it is modern hardware and software  The bandwidth is inexpensive since it does not come from the phone company.  It is reliable since it is in a controlled environment;  and it is efficient since it can use specialized protocol stacks optimized for local communication.  Communication in a distributed system is relatively slow, unreliable, and expensive.
   Trust:  The nodes of a cluster all trust one another.   They do authentication for one another, they share the load, they provide failover for one another, and in general they act as a federation.   A distributed system is more typically an autonomous collection of mutually suspicious nodes.


##   不可能三角

![three](https://github.com/stone-note/stone-note.github.io/blob/master/_pictures/blockchainNG/three.png?raw=true)

追求“安全”与“去中心化”则无法达到“可扩展性”
追求“可扩展性”与“去中心化”则需要牺牲“安全”
追求“可扩展性”与“安全”则无法实现“去中心化”


##   胖协议

这是考虑互联网和区块链差异的一种方法。上一代的共享协议（TCP / IP，HTTP，SMTP等）产生了不可估量的价值，但其中大部分被捕获并重新聚合在应用层上，主要是数据形式（认为Google ，Facebook等）。就价值如何分配而言，互联网栈由“瘦”协议和“胖”应用程序组成。随着市场的发展，我们了解到投资于应用产生高回报，而直接投资于协议技术通常产生低回报。

![fat1](https://github.com/stone-note/stone-note.github.io/blob/master/_pictures/blockchainNG/fat1.png?raw=true)

协议和应用程序之间的这种关系在区块链应用程序堆栈中相反。值集中在共享协议层，并且只有一部分值分布在应用程序层。这是一个包含“胖”协议和“瘦”应用程序的堆栈。

我们在两个占统治地位的区块链网络比特币和以太坊看到了这一点。比特币网络拥有10亿美元的市值，但最大的顶级公司价值最多只有几亿美元，而大多数公司可能被“商业基础”标准高估。类似的，Ethereum甚至在真正的突破性应用出现之前，仅在其公开发布一年之后才拥有了1亿美元的市值。
![fat2](https://github.com/stone-note/stone-note.github.io/blob/master/_pictures/blockchainNG/fat2.png?raw=true)


##   区块链：开放成员关系下的状态机复制

PBFT的缺点：
开放成员关系
数百副本的扩展性
区块冲突
交易提交速率

强一致 和 概率一致
比特币的中本聪共识是一种概率一致性
强一致性的优点：
无需工作量证明
无需等待提交完成
前向安全


## 中本聪共识

运行比特币网络的步骤如下：
1) 新的交易向全网进行广播；
2) 每一个节点都将收到的交易信息纳入一个区块中；
3) 每个节点都尝试在自己的区块中找到一个具有足够难度的工作量证明；
4) 当一个节点找到了一个工作量证明，它就向全网进行广播；
5) 当且仅当包含在该区块中的所有交易都是有效的且之前未存在过的，其他节点才认同该区块的有效性；
6) 其他节点表示他们接受该区块，而表示接受的方法，则是在跟随该区块的末尾，制造新的区块以延长该链条，而将被接受区块的随机散列值视为先于新区快的随机散列值。

共识的基本问题：
Who should produce the next block of updates to apply to the database?
谁可以像数据库中添加下一个区块？
When should the next block be produced?
什么时候可以生产下一个区块？
What transactions should be included in the block?
区块中应该包含哪些交易？
How are changes to the protocol applied?
协议如何应用更新？
How should competing transaction histories be resolved?
如何解决竞争的交易历史？


##   架构演进

![decentralizedarch](https://github.com/stone-note/stone-note.github.io/blob/master/_pictures/blockchainNG/decentralizedarch.png?raw=true)

![decentralizeddecisions](https://github.com/stone-note/stone-note.github.io/blob/master/_pictures/blockchainNG/decentralizeddecisions.png?raw=true)

![decentralizedlevel](https://github.com/stone-note/stone-note.github.io/blob/master/_pictures/blockchainNG/decentralizedlevel.png?raw=true)

![decentralizedprojects](https://github.com/stone-note/stone-note.github.io/blob/master/_pictures/blockchainNG/decentralizedprojects.png?raw=true)

![blockchainconfig](https://github.com/stone-note/stone-note.github.io/blob/master/_pictures/blockchainNG/blockchainconfig.png?raw=true)

Design process for blockchain-based systems：
![blokchaindesignflow](https://github.com/stone-note/stone-note.github.io/blob/master/_pictures/blockchainNG/blokchaindesignflow.png?raw=true)



##   Tangle背后的数学原理


##   架构案例



[survey blockchain storage computing services](https://blog.coinfabrik.com/survey-blockchain-storage-computing-services/)
    


![bitcoincorearch](https://github.com/stone-note/stone-note.github.io/blob/master/_pictures/blockchainNG/bitcoincorearch.png?raw=true)

![blockstack1](https://github.com/stone-note/stone-note.github.io/blob/master/_pictures/blockchainNG/blockstack1.png?raw=true)

![blockstack2](https://github.com/stone-note/stone-note.github.io/blob/master/_pictures/blockchainNG/blockstack2.png?raw=true)

> Overview of Blockstack’s architecture. Blockchain records give (name, hash) mappings. Hashes are looked up in routing layer to discover routes to data. Data, signed by name owner’s public-key, is stored in cloud storage.

![siaarch](https://github.com/stone-note/stone-note.github.io/blob/master/_pictures/blockchainNG/siaarch.png?raw=true)
> 简单来说，我们使用Sia的客户端上传到我们的文件，Sia客户端会把文件分割成多份比如10份，分别存放到30个主机中, 那么你的一份文件同时保存在3个备份，而且每个主机只保存一部分文件的数据，就保证了数据的隐私性，没有人可以偷窥你的文件.
  通过SiA,你的一个文件可以有多个备份，你的文件不会被他人偷窥，你的文件可以随时随地的下载。
  当然你在托管主机的文件的同时，可以把你的电脑拿出来当作主机，托管他人的文件，可以赚些费用.
  Sia的主要目标是提供一个去中心化的，有奖励机制的，数据加密、低廉费用、使用方便的云储存系统，而这个系统将与中心化的类似系统（主要是像支持Dropbox的亚马逊 S3这样的系统）竞争。


![filecoinarch](https://github.com/stone-note/stone-note.github.io/blob/master/_pictures/blockchainNG/filecoinarch.png?raw=true)



![filecoin1](https://github.com/stone-note/stone-note.github.io/blob/master/_pictures/blockchainNG/filecoin1.png?raw=true)


![filecoin2](https://github.com/stone-note/stone-note.github.io/blob/master/_pictures/blockchainNG/filecoin2.png?raw=true)


https://datum.org/
![Datum](https://github.com/stone-note/stone-note.github.io/blob/master/_pictures/blockchainNG/Datum.png?raw=true)
> The distributed database & marketplace for safe exchange and trade of data. Powered by Ethereum, BlockchainDB and IPFS.
  
>  User submits data and gets paid by a consumer; 
>  1. User submits a piece of data to the Datum Network using the client software. The user pays gas to submit the data. As the data is encrypted, only the user can provide a decryption key to all the interested parties. 
>  2. A Storage Node receives the data and stores the data. The data is replicated to many other storage nodes. 
>  3. A Data Consumer declares interest to purchase the piece of data.
>  4. The User receives a data purchase request with the details such as purchaser and price offered. He can agree to the purchase request or counter offer with a modified proposal. 
>  5. The User accepts the proposal, the user receives DAT Tokens and the decryption key is sent to the Data Consumer who pays in DAT Tokens.


![Tahoe-LAFS](https://github.com/stone-note/stone-note.github.io/blob/master/_pictures/blockchainNG/Tahoe-LAFS.png?raw=true)

[tahoe-lafs](https://tahoe-lafs.org/trac/tahoe-lafs)
    


![enigma](https://github.com/stone-note/stone-note.github.io/blob/master/_pictures/blockchainNG/enigma.png?raw=true)
> To illustrate, consider the following example: a user installs an application that uses our platform for preserving her privacy. As the user signs up for the first time, a new shared (user, service) identity is generated and sent, along with the associated permissions, to the blockchain in a Taccesstransaction. Data collected on the phone (e.g., sensor data such as location) is encrypted using a shared encryption key and sent to the blockchain in a Tdata transaction, which subsequently routes it to an off-blockchain key-value store, while retaining only a pointer to the data on the public ledger (the pointer is the SHA-256 hash of the data).

![eosarch](https://github.com/stone-note/stone-note.github.io/blob/master/_pictures/blockchainNG/eosarch.png?raw=true)


![ethswarm](https://github.com/stone-note/stone-note.github.io/blob/master/_pictures/blockchainNG/ethswarm.png?raw=true)


![web30stack](https://github.com/stone-note/stone-note.github.io/blob/master/_pictures/blockchainNG/web30stack.png?raw=true)


Application design with and without Syndicate.
![syndicate](https://github.com/stone-note/stone-note.github.io/blob/master/_pictures/blockchainNG/syndicate.png?raw=true)


[Decentralized Markets for Data and Artificial Intelligence](https://www.slideshare.net/DimitriDeJonghe/decentralized-markets-for-data-and-artificial-intelligence)
    
##   零知识证明

机密性confidentiality：通过加密消息来防止攻击者读取消息内容。
完整性integrity：攻击者不能读取，但能修改消息中的某些位。技术虽然不能避免篡改，但可以检测到篡改。能够检测篡改的协议称为提供了数据完整性。
不可抵赖：
可用性：
认证：

##   跨链
BM说：
Inter-blockchain communication is the ultimate scalability feature — the holy grail — that the industry has been searching for with proposals such as side-chains, plasma, and sharding.

##   区块图


##   一些重要的白皮书


  
https://ethfans.org/posts/blockchain-infrastructure-landscape-a-first-principles
http://8btc.com/doc-view-1184.html

## Transaction in Ethereum
[key]https://blog.csdn.net/TurkeyCock/article/details/80485391   
https://blog.csdn.net/cj2094/article/details/80343004  
https://blog.csdn.net/shebao3333/article/details/80041358   
https://bitshuo.com/topic/5948897c8e822fcb444317d0   
http://blog.luoyuanhang.com/2018/05/02/eth-basis-block-concepts/   
https://github.com/xianfeng92/ethereum-code-analysis/blob/master/notes/ethDB.md   



## Reference
* [GFS](https://research.google.com/archive/gfs-sosp2003.pdf)
* [Hadoop](http://hadoop.apache.org/)
* [Sia](https://github.com/NebulousLabs/Sia)
* [BitCoin](https://github.com/bitcoin/bitcoin)
* [IPFS](https://github.com/ipfs/go-ipfs)
* [Storj](https://github.com/storj)
* [MaidSafe](https://github.com/maidsafe)
* https://paper.seebug.org/642/   
* https://www.jianshu.com/p/94769c88feac   
* https://ethfans.org/posts/blockchain-infrastructure-landscape-a-first-principles   
* https://studygolang.com/articles/13588    
* http://blockchainbrother.com/article/6346
* https://blog.csdn.net/teaspring/article/category/7157777
* https://github.com/ZtesoftCS/go-ethereum-code-analysis
* https://www.haowuliaoa.com/article/info/11636.html
* https://paper.seebug.org/642/
* https://blog.csdn.net/teaspring/article/details/78050274
* https://blog.csdn.net/TurkeyCock/article/details/80586951
* https://blog.csdn.net/superswords/article/details/76445278

## Instantiate ethereum
* https://medium.com/mercuryprotocol/how-to-create-your-own-private-ethereum-blockchain-dad6af82fc9f


Enigma: Decentralized Computation Platform with Guaranteed Privacy
Decentralizing Privacy: Using Blockchain to Protect Personal Data
IPFS - Content Addressed, Versioned, P2P File System (DRAFT 3)
Towards Blockchain-based Auditable Storage and Sharing of IoT Data
Syndicate: Virtual Cloud Storage through Provider Composition
Blockchains and Databases: A New Era in Distributed Computing
TRUST-TO-TRUST DESIGN OF A NEW INTERNET

