# XMC的核心概念

#### XMC和XMR的地址（address）

XMC和XMR的地址是95个字符的字符串（base58编码），主网地址以“4”开头，测试了网络以“9”开头（XMC以后版本可能会修改开头字符，但是目前还是与XMR保持一致），例如:

> `45RJpvvyb39CYpCnGi9cAviywdMmoJkrWe7QCq6aprMzU3qxijZy19LQttRkrsk7Z4hhtq5yZbZYkgTLRZbTSaraEJ53tVB`
>
> `9tAbBhspbCCSB9CRSDaTybaDxBGT1aomYcYkViAVq2HEUM5iVEB1u3PDPCvJCBwXqMTmK6TdZsqgNUqnnPULtAHGPADzXn7`

XMC和XMR地址由四部分组成，第一部分是前缀\(即主网的“4”和测试网络的“9”，大小为1byte\)，第二部分是Public Spend Key \(32 byte\), 第三部分是Public View Key \(32 byte\), 第四部分是用Keccac-256 对地址\( 1 byte 前缀+ 32 byte Public Spend Key+ 32 byte Public View Key\)的Hash后，Hash值的前4 byte值。最后此69 byte经过base58后，得到95个字符的地址字符串。

XMC和XMR中使用的Base58算法实现也与Bitcoin有所不同。Bitcoin中的Base58 encoding是将所有的data都转成Integer, 然后再去除以58，以转换成base58编码。这样处理的以一个问题是如果data比较大，转换成的Integer就会非常大，可能会需要BigInteger的特殊处理，并且会降低处理速度。XMC和XMR中，是将data分成8 byte的block分别进行处理，这样就避免了转化成BigInteger后造成的问题。上文提到XMC和XMR地址是69 byte data, 分成8 byte的block处理后，可以得到8个block 和剩余 5 byte数据。 每个8 byte的block都会被转成11个字符的base58字符串（如果少于11个会用base58编码后的1进行padding），剩余的5 byte数据会被转成7个字符的base58字符串（如果少于7个也会用base58的1 padding\)，最后可以得到base58编码后的地址，即8 \* 11 + 7 = 95 个字符的地址字符串。以下是XMC base58 encode的代码。

> ```cpp
> std::string encode(conststd::string& data)
> {
>     `if(data.empty())`
>         `return std::string();`
>     `size_t full_block_count = data.size() / full_block_size;`
>     `size_t last_block_size = data.size() % full_block_size;`
>     `size_t res_size = full_block_count * full_encoded_block_size + encoded_block_sizes[last_block_size];`
>     `std::string res(res_size,alphabet[0]);`
>     `for(size_t i =0;i < full_block_count;++i)`
>     `{`
>         `encode_block(data.data() + i * full_block_size,full_block_size,&res[i * full_encoded_block_size]);`
>     `}`
>     `if(0< last_block_size)`
>     `{`
>         `encode_block(data.data() + full_block_count * full_block_size,last_block_size,&res[full_block_count * full_encoded_block_size]);`
>     `}`
>     `return res;`
> }
> ```

代码中src/cryptonote\_config.h中定义了mainet的CRYPTONOTE\_PUBLIC\_ADDRESS\_BASE58\_PREFIX和testnet的CRYPTONOTE\_PUBLIC\_ADDRESS\_BASE58\_PREFIX两个常量值来表示主网"4"开头的前缀和测试网络"9"开头的前缀。

> `uint64_t const CRYPTONOTE_PUBLIC_ADDRESS_BASE58_PREFIX =18;`
>
> `uint64_t const CRYPTONOTE_PUBLIC_INTEGRATED_ADDRESS_BASE58_PREFIX =19;`
>
> `uint64_t const CRYPTONOTE_PUBLIC_SUBADDRESS_BASE58_PREFIX =42;`

如上代码所示，主网`CRYPTONOTE_PUBLIC_ADDRESS_BASE58_PREFIX`被设置成uint64\_t类型常量18。此处使用了Varint压缩算法对前缀进行处理。Varint压缩算法是用一个或者多个字节来表示数字的方法，当表示的数字值比较小的数字占大多数时，能有效节省存储空间。Varint中的每个byte都有一个有特殊意义的最高有效位MSB（Most Signaficant Bit \)。当MSB被设置成1时表示后续的一个byte仍然是这个数字的一部分。除MSB外剩下的7bit以二进制补码的方式表示，每7bit可以看成一组，组之间是低位在前的顺序。在XMC和XMR中，前缀数值都比较小，经过处理后只是将前缀压缩到1byte表示。

#### Integrated address和Payment ID

Payment ID是8 byte长度的交易额外信息，Payment ID被嵌入进XMC和XMR地址中，生成的地址即所谓的Integrated address，Integrated address的生成与普通address类似，只是在原有1 byte PREFIX+ 32 byte Public Spend Key+ 32 byte Public View key 基础上再加上8 byte Payment ID，即最后的地址为1 byte PREFIX+ 32 byte Public Spend Key+ 32 byte Public View key + 8 byte Payment ID + 4 byte  checksum = 77 byte

#### Stealth Address

####  

参考资料:

[https://stackoverflow.com/questions/24614553/why-is-varint-an-efficient-data-representation](https://stackoverflow.com/questions/24614553/why-is-varint-an-efficient-data-representationhttps://www.cnblogs.com/smark/archive/2012/05/03/2480034.html)

[https://monero.stackexchange.com/questions/6049/why-monero-address-is-converted-to-base-58-in-blocks-instead-of-all-at-once/6052\#6052](https://monero.stackexchange.com/questions/6049/why-monero-address-is-converted-to-base-58-in-blocks-instead-of-all-at-once/6052#6052)

[https://www.cnblogs.com/smark/archive/2012/05/03/2480034.html](https://stackoverflow.com/questions/24614553/why-is-varint-an-efficient-data-representationhttps://www.cnblogs.com/smark/archive/2012/05/03/2480034.html)

[https://xmr.llcoins.net/addresstests.html](https://xmr.llcoins.net/addresstests.html)

