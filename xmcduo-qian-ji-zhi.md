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

4.A,B,C分别使用**finalize\_multisig &lt;multisig-info&gt; &lt;multisig-info&gt;**命令Finalize Multisig, 其中multisig-info是上一步骤中，另外两个人产生的multisig-info。例如用户A应使用B和C在上一步中产生的multisig-info。

walletA:

> \[wallet 9sCrDe \(out of sync\)\]: finalize\_multisig MultisigxV18VBMJangwAY19jSU25hzazSFEcpaJgANKMkbsPUgxP3qhz15Yg6DRjHZCv6YGwpSqqUFnEpXQeEFaNEzc5RcMpiYAFgFgRrGFfB4cPpc3WrYM1D6Vk2Pxm2QzHz5VMRPaNp9ATGefPUwpiWJYiHg2EThkMcyuPqL3FVxRM4TEeq94nuuL7MADuFZ1dd9aUKvZq2xRTNxV43Z7nfhaZf9J3CXZXK4 MultisigxV13KscmPnoGs9ZD5aYYLdan3QapbhEwNgrsbpneaPFbkJ23ntw4s7k5RxPMYeQ7EyDPXhSZ7qfgaVWGZTv7pXqTj7FAFgFgRrGFfB4cPpc3WrYM1D6Vk2Pxm2QzHz5VMRPaNp9TaN1MyegJt2Qk2BNtrhdbwPgBvRCKYeDYSe9H2U8sJnQ192t8xumERuQFvrGbbGEWp4TDkGSD1sRqWpn3TMf8REw

walletB:

> \[wallet 9sCrDe \(out of sync\)\]: finalize\_multisig MultisigxV1fSkNJQi4XwWhZhQ1zqh6o5AYveN9G9i1BATZsT969qC2hz15Yg6DRjHZCv6YGwpSqqUFnEpXQeEFaNEzc5RcMpiY3ntw4s7k5RxPMYeQ7EyDPXhSZ7qfgaVWGZTv7pXqTj7F2FhZVRiKFsv6QBLKJ6yf7kTNm7ESG3NjgSPjgdiyqETrgzKeFmV7NaAJ2yNB2WtTWzUUbqMtHg7d8R2u4FxvTMR4 MultisigxV13KscmPnoGs9ZD5aYYLdan3QapbhEwNgrsbpneaPFbkJ23ntw4s7k5RxPMYeQ7EyDPXhSZ7qfgaVWGZTv7pXqTj7FAFgFgRrGFfB4cPpc3WrYM1D6Vk2Pxm2QzHz5VMRPaNp9TaN1MyegJt2Qk2BNtrhdbwPgBvRCKYeDYSe9H2U8sJnQ192t8xumERuQFvrGbbGEWp4TDkGSD1sRqWpn3TMf8REw

walletC:

> \[wallet 9sCrDe \(out of sync\)\]: finalize\_multisig MultisigxV1fSkNJQi4XwWhZhQ1zqh6o5AYveN9G9i1BATZsT969qC2hz15Yg6DRjHZCv6YGwpSqqUFnEpXQeEFaNEzc5RcMpiY3ntw4s7k5RxPMYeQ7EyDPXhSZ7qfgaVWGZTv7pXqTj7F2FhZVRiKFsv6QBLKJ6yf7kTNm7ESG3NjgSPjgdiyqETrgzKeFmV7NaAJ2yNB2WtTWzUUbqMtHg7d8R2u4FxvTMR4 MultisigxV18VBMJangwAY19jSU25hzazSFEcpaJgANKMkbsPUgxP3qhz15Yg6DRjHZCv6YGwpSqqUFnEpXQeEFaNEzc5RcMpiYAFgFgRrGFfB4cPpc3WrYM1D6Vk2Pxm2QzHz5VMRPaNp9ATGefPUwpiWJYiHg2EThkMcyuPqL3FVxRM4TEeq94nuuL7MADuFZ1dd9aUKvZq2xRTNxV43Z7nfhaZf9J3CXZXK4

5.经过上述步骤后，使用**address**命令查看地址，三个钱包的地址应该是一样的。

walletA:

> \[wallet 9zwR2b\]: address
>
> 0  9zwR2bm7xasETDL7ed5PXjUP1T5zBzSzhKVSrcjb8oxNNxbTEnwNNHodAo3WiHZWDNBdgQxJaYbhTMhrfVs7a5QbDPzCbQE  Primary address

walletB:

