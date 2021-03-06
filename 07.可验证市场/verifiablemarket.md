##   可验证市场


激励机制，放在共识层，可以，放在市场这里，也可以。如果从市场的角度来看，一个市场中，最重要的机制就是激励机制。
有两篇文章讨论了区块链的激励机制：    
+ 《电子货币激励机制综述》
+ 《Bitcoin's Underlying Incentives》

《Bitcoin's Underlying Incentives》我翻译了中文版，[这里](https://github.com/stone-note/articles)可以下载。

竞争让网络更加安全。《Bitcoin's Underlying Incentives》指出，比特币的安全性和经济性是相互作用的。危及安全性的因素包括：1，确保最长链规则；2，区块奖励下降，导致无人挖矿；3，交易量下降，矿工费下降，导致无人挖矿；4，竞争使得区块创建难度增加，矿工可以使用额外回报来购买更多的算力，并因此而变得更加强大，继而提升挖矿的难度，最终将其他小型（因而利润较低）矿工排挤出这场游戏；5，ASIC挖矿提高了系统的准入门槛：普通人无法轻易地加入挖矿工作，也因此减少了系统的去中心化。另一方面，ASIC挖矿也引入了一种退出的“门槛”：矿工无法将他们的设备用于其他经济活动，因此有助于提供系统的安全性。

《电子货币激励机制综述》提到的几种博弈模型值得研究：
+ Stackelberg博弈
+ 拍卖博弈


可验证市场以Filecoin为代表。Filecoin的文章主要在《存储证明》栏目下。
+ 存储市场
> 存储矿工与用户设定好自己的需求与价格提交到订单薄上面，并由去中心化的交易所进行撮合，当两者的价格与需求匹配的话，交易所会进行自动撮合，并把两者的交易提交到分配表上面，用户再发送自己的数据给矿工，系统会自动把用户的文件进行分片处理，处理之后再把分片的数据分发给存储矿工进行数据存储，filecoin系统向存储矿工发起挑战，存储矿工提交自己的存储证明，当存储矿工提交的存储证明是有效的正确的，系统会把存储证明提交到分配表上面，如果存储证明被网络协议运行证明是真实有效的，那么存储矿工将会收到用户的代币，并且交易记录会提交到区块链上面。（存储市场的交易是通过链上交易的）存储矿工与用户设定好自己的需求与价格提交到订单薄上面，并由去中心化的交易所进行撮合，当两者的价格与需求匹配的话，交易所会进行自动撮合，并把两者的交易提交到分配表上面，用户再发送自己的数据给矿工，系统会自动把用户的文件进行分片处理，处理之后再把分片的数据分发给存储矿工进行数据存储，filecoin系统向存储矿工发起挑战，存储矿工提交自己的存储证明，当存储矿工提交的存储证明是有效的正确的，系统会把存储证明提交到分配表上面，如果存储证明被网络协议运行证明是真实有效的，那么存储矿工将会收到用户的代币，并且交易记录会提交到区块链上面。（存储市场的交易是通过链上交易的）


+ 检索市场
> 检索市场允许客户请求检索用户所需要的数据，并且由检索矿工来提供检索服务。    
> 检索矿工不需要在一定的周期内存储数据以及生成存储证明并向网络证明自己在特定的时间内存储了用户所需要存储的数据，检索矿工是不参与挖区块这一环节的，检索矿工只能从市场或者客户哪里获取相应的费用。   
> Filecoin网络中检索矿工通过提供检索服务来获取Filecoin。   
> 检索矿工可以直接从客户端或者检索接收数据碎片，也可以存储数据碎片成为存储矿工。  
> 检索矿工与用户根据自己的需求与价格提交到去中心化的交易所，当两者的需求与价格是匹配的，交易所会自动进行匹配，当检索矿工把数据碎片发送给用户，检索矿工就此可以收到用户支付的费用，并且两者的交易记录会提交到区块链上面。   
> 检索市场的交易不是在链上进行的，是开通的小额支付通道进行交易。   
> 并且检索市场是没有区块链网络来进行见证数据交换的，他是采用的零知识证明，系统要求检索矿工将数据碎片发送给用户来达到目的。    
> 如果检索矿工与客户一方停止发送数据以及停止付款的话，任何一方都可以终止此交易。   

+ 检索市场的设计
> 链下订单薄 -- 客户端需要找到能提供用户所需要的数据碎片的检索矿工，并且在定价之后进行直接交易。   
> 快速的进行交易并形成交易订单向订单薄进行提交，会成为检索请求的瓶颈，所以检索市场的订单薄不能通过区块链来记录，只能通过链下订单薄来进行记录。   

