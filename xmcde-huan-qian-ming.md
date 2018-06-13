# XMC的环签名

一般比特币的模型\(UTXO模型\)中，每个交易（transaction or tx）都包含发送地址\(input中的某个地址\)和接收地址（output中的地址）。所以比特币的UTXO模型中的支付是可以被追溯的。cryptonote协议则是使用使用环签名来实现交易的不可追溯功能。环签名，是对于没一笔交易，都存在一个用户组，用户组中的某一个人用私钥签名，即可以用户组的身份发出一笔交易。对于验证交易的人来说，他们只能知道此交易来自某用户组，而无法定位是用户组中的哪个人发起的交易。另外一种常见的匿名交易的方法，混币也是类似的原理，不同之处在于，混币通常需要一个可信任的节点提供混币服务，而环签名并不需要这样一个节点。

组签名（Group Signatures）的概念最早是Chaum, David; van Heyst, Eugene在其1991年的论文《Group signatures》首先提出的。在其论文中，组签名（Group signature）被定义为包含以下三个性质:

1. 只有组里的成员可以签名
2. 接受者可以验证签名是一个合法的环签名但是没有办法发现是哪个组成员对其进行了签名
3. 如果有必要，签名可以被“打开”，签名人可以被揭示出来

组签名的一个缺陷是也需要一个可信的第三方（Group Manager），此第三方唯一可以追溯签名人。Ronald L. Rivest, Adi Shamir 和Yael Tauman 在论文《How to Leak a Secret》中提出了环签名的概念。环签名是组签名（Group Signature）的发展，并且不再需要信任的第三方（Group Manager）完成流程。



参考资料:

[https://cryptonote.org/whitepaper.pdf](https://cryptonote.org/whitepaper.pdf)

[https://chaum.com/publications/Group\_Signatures.pdf](https://chaum.com/publications/Group_Signatures.pdf)

[https://www.iacr.org/archive/asiacrypt2001/22480554.pdf](https://www.iacr.org/archive/asiacrypt2001/22480554.pdf)