> \[wallet 9zwR2b\]: address
>
> 0  9zwR2bm7xasETDL7ed5PXjUP1T5zBzSzhKVSrcjb8oxNNxbTEnwNNHodAo3WiHZWDNBdgQxJaYbhTMhrfVs7a5QbDPzCbQE  Primary address

walletC:

> \[wallet 9zwR2b\]: address
>
> 0  9zwR2bm7xasETDL7ed5PXjUP1T5zBzSzhKVSrcjb8oxNNxbTEnwNNHodAo3WiHZWDNBdgQxJaYbhTMhrfVs7a5QbDPzCbQE  Primary address

经过上述步骤后，产生的多签地址即可用来正常接收XMC

下面是从多签地址转出币的步骤：

1.因为上述钱包只要有两个人签名即可转出，我们假设使用钱包A和钱包B，使用**export\_multisig\_info filename**命令（filename可以是任何名字）导出multisig info

walletA:

> \[wallet 9zwR2b\]: export\_multisig\_info infoA
>
> Wallet password:
>
> Multisig info exported to infoA

walletB:

> \[wallet 9zwR2b\]: export\_multisig\_info infoB
>
> Wallet password:
>
> Multisig info exported to infoB

walletC:

> \[wallet 9zwR2b\]: export\_multisig\_info infoC
>
> Wallet password:
>
> Multisig info exported to infoC

2.假设使用walletA来操作转账流程，B和C将上一步中产生的infoB和infoC发给A，A使用** import\_multisig\_info infoB infoC**命令导入multisig info

3.A使用**transfer**命令发起转账交易

walletA:

> \[wallet 9zwR2b\]: transfer 9tCVYpdfe461LV2gya6A1u7cUQjchvcomX1qdqdRSJRb7qiNfF9nrKHein74mUasusfboTJ5Z2qhYCsZhmMNmqKyEdfqbsu 100
>
> Wallet password:
>
> No payment id is included with this transaction. Is this okay?  \(Y/Yes/N/No\): Y
>
> Transaction 1/1:
>
> Spending from address index 0
>
> Sending 100.000000000000.  The transaction fee is 0.005848290000
>
> Is this okay?  \(Y/Yes/N/No\): Y
>
> Unsigned transaction\(s\) successfully written to file: multisig\_monero\_tx

4.A将上一步产生的multisig\_monero_\__tx文件发给B签名，在walletB中使用**sign\_multisig multisig\_monero\_tx**命令

walletB:

> \[wallet 9zwR2b\]: sign\_multisig multisig\_monero\_tx
>
> Wallet password:
>
> Loaded 1 transactions, for 102.356449303959, fee 0.005848290000, sending 100.000000000000 to 9tCVYpdfe461LV2gya6A1u7cUQjchvcomX1qdqdRSJRb7qiNfF9nrKHein74mUasusfboTJ5Z2qhYCsZhmMNmqKyEdfqbsu, 2.350601013959 change to 9zwR2bm7xasETDL7ed5PXjUP1T5zBzSzhKVSrcjb8oxNNxbTEnwNNHodAo3WiHZWDNBdgQxJaYbhTMhrfVs7a5QbDPzCbQE, with min ring size 7, no payment ID. Is this okay? \(Y/Yes/N/No\): Y
>
> Transaction successfully signed to file multisig\_monero\_tx, txid bc8129bc784fc9c9531af2310fbaf78c9bc741c96bd08dcb219849b0212d7677
>
> It may be relayed to the network with submit\_multisig

5.B在上一步签名后得到multisig\_monero\_tx文件后，即可使用**submit\_multisig multisig\_monero\_tx**命令提交transaction

walletB:

> \[wallet 9zwR2b \(out of sync\)\]: submit\_multisig multisig\_monero\_tx
>
> Wallet password:
>
> Loaded 1 transactions, for 102.356449303959, fee 0.005848290000, sending 100.000000000000 to 9tCVYpdfe461LV2gya6A1u7cUQjchvcomX1qdqdRSJRb7qiNfF9nrKHein74mUasusfboTJ5Z2qhYCsZhmMNmqKyEdfqbsu, 2.350601013959 change to 9zwR2bm7xasETDL7ed5PXjUP1T5zBzSzhKVSrcjb8oxNNxbTEnwNNHodAo3WiHZWDNBdgQxJaYbhTMhrfVs7a5QbDPzCbQE, with min ring size 7, no payment ID. Is this okay? \(Y/Yes/N/No\): Y
>
> Transaction successfully submitted, transaction &lt;bc8129bc784fc9c9531af2310fbaf78c9bc741c96bd08dcb219849b0212d7677&gt;
>
> You can check its status by using the \`show\_transfers\` command.



