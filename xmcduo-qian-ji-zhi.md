# XMC多签机制

### 多签钱包的使用

在此以2/3 Multisig为例，即共三个人参加签名，有两个人签名同意，即可使用币。假设有A,B,C三个人。

1.A,B,C三个人分别使用**./moneroclassic-wallet-cli --testnet **命令打开钱包walletA, walletB, walletC

2.A, B, C三个人分别使用**prepare\_multisig**命令产生walletA, walletB和walletC的multisig info

walletA:

> \[wallet 9uKdar\]: prepare\_multisig
>
> Wallet password:
>
> MultisigV1MLhQU3JTFkkMmcoG1ALeFHJv2oB8XiQAi2Lu48qH7vno1hVStECZUot9NyvbnvCNdM24hz6mwciPSZv91RtjLaopWJHB5J17aWDinWvBXKsyV741GLB7Puy4zZDM3VVpmP88LT38At6vc3XBCcVxu72ZTuexRab2w381s5vgx8Kh6gtq
>
> Send this multisig info to all other participants, then use make\_multisig &lt;threshold&gt; &lt;info1&gt; \[&lt;info2&gt;...\] with others' multisig info
>
> This includes the PRIVATE view key, so needs to be disclosed only to that multisig wallet's participants

walletB:

> \[wallet 9wbQhC\]: prepare\_multisig
>
> Wallet password:
>
> MultisigV1gYCUZQLBQwPhSDuJFDqwF3fzVG3kuF6aPBLFhm1RYn2bMECwHPfjHSn2R4m5GKn1Be5BmrDadHCp5GVNVhgKzNHkj4tkRARsyJm9oYVcKJ71RDDcExFR817SAi8RibPjwfXQj2ee418RqNgNM4eQycmcxLQ6QQ3UGKnwyLAnCcrDS9nn
>
> Send this multisig info to all other participants, then use make\_multisig &lt;threshold&gt; &lt;info1&gt; \[&lt;info2&gt;...\] with others' multisig info
>
> This includes the PRIVATE view key, so needs to be disclosed only to that multisig wallet's participants

walletC:

> \[wallet A2q9oZ\]: prepare\_multisig
>
> Wallet password:
>
> MultisigV1c8XMWmfQYsKdPjNDgzVRYjPcVh7YJonYoXAiyGcmMCqUekyHCvhSNGGhXdwaaTPZXHDkVa99Vh6beUfaRtG4V75sM8HF8avvRWxSpsdKtjHmQTY1YM9GxQYWFRcfuqgP4nsbNToMPmhiqV14htkRAMUoKT7Qrb2LotUbnLBbtCxyhGRN
>
> Send this multisig info to all other participants, then use make\_multisig &lt;threshold&gt; &lt;info1&gt; \[&lt;info2&gt;...\] with others' multisig info
>
> This includes the PRIVATE view key, so needs to be disclosed only to that multisig wallet's participants

3.A,B,C分别使用**make\_multisig 2 &lt;multisig-info&gt; &lt;multisig-info&gt;**命令生成multisig钱包，其中2表示有两个签名即可生效，multisig-info是另外两个人的上一步骤中产生的multisig-info。举例来说，用户A应使用用户B和C提供的mutlisig-info

walletA:

> \[wallet 9uKdar\]: make\_multisig 2 MultisigV1gYCUZQLBQwPhSDuJFDqwF3fzVG3kuF6aPBLFhm1RYn2bMECwHPfjHSn2R4m5GKn1Be5BmrDadHCp5GVNVhgKzNHkj4tkRARsyJm9oYVcKJ71RDDcExFR817SAi8RibPjwfXQj2ee418RqNgNM4eQycmcxLQ6QQ3UGKnwyLAnCcrDS9nn MultisigV1c8XMWmfQYsKdPjNDgzVRYjPcVh7YJonYoXAiyGcmMCqUekyHCvhSNGGhXdwaaTPZXHDkVa99Vh6beUfaRtG4V75sM8HF8avvRWxSpsdKtjHmQTY1YM9GxQYWFRcfuqgP4nsbNToMPmhiqV14htkRAMUoKT7Qrb2LotUbnLBbtCxyhGRN
>
> Wallet password:
>
> Another step is needed
>
> MultisigxV1fSkNJQi4XwWhZhQ1zqh6o5AYveN9G9i1BATZsT969qC2hz15Yg6DRjHZCv6YGwpSqqUFnEpXQeEFaNEzc5RcMpiY3ntw4s7k5RxPMYeQ7EyDPXhSZ7qfgaVWGZTv7pXqTj7F2FhZVRiKFsv6QBLKJ6yf7kTNm7ESG3NjgSPjgdiyqETrgzKeFmV7NaAJ2yNB2WtTWzUUbqMtHg7d8R2u4FxvTMR4
>
> Send this multisig info to all other participants, then use finalize\_multisig &lt;info1&gt; \[&lt;info2&gt;...\] with others' multisig info