> 无信任方验证 -- 在存储市场，由区块链网络作为去中心化的信任方来验证存储矿工所提供的存储证明。   
> 在检索市场没有第三方来进行见证交换文件的情况下来交换数据，检索市场采用的零知识证明来进行验证此交换数据的真实性，所谓的零知识证明，就是不需要知道里面的内容，通过要求检索矿工将数据碎片的多个部分发送给客户来达到此目的，当用户收到文件的时候，那么检索矿工也将会收到所对应的交易费用.   

> 支付通道 -- 客户当提交付款的时候，可以立即检索所需要的数据。检索矿工当确认收到付款的时候，才会提供数据碎片。   
> 通过区块链账本来确认交易可能会成为检索请求的瓶颈，所以检索市场选择的是进行的链下支付（就跟比特币的闪电网络一样的）。   
> Filecoin区块链交易必须支持快速的支付通道，如果检索市场要支持链上交易的话，只有等到区块链能满足高并发的交易量以及检索交易的时候出现纠纷的时候才会使用区块链。   

+ 检索市场的运行；

> 获取订单 -- 检索市场中包含三种类型的订单； 客户创建出价单Obid，检索矿工创建询价订单Oask，与存储矿工和客户端达成的交易订单Odeal。
> 获取订单薄 -- 检索市场的订单薄是有效的并且都是公开的出价订单，询价订单和交易订单的集合。与存储市场不同，检索市场的每个用户有不同的订单薄，因为订单薄是在网络中进行传播的，每个矿工和客户只会跟踪他们所感兴趣的订单。
> 在Filecoin检索市场，检索矿工可以根据用户所要求检索的内容，知道那些是高访问的内容，检索矿工可以将起存储，这样可以增加额外的收益。   


借鉴交易所架构设计：    
![arch1](https://raw.githubusercontent.com/stone-note/stone-note.github.io/master/_pictures/2018-12-13-trademaket.png)   

EtherFlyer交易所实例（github地址：https://github.com/EtherFlyer/etherflyer_exchange_server）：    
![arch2](https://user-images.githubusercontent.com/33028500/32134960-134bcb4e-bc32-11e7-9dbf-1017adc4e893.jpg)    

Order placement and trading procedure(link: http://csx.com.kh/operation/market/listPosts.do?MNCD=30201)    
![arch3](http://csx.com.kh/en/common/img/operation/img_market2_1_1.gif) 


https://medium.com/prysmeconomics/blockchain-incentives-101-what-they-are-and-why-they-matter-5127afb56aeb



《swap, swear and swindle: incentive system for swarm and beyond》
以太坊的swarm存储系统期望做到两个方面：
+ 内容交付
> 数据能够检索：把节点的ID，数据块的ID映射到同一地址空间，数据块保存在最接近其ID的节点上。swarm的检索进程负责完成内容的交付,这个功能类似IPFS的bitswap。swap: swarm accounting protocol 会对peer之间的带宽进行审计，并跟踪流入和流出 两个方向的数据检索。如果两者两个peer之间有特别不对等的服务，则需要付费。

> 为数据付费
并且为每一个数据块交易付费是不可行的。甚至是批量付费也会造成区块膨胀。为了不用把每一次支付上链，SWAP引入了一个 chequebook 智能合约：chequebook 在多个swarm 节点之间传递，peer可以在任意时刻结账，账单是累积的，只有最后一个账单需要结账并上链。
SWAP 会很快支持 payment channel 。
chequebook 和 payment channel 各有优缺点。

+ 内容存储
> 延迟交付和存储证明，以太坊这里成为保管证明:proof of custody。SWAP保证热点数据的检索，但没有保证冷门数据的持久可用。proof of custody解决这一问题。基本的想法是：swarm存储节点提前提交一部分押金，持续一段时间，向swarm存储节点发起挑战，节点需要证明数据仍然是可用的。每一次 proof of custody 都向swarm存储节点释放一部分费用。需要注意的是 proof of custody 只是一个很小的消息。

这样的延迟支付构成一个第三方保管的条件支付合约：费用预先支付，但是暂由第三方保管，当且仅当（条件）收到一个有效的proof of custody时，才真正支付费用。

上面的过程可以直接在off-chain完成，并和 payment channel 结合在一起。这里需要一个能够理解存储证明的判断合约即可。

如果swarm存储节点丢失数据，则会失去收入。

为了激烈节点完成存储，swarm引入一个保险机制来惩罚没有遵守存储承诺的节点。

SWEAR ：保证数据的归档存储

SWINDLE ：数据丢失的诉讼。

> 存储合约和负激励




