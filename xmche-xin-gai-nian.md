# XMC的核心概念

#### XMC和XMR的地址（address）

XMC和XMR的地址是95个字符的字符串（base58编码），主网地址以“4”开头，测试了网络以“9”开头（XMC以后版本可能会修改开头字符，但是目前还是与XMR保持一致），例如:

> `45RJpvvyb39CYpCnGi9cAviywdMmoJkrWe7QCq6aprMzU3qxijZy19LQttRkrsk7Z4hhtq5yZbZYkgTLRZbTSaraEJ53tVB`
>
> `9tAbBhspbCCSB9CRSDaTybaDxBGT1aomYcYkViAVq2HEUM5iVEB1u3PDPCvJCBwXqMTmK6TdZsqgNUqnnPULtAHGPADzXn7`

XMC和XMR地址由四部分组成，第一部分是前缀\(即主网的“4”和测试网络的“9”\)，第二部分是Public Spend Key, 第三部分是Public View Key, 第四部分是Keccac-256 对地址的校验码。

代码中src/cryptonote\_config.h中定义了mainet的CRYPTONOTE\_PUBLIC\_ADDRESS\_BASE58\_PREFIX和testnet的CRYPTONOTE\_PUBLIC\_ADDRESS\_BASE58\_PREFIX两个常量值来表示主网"4"开头的前缀和测试网络"9"开头的前缀。

> `uint64_t const CRYPTONOTE_PUBLIC_ADDRESS_BASE58_PREFIX =18;`
>
> `uint64_t const CRYPTONOTE_PUBLIC_INTEGRATED_ADDRESS_BASE58_PREFIX =19;`
>
> `uint64_t const CRYPTONOTE_PUBLIC_SUBADDRESS_BASE58_PREFIX =42;`

如上代码所示，主网`CRYPTONOTE_PUBLIC_ADDRESS_BASE58_PREFIX`被设置成常量18。此处使用了Varint压缩算法对前缀进行处理。Varint压缩算法是用一个或者多个字节来表示数字的方法，当表示的数字值比较小的数字占大多数时，能有效节省存储空间。Varint中的每个byte都有一个有特殊意义的最高有效位MSB（Most Signaficant Bit \)。当MSB被设置成1时表示后续的一个byte仍然是这个数字的一部分。除MSB外剩下的7bit以二进制补码的方式表示，每7bit可以看成一组，组之间是低位在前的顺序。



参考资料:

[https://stackoverflow.com/questions/24614553/why-is-varint-an-efficient-data-representation](https://stackoverflow.com/questions/24614553/why-is-varint-an-efficient-data-representationhttps://www.cnblogs.com/smark/archive/2012/05/03/2480034.html)

[https://www.cnblogs.com/smark/archive/2012/05/03/2480034.html](https://stackoverflow.com/questions/24614553/why-is-varint-an-efficient-data-representationhttps://www.cnblogs.com/smark/archive/2012/05/03/2480034.html)

