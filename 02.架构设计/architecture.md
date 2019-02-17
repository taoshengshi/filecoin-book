##   架构设计



架构思考：

Principle
* Local Storage vs. Outsourced Storage
* Centralized vs. Decentralized
* Mutable vs. Immutable 
* P2P vs. Enterprise

Philosophy
* Contract is for resource（Storage & Computing）
* Coin is for Contract
* Chain is for Coin


区块链，作为一个支持多方交易的网络，可以支持创新型的交易应用。

区块链作为软件连接器：《A Review Of Blockchain》

区块链作为可验证市场：以为filecoin为代表。

验证驱动的交易：《Research Directions in Blockchain Data Management and Analytics》

机器验证的安全（Machine-checked security）：《Proving confidentiality in a file system using DISKSEC》


##   架构演进

![decentralizedarch](https://github.com/stone-note/stone-note.github.io/blob/master/_pictures/blockchainNG/decentralizedarch.png?raw=true)

![decentralizeddecisions](https://github.com/stone-note/stone-note.github.io/blob/master/_pictures/blockchainNG/decentralizeddecisions.png?raw=true)

![decentralizedlevel](https://github.com/stone-note/stone-note.github.io/blob/master/_pictures/blockchainNG/decentralizedlevel.png?raw=true)

![decentralizedprojects](https://github.com/stone-note/stone-note.github.io/blob/master/_pictures/blockchainNG/decentralizedprojects.png?raw=true)

![blockchainconfig](https://github.com/stone-note/stone-note.github.io/blob/master/_pictures/blockchainNG/blockchainconfig.png?raw=true)

![blokchaindesignflow](https://github.com/stone-note/stone-note.github.io/blob/master/_pictures/blockchainNG/blokchaindesignflow.png?raw=true)


##   架构案例

![bitcoincorearch](https://github.com/stone-note/stone-note.github.io/blob/master/_pictures/blockchainNG/bitcoincorearch.png?raw=true)

![blockstack1](https://github.com/stone-note/stone-note.github.io/blob/master/_pictures/blockchainNG/blockstack1.png?raw=true)

![blockstack2](https://github.com/stone-note/stone-note.github.io/blob/master/_pictures/blockchainNG/blockstack2.png?raw=true)

> Overview of Blockstack’s architecture. Blockchain records give (name, hash) mappings. Hashes are looked up in routing layer to discover routes to data. Data, signed by name owner’s public-key, is stored in cloud storage.

![siaarch](https://github.com/stone-note/stone-note.github.io/blob/master/_pictures/blockchainNG/siaarch.png?raw=true)


![filecoinarch](https://github.com/stone-note/stone-note.github.io/blob/master/_pictures/blockchainNG/filecoinarch.png?raw=true)



![filecoin1](https://github.com/stone-note/stone-note.github.io/blob/master/_pictures/blockchainNG/filecoin1.png?raw=true)


![filecoin2](https://github.com/stone-note/stone-note.github.io/blob/master/_pictures/blockchainNG/filecoin2.png?raw=true)



![Datum](https://github.com/stone-note/stone-note.github.io/blob/master/_pictures/blockchainNG/Datum.png?raw=true)


![Tahoe-LAFS](https://github.com/stone-note/stone-note.github.io/blob/master/_pictures/blockchainNG/Tahoe-LAFS.png?raw=true)


![enigma](https://github.com/stone-note/stone-note.github.io/blob/master/_pictures/blockchainNG/enigma.png?raw=true)


![eosarch](https://github.com/stone-note/stone-note.github.io/blob/master/_pictures/blockchainNG/eosarch.png?raw=true)


![ethswarm](https://github.com/stone-note/stone-note.github.io/blob/master/_pictures/blockchainNG/ethswarm.png?raw=true)


![web30stack](https://github.com/stone-note/stone-note.github.io/blob/master/_pictures/blockchainNG/web30stack.png?raw=true)





[Decentralized Markets for Data and Artificial Intelligence](https://www.slideshare.net/DimitriDeJonghe/decentralized-markets-for-data-and-artificial-intelligence).
    

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
