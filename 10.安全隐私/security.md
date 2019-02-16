## Content   

《密码学与博弈论的交叉研究综述》


https://jhalderm.com/

## to read
+ 《Research on the Security of Blockchain Data: A Survey》

https://asecuritysite.com/encryption/bn
http://web.xidian.edu.cn/qkdong/teach.html
http://staff.ustc.edu.cn/~billzeng/ns/ns.htm

《基于配对的密码学》
《基于双线性配对的加密方案及密钥协商协议》
https://blog.csdn.net/trustbo/article/details/8806441
https://medium.com/coinmonks/having-fun-with-bn-curves-37fb5b816f67
https://dearsw.github.io/2017/05/31/PBC/
2000年,Sakai等学者,以及Joux分别开创性地利用双线性配对构造出静态(非交互式)身份基密钥共享方案和一轮三方密钥协商协议,解决了公钥密码学界的两个著名难题。从那以后,双线性配对作为一种基本工具在设计崭新密码方案方面的有效作用不断被挖掘出来,出现了大量新颖而又实用的密码方案。例如,身份基加密方案、无证书加密方案、短签名方案、双方及多方身份基密钥协商协议等等。 利用双线性配对构造各种新型密码方案的研究,是当前公钥密码学研究领域的一个热点。


P2P网络层的eclipse攻击：
本部分是区块链网络最基础的一层。可以称为node management，或者 peer network ，或者 p2p network protocol。为什么把peer network设计作为区块链设计的第一个出发点？通过多篇eclipse attack论文的研究，可以看到，中本聪通过50%的算力，本以为可以保证网络的共识。但是网络的共识依赖于底层节点的管理。就像Low-Resource Eclipse Attacks on Ethereum’s Peer-to-Peer Network中所说的：

> Simply put, if the peer-to-peer network partitions, causing different nodes see different views of the blockchain, then how can these nodes actually come to a consensus about what the blockchain actually is?


Heilman在2015年发表《Eclipse Attacks on Bitcoin’s Peer-to-Peer Network》.Eclipse Attacks 就是说通过大量恶意节点垄断侵蚀一个受害节点的所有出入连接：

> We present eclipse attacks on bitcoin's peer-to-peer network. Our attack allows an adversary controlling a sufficient number of IP addresses to monopolize all connections to and from a victim bitcoin node. The attacker can then exploit the victim for attacks on bitcoin's mining and consensus system, including N-confirmation double spending, selfish mining, and adversarial forks in the blockchain. We take a detailed look at bitcoin’s peer-to-peer network, and quantify the resources involved in our attack via probabilistic analysis, Monte Carlo simulations, measurements and experiments with live bitcoin nodes. Finally, we present countermeasures, inspired by botnet architectures, that are designed to raise the bar for eclipse attacks while preserving the openness and decentralization of bitcoin’s current network architecture.


![eclipseattacks](https://github.com/stone-note/stone-note.github.io/blob/master/_pictures/blockchainNG/eclipseattacks.png?raw=true)








