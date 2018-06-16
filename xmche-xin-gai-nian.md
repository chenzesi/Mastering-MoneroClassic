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

如上代码所示，主网`CRYPTONOTE_PUBLIC_ADDRESS_BASE58_PREFIX`被设置成常量18，

  
p.p1 {margin: 0.0px 0.0px 0.0px 0.0px; line-height: 15.0px; font: 12.0px Menlo; color: \#808080; -webkit-text-stroke: \#222222; background-color: \#2b2b2b}  
p.p2 {margin: 0.0px 0.0px 0.0px 0.0px; line-height: 15.0px; font: 12.0px Menlo; color: \#cc7831; -webkit-text-stroke: \#222222; background-color: \#2b2b2b}  
p.p3 {margin: 0.0px 0.0px 0.0px 0.0px; line-height: 15.0px; font: 12.0px Menlo; color: \#a9b7c6; -webkit-text-stroke: \#222222; background-color: \#2b2b2b}  
p.p4 {margin: 0.0px 0.0px 0.0px 0.0px; line-height: 15.0px; font: 12.0px Menlo; color: \#a9b7c6; -webkit-text-stroke: \#222222; background-color: \#2b2b2b; min-height: 14.0px}  
span.s1 {font-kerning: none}  
span.s2 {font-kerning: none; color: \#a9b7c6}  
span.s3 {font-kerning: none; color: \#cc7831}  
span.s4 {font-kerning: none; color: \#808080}  
span.s5 {font-kerning: none; color: \#6897bb}  
span.Apple-tab-span {white-space:pre}  


/\*! \brief writes a varint to a stream.

\*/

**template**&lt;**typename**OutputIt, **typename**T&gt;

/\* Requires T to be both an integral type and unsigned, should be a compile error if it is not \*/

**typename**std::enable\_if&lt;std::is\_integral&lt;T&gt;::value && std::is\_unsigned&lt;T&gt;::value, **void**&gt;::type

write\_varint\(OutputIt &&dest,T i\) {

/\* Make sure that there is one after this \*/

**while**\(i &gt;=0x80\) {

 \*dest = \(**static\_cast**&lt;**char**&gt;\(i\) &0x7f\) \|0x80;

++dest;

i &gt;&gt;=7;/\* I should be in multiples of 7, this should just get the next part \*/

}

/\* writes the last one to dest \*/

\*dest =**static\_cast**&lt;**char**&gt;\(i\);

dest++;/\* Seems kinda pointless... \*/

}

/\*! \brief Returns the string that represents the varint

\*/

**template**&lt;**typename**T&gt;

 std::string get\_varint\_data\(**const**T& v\)

 {

 std::stringstream ss;

write\_varint\(std::ostreambuf\_iterator&lt;**char**&gt;\(ss\),v\);

**return**ss.str\(\);

}

LLLLLLLLLLLLLLL

> `uint64_t const CRYPTONOTE_PUBLIC_ADDRESS_BASE58_PREFIX =53;`
>
> `uint64_t const CRYPTONOTE_PUBLIC_INTEGRATED_ADDRESS_BASE58_PREFIX =54;`
>
> `uint64_t const CRYPTONOTE_PUBLIC_SUBADDRESS_BASE58_PREFIX =63;`



