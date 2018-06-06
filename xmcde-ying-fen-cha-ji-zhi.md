# XMC的硬分叉机制

所谓硬分叉即不兼容旧版本客户端的分叉，新版本客户端产生的区块，旧版本的客户端不能确认。硬分叉一般会涉及到修改共识协议，例如修改挖矿算法等等。XMR经常性的硬分叉来添加新特性，修改挖矿算法等等，所以代码有一套硬件分叉的机制。XMC基于XMR的某个历史版本，同样继承了此分叉机制。

硬分叉设计到的代码主要有:

* src/cryptonote\_basic/hardfork.cpp
* src/cryptonote\_core/blockchain.cpp
* src/cryptonote\_core/cryptonote\_tx\_utils.cpp

hardfork.cpp中定义了struct mainnet\_hard_\_forks和struct testnet_\_hard_forks, struct中包含uint8\_t version， uint64\_t height，uint8\_t threshold，time\_t time_

`static const struct{`

`uint8_t version;`

`uint64_t height;`

`uint8_t threshold;`

`time_t time;`

`}`



