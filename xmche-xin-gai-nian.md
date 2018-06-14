# XMC的核心概念

#### XMC和XMR的地址（address）

XMC和XMR的地址是95个字符的字符串，主网地址以“4”开头，测试了网络以“9”开头（XMC以后版本可能会修改开头字符，但是目前还是与XMR保持一致），例如:

> `45RJpvvyb39CYpCnGi9cAviywdMmoJkrWe7QCq6aprMzU3qxijZy19LQttRkrsk7Z4hhtq5yZbZYkgTLRZbTSaraEJ53tVB`
>
> `9tAbBhspbCCSB9CRSDaTybaDxBGT1aomYcYkViAVq2HEUM5iVEB1u3PDPCvJCBwXqMTmK6TdZsqgNUqnnPULtAHGPADzXn7`

XMC和XMR地址由四部分组成，第一部分是前缀\(即主网的“4”和测试网络的“9”\)，第二部分是Public Spend Key, 第三部分是Public View Key, 第四部分是Keccac-256 对地址的校验码。

代码中src/cryptonote\_config.h中定义了mainet的CRYPTONOTE\_PUBLIC\_ADDRESS\_BASE58\_PREFIX和testnet的CRYPTONOTE\_PUBLIC\_ADDRESS\_BASE58\_PREFIX两个常量值来表示主网"4"开头的前缀和测试网络"9"开头的前缀。

> `uint64_tconstCRYPTONOTE_PUBLIC_ADDRESS_BASE58_PREFIX =18;`
>
> `uint64_tconstCRYPTONOTE_PUBLIC_INTEGRATED_ADDRESS_BASE58_PREFIX =19;`
>
> `uint64_tconstCRYPTONOTE_PUBLIC_SUBADDRESS_BASE58_PREFIX =42;`



> `uint64_tconstCRYPTONOTE_PUBLIC_ADDRESS_BASE58_PREFIX =53;`
>
> `uint64_tconstCRYPTONOTE_PUBLIC_INTEGRATED_ADDRESS_BASE58_PREFIX =54;`
>
> `uint64_tconstCRYPTONOTE_PUBLIC_SUBADDRESS_BASE58_PREFIX =63;`



