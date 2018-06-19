# XMC多签机制

### 多签钱包的使用

在此以2/3 Multisig为例，即共三个人参加签名，有两个人签名同意，即可使用币。假设有A,B,C三个人。

1.A,B,C三个人分别使用**./moneroclassic-wallet-cli --testnet **命令打开钱包walletA, walletB, walletC

2.A, B, C三个人分别使用**prepare\_multisig**命令产生multisig info

A:

> `[wallet 9ydm81]: prepare_multisig`
>
> `Wallet password:`
>
> `MultisigV15Ayhc5PkhRzet4U7JkFxoaJBiRJxejQhoWsakmsh8Gevhoo8EvhEKu226tsj5cNbvmUJG5wA9AV4rAXAkb1bFj7e6FVPzi6caEoDLMYo472Lg7gRBqnrCwvXjGmErtJniBa7DVZ21JhJAFjbK2X8GqvQW59N7YHcbNNFJSLzT9bxp6rp`
>
> `Send this multisig info to all other participants, then use make_multisig <threshold> <info1> [<info2>...] with others' multisig info`
>
> `This includes the PRIVATE view key, so needs to be disclosed only to that multisig wallet's participants`

B:

> `[wallet 9ydm81]: prepare_multisig`
>
> `Wallet password:`
>
> `MultisigV15Ayhc5PkhRzet4U7JkFxoaJBiRJxejQhoWsakmsh8Gevhoo8EvhEKu226tsj5cNbvmUJG5wA9AV4rAXAkb1bFj7ebf9ytkH16pg65bEumtCKifJnTFbBALEEEPQNYwtgMp5JiHMdyUnP6p9HgVVWd5gJAhPEBs6kmqMZHYh6dQ8Snvg6`
>
> `Send this multisig info to all other participants, then use make_multisig <threshold> <info1> [<info2>...] with others' multisig info`
>
> `This includes the PRIVATE view key, so needs to be disclosed only to that multisig wallet's participants`

C:

> `[wallet 9ydm81]: prepare_multisig`
>
> `Wallet password:`
>
> `MultisigV15Ayhc5PkhRzet4U7JkFxoaJBiRJxejQhoWsakmsh8Gevhoo8EvhEKu226tsj5cNbvmUJG5wA9AV4rAXAkb1bFj7eRXmRLgbUybjbn1RKn5drSbY3wwkWU2SKii79yyKmMmpHJeniVpfRKWoGmY6PPqv4tq5VA9ZVNvmBdJe9bfakHyba`
>
> `Send this multisig info to all other participants, then use make_multisig <threshold> <info1> [<info2>...] with others' multisig info`
>
> `This includes the PRIVATE view key, so needs to be disclosed only to that multisig wallet's participants`

3.

