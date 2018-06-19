# XMC多签机制

### 多签钱包的使用

在此以2/3 Multisig为例，即共三个人参加签名，有两个人签名同意，即可使用币。假设有A，B，C三个人

1.使用**./moneroclassic-wallet-cli --testnet **命令打开钱包

2.使用prepare\_multisig命令产生multisig info

> `[wallet 9zSb65]: prepare_multisig`
>
> `Wallet password:`
>
> `MultisigV115Meo3UCxuqfMrt5aUy8Sj18512fHuRn64jH8nT23sMYTv1n6bVNnMqHVmVdPGhdYX3UckDdb8spR9azMBtx3WqBbTgvAe1DU6L4idbCpVGPSvCpxH4pScP3n9WLhzZtCWSb32zexg41ayeQXgFkZnBPy7cvb7ipSXNUNeJMG9utJjFb`
>
> `Send this multisig info to all other participants, then use make_multisig <threshold><info1> [<info2>...] with others' multisig info`
>
> `This includes the PRIVATE view key, so needs to be disclosed only to that multisig wallet's participants`



