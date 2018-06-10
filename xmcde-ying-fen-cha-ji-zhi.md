# XMC的硬分叉机制

所谓硬分叉即不兼容旧版本客户端的分叉，新版本客户端产生的区块，旧版本的客户端不能确认。硬分叉一般会涉及到修改共识协议，例如修改挖矿算法等等。XMR经常性的硬分叉来添加新特性，修改挖矿算法等等，所以代码有一套硬件分叉的机制。XMC基于XMR的历史版本，同样继承了此分叉机制。

硬分叉设计到的代码主要有:

* src/cryptonote\_basic/hardfork.cpp
* src/cryptonote\_core/blockchain.cpp
* src/cryptonote\_core/cryptonote\_tx\_utils.cpp
* src/blockchain\_db/lmdb/db\_lmdb.cpp

hardfork.cpp中定义了struct mainnet\_hard\_forks和struct testnethardforks, \_struct中包含uint8\_t version，uint64\_t height，uint8\_t threshold，time\_t time和mainnet\_hard\_fork\_version\_1\_till，testnet\_hard\_fork\_version\_1\_till

> `static const struct{`
>
> `uint8_t version;`
>
> `uint64_t height;`
>
> `uint8_t threshold;`
>
> `time_t time;`
>
> `}`

其中version表示分叉版本，height表示分叉高度，threshold目前全部设置为0，time表示分叉版本发布时间。mainethard\_fork\_version\_1\_till和testnet\_hard\_fork\_version\_1\_till表示版本1分叉的高度的上一个高度（分叉高度减一）。

#### HardFork 初始化

blockchain.cpp 中init初始化了HardFork，并且添加各个hard fork版本的信息。

> `for (size_t n = 0; n < sizeof(mainnet_hard_forks) / sizeof(mainnet_hard_forks[0]); ++n)`
>
> `m_hardfork->add_fork(mainnet_hard_forks[n].version, mainnet_hard_forks[n].height, mainnet_hard_forks[n].threshold, mainnet_hard_forks[n].time);`

除添加上述版本信息外，init function中还会调用HardFork类的init function. hardfork.h中定义了

> `uint32_t current_fork_index;`

用来跟踪最新的hardfork的index

XMC使用了lmdb作为database， 其中跟hardfork相关的数据，记录了每个高度对应的分叉版本，所以可以使用

> `uint8_t BlockchainLMDB::get_hard_fork_version(uint64_t height)const`

来获得某个已有高度的block对应的分叉版本信息

#### HardFork state

src/cryptonotebasic/hardfork.h中定义了两个时间的成员变量time\_t forked\_time 和 time\_t update\_time，其默认值分别是

> `static const time_t DEFAULT_FORKED_TIME =31557600;// a year in seconds`
>
> `static const time_t DEFAULT_UPDATE_TIME =31557600/2;`

此两个变量会用来产生hardfork state，state产生方法如下代码所示，

> `HardFork::State HardFork::get_state(time_t t)const`
>
> `{`
>
> `CRITICAL_REGION_LOCAL(lock);`
>
> `// no hard forks setup yet`
>
> `if(heights.size() <=1)`
>
> `returnReady;`
>
> `time_t t_last_fork = heights.back().time;`
>
> `if(t >= t_last_fork + forked_time)`
>
> `returnLikelyForked;`
>
> `if(t >= t_last_fork + update_time)`
>
> `returnUpdateNeeded;`
>
> `returnReady;`
>
> `}`
>
> `HardFork::State HardFork::get_state()const`
>
> `{`
>
> `returnget_state(time(NULL));`
>
> `}`

钱包启动时，会检查state信息，如果是LikelyForked或者UpdateNeeded状态，会显示出提示信息。

> `*****************************************************************`
>
> `2018-06-10 03:50:33.156    [P2P1]    WARN     global    src/cryptonote_core/cryptonote_core.cpp:1380    Last scheduled hard fork time shows a daemon update is needed soon.`
>
> `2018-06-10 03:50:33.156    [P2P1]    WARN     global    src/cryptonote_core/cryptonote_core.cpp:1381    **********************************************************************`



