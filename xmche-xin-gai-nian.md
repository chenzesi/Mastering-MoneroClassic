# XMC的核心概念

#### XMC和XMR的地址（address）

XMC和XMR的地址是95个字符的字符串，主网地址以“4”开头，测试了网络以“9”开头（XMC以后版本可能会修改开头字符，但是目前还是与XMR保持一致），例如:

> `45RJpvvyb39CYpCnGi9cAviywdMmoJkrWe7QCq6aprMzU3qxijZy19LQttRkrsk7Z4hhtq5yZbZYkgTLRZbTSaraEJ53tVB`
>
> `9tAbBhspbCCSB9CRSDaTybaDxBGT1aomYcYkViAVq2HEUM5iVEB1u3PDPCvJCBwXqMTmK6TdZsqgNUqnnPULtAHGPADzXn7`

代码中src/cryptonote\_config.h中定义了CRYPTONOTE\_PUBLIC\_ADDRESS\_BASE58\_PREFIX和CRYPTONOTE\_PUBLIC\_INTEGRATED\_ADDRESS\_BASE58\_PREFIX两个常量值来表示主网4开头的前缀和测试网络9开头的前缀。



