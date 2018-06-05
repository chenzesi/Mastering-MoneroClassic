# XMC实现离线钱包

不管是哪种数字货币，想要实现转账操作，都要使用私钥\(private key\)对交易签名。私钥，确保了用户对加密货币的拥有权。但是，互联网的环境是一个不安全的网络环境。离线钱包或者冷钱包，就是将私钥与互联网脱离，需要签名的时候使用二维码或者其他的物理形式，讲签名好的交易，广播到互联网的环境中。

所以，最简单的离线钱包形式应该是包含两台电脑，其中一台电脑离线，我们称之为OfflineA，另外一台电脑在线，我们称之为OnlineB。由于XMC包含spend key 和 view key两种类型的私钥，其中view key可以用来查看余额，但是不能花费余额，可以将view key放在OnlineB电脑中。所以，离线钱包的环境设定如下:

OnlineB包括view only钱包，完整的区块同步的节点。

OffineA

对于接收XMC来说，离线钱包和在线钱包没有任何区别，只需要将公钥提供给付款者即可。

XMC编译完成后，会有**moneroclassic-blockchain-export** , **moneroclassic-wallet-cli** , **moneroclassicd** , **moneroclassic-blockchain-import** 和 **moneroclassic-wallet-rpc** 五个可执行文件。

OnlineB电脑需要使用**moneroclassicd **同步一份XMC的区块数据，同步完数据后，使用