walletB:

> \[wallet 9wbQhC\]: make\_multisig 2 MultisigV1MLhQU3JTFkkMmcoG1ALeFHJv2oB8XiQAi2Lu48qH7vno1hVStECZUot9NyvbnvCNdM24hz6mwciPSZv91RtjLaopWJHB5J17aWDinWvBXKsyV741GLB7Puy4zZDM3VVpmP88LT38At6vc3XBCcVxu72ZTuexRab2w381s5vgx8Kh6gtq MultisigV1c8XMWmfQYsKdPjNDgzVRYjPcVh7YJonYoXAiyGcmMCqUekyHCvhSNGGhXdwaaTPZXHDkVa99Vh6beUfaRtG4V75sM8HF8avvRWxSpsdKtjHmQTY1YM9GxQYWFRcfuqgP4nsbNToMPmhiqV14htkRAMUoKT7Qrb2LotUbnLBbtCxyhGRN
>
> Wallet password:
>
> Another step is needed
>
> MultisigxV18VBMJangwAY19jSU25hzazSFEcpaJgANKMkbsPUgxP3qhz15Yg6DRjHZCv6YGwpSqqUFnEpXQeEFaNEzc5RcMpiYAFgFgRrGFfB4cPpc3WrYM1D6Vk2Pxm2QzHz5VMRPaNp9ATGefPUwpiWJYiHg2EThkMcyuPqL3FVxRM4TEeq94nuuL7MADuFZ1dd9aUKvZq2xRTNxV43Z7nfhaZf9J3CXZXK4
>
> Send this multisig info to all other participants, then use finalize\_multisig &lt;info1&gt; \[&lt;info2&gt;...\] with others' multisig info

walletC:

> \[wallet A2q9oZ\]: make\_multisig 2 MultisigV1MLhQU3JTFkkMmcoG1ALeFHJv2oB8XiQAi2Lu48qH7vno1hVStECZUot9NyvbnvCNdM24hz6mwciPSZv91RtjLaopWJHB5J17aWDinWvBXKsyV741GLB7Puy4zZDM3VVpmP88LT38At6vc3XBCcVxu72ZTuexRab2w381s5vgx8Kh6gtq MultisigV1gYCUZQLBQwPhSDuJFDqwF3fzVG3kuF6aPBLFhm1RYn2bMECwHPfjHSn2R4m5GKn1Be5BmrDadHCp5GVNVhgKzNHkj4tkRARsyJm9oYVcKJ71RDDcExFR817SAi8RibPjwfXQj2ee418RqNgNM4eQycmcxLQ6QQ3UGKnwyLAnCcrDS9nn
>
> Wallet password:
>
> Another step is needed
>
> MultisigxV13KscmPnoGs9ZD5aYYLdan3QapbhEwNgrsbpneaPFbkJ23ntw4s7k5RxPMYeQ7EyDPXhSZ7qfgaVWGZTv7pXqTj7FAFgFgRrGFfB4cPpc3WrYM1D6Vk2Pxm2QzHz5VMRPaNp9TaN1MyegJt2Qk2BNtrhdbwPgBvRCKYeDYSe9H2U8sJnQ192t8xumERuQFvrGbbGEWp4TDkGSD1sRqWpn3TMf8REw
>
> Send this multisig info to all other participants, then use finalize\_multisig &lt;info1&gt; \[&lt;info2&gt;...\] with others' multisig info

4.A,B,C分别使用**finalize\_multisig &lt;multisig-info&gt; &lt;multisig-info&gt;**命令

