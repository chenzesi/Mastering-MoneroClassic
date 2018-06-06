# XMC实现离线钱包

不管是哪种数字货币，想要实现转账操作，都要使用私钥\(private key\)对交易签名。私钥，确保了用户对加密货币的拥有权。但是，互联网的环境是一个不安全的网络环境。离线钱包或者冷钱包，就是将私钥与互联网脱离，需要签名的时候使用二维码或者其他的物理形式，讲签名好的交易，广播到互联网的环境中。

所以，最简单的离线钱包形式应该是包含两台电脑，其中一台电脑离线，我们称之为OfflineA，另外一台电脑在线，我们称之为OnlineB。由于XMC包含spend key 和 view key两种类型的私钥，其中view key可以用来查看余额，但是不能花费余额，可以将view key放在OnlineB电脑中。XMC编译完成后产生后共有**moneroclassic-blockchain-export** ，**moneroclassic-blockchain-import moneroclassic-wallet-cli ，moneroclassic-wallet-rpc**  和 **moneroclassicd。**所以，离线钱包的环境设定如下:

1.OnlineB包括view only钱包，完整的区块同步的节点（**moneroclassicd** 和**moneroclassic-wallet-cli**）。

2.OffineA包含spend key和view key的钱包（**moneroclassic-wallet-cli**）。

对于接收XMC来说，离线钱包和在线钱包没有任何区别，只需要将公钥提供给付款者即可。

对于使用XMC离线钱包支付的情形:

1.使用**./moneroclassic-wallet-cli --testnet** 命令在OfflineA电脑上创建新的冷钱包

用**address**命令显示address，用**viewkey**命令显示viewkey

> `[wallet 9zRXgy (no daemon)]: address`
>
> `9xALWudHXg4LWRtCzrJv2UVsAGbQ2hNdCRyxTa9cWVySZqyDg2PqjxTeM1vZeKDtdGS1EY5et9sgycyg69A1ToaZB6LQiqi`
>
> `[wallet 9zRXgy (no daemon)]: viewkey`
>
> `Wallet password: ********`
>
> `secret: 45d7ca2be264d65b278f3ac30d2f2f804ae9e60bd716c3ca83561adab79c5405`
>
> `public: 5cfc7f99e19ab8df4593341f299c03957d422693c61526d717df1916d5d84259`

2.在OnlineB电脑上使用./**moneroclassicd --testnet **命令同步一份XMC的区块数据。

3.在OnlineB电脑上使用**./moneroclassic-wallet-cli --testnet --generate-from-view-key viewonlywallet **命令创建只读钱包。输入命令后，会提示填写Standard address和viewkey, 填上文中对应的address和viewkey即可。

4.在OnlineB电脑上使用viewonly钱包的**export\_outputs **命令导出outputs

> `[wallet 9xALWu]: export_outputs outputs`
>
> `Wallet password: ********`
>
> `Outputs exported to outputs`

5.将导出的文件outputs从OnlineB复制到OfflineA的冷钱包工作目录

6.在OfflineA电脑上使用冷钱包的**import\_outputs**命令导入outputs

> `[wallet 9xALWu]: import_outputs outputs`
>
> `287 outputs imported`

7.在OnlineB电脑上使用viewonly钱包的export_key_images 导出key images

4.使用**transfer**命令在只读钱包钱包产生未签名的transaction，结果会被写到unsigned\_monero\_tx

> `[wallet 9xALWu]: transfer 9wd28TGpRBP3vB4Zc8Zgrpfjyp9hjtAHHBoMvCa8KnVZ1ofqAJE5iFYaBvWsnj8QFERJU3DVXrWNwVADMacUwCwCATyLEp8 200`
>
> `Wallet password: ********`
>
> `No payment id is included with this transaction. Is this okay?  (Y/Yes/N/No): Y`
>
> `Sending 200.000000000000.  The transaction fee is 0.028004000000`
>
> `Is this okay?  (Y/Yes/N/No): Y`
>
> `Unsigned transaction(s) successfully written to file: unsigned_monero_tx`

5.讲未签名的交易文件unsigned\_monero\_tx复制到OffinleA电脑中冷钱包的工作目录（使用非联网的方式）

6.在OfflineA电脑中的冷钱包中，使用sign\_transfer对没签名的交易签名，签名后产生文件signed\_monero\_tx:

> `[wallet 9xALWu]: sign_transfer`
>
> `Wallet password: ********`
>
> `Loaded 1 transactions, for 203.695646668577, fee 0.028004000000, sending 200.000000000000 to 9wd28TGpRBP3vB4Zc8Zgrpfjyp9hjtAHHBoMvCa8KnVZ1ofqAJE5iFYaBvWsnj8QFERJU3DVXrWNwVADMacUwCwCATyLEp8, 3.667642668577 change to 9xALWudHXg4LWRtCzrJv2UVsAGbQ2hNdCRyxTa9cWVySZqyDg2PqjxTeM1vZeKDtdGS1EY5et9sgycyg69A1ToaZB6LQiqi, with min ring size 5, no payment ID. 287 outputs to import. Is this okay? (Y/Yes/N/No): Y`
>
> `Transaction successfully signed to file signed_monero_tx, txid cd9679f4c528f140276e9777fa31193da76abdc143f4bbfa06bc0387eec1f028`

7.将OflfineA电脑中的签名后的文件signed\_monero\_tx再复制回OnlineB电脑中的只读钱包的工作目录（使用非联网的方式）

8.在只读钱包，使用**submit\_transfer**命令，提交transaction到网络中

> `[wallet 9xALWu]: submit_transfer`
>
> `Loaded 1 transactions, for 21.609111149840, fee 0.016802400000, sending 20.000000000000 to 9wd28TGpRBP3vB4Zc8Zgrpfjyp9hjtAHHBoMvCa8KnVZ1ofqAJE5iFYaBvWsnj8QFERJU3DVXrWNwVADMacUwCwCATyLEp8, 1.592308749840 change to 9xALWudHXg4LWRtCzrJv2UVsAGbQ2hNdCRyxTa9cWVySZqyDg2PqjxTeM1vZeKDtdGS1EY5et9sgycyg69A1ToaZB6LQiqi, with min ring size 5, no payment ID. 287 key images to import. Is this okay? (Y/Yes/N/No): Y`
>
> `Money successfully sent, transaction: <987db6be2e5a2a2ca60ebed258e431207975c418bd0de74e97351c46d2849753>`



