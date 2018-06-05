# XMC实现离线钱包

不管是哪种数字货币，想要实现转账操作，都要使用私钥\(private key\)对交易签名。私钥，确保了用户对加密货币的拥有权。但是，互联网的环境是一个不安全的网络环境。离线钱包或者冷钱包，就是将私钥与互联网脱离，需要签名的时候使用二维码或者其他的物理形式，讲签名好的交易，广播到互联网的环境中。

所以，最简单的离线钱包形式应该是包含两台电脑，其中一台电脑离线，我们称之为OfflineA，另外一台电脑在线，我们称之为OnlineB。由于XMC包含spend key 和 view key两种类型的私钥，其中view key可以用来查看余额，但是不能花费余额，可以将view key放在OnlineB电脑中。XMC编译完成后产生后共有**moneroclassic-blockchain-export** ，**moneroclassic-blockchain-import moneroclassic-wallet-cli ，moneroclassic-wallet-rpc**  和 **moneroclassicd。**所以，离线钱包的环境设定如下:

1.OnlineB包括view only钱包，完整的区块同步的节点（**moneroclassicd** 和**moneroclassic-wallet-cli**）。

2.OffineA包含spend key和view key的钱包（**moneroclassic-wallet-cli**）。

对于接收XMC来说，离线钱包和在线钱包没有任何区别，只需要将公钥提供给付款者即可。

OnlineB电脑需要使用**moneroclassicd **同步一份XMC的区块数据，同步完数据后，使用

./monero-wallet-cli --testnet --generate-from-view-key 45d7ca2be264d65b278f3ac30d2f2f804ae9e60bd716c3ca83561adab79c5405







**\[wallet 9xALWu\]: viewkey**

**Wallet password: \*\*\*\*\*\*\*\***

**secret: 45d7ca2be264d65b278f3ac30d2f2f804ae9e60bd716c3ca83561adab79c5405**

**public: 5cfc7f99e19ab8df4593341f299c03957d422693c61526d717df1916d5d84259**

**\[wallet 9xALWu\]: address**

**9xALWudHXg4LWRtCzrJv2UVsAGbQ2hNdCRyxTa9cWVySZqyDg2PqjxTeM1vZeKDtdGS1EY5et9sgycyg69A1ToaZB6LQiqi**

