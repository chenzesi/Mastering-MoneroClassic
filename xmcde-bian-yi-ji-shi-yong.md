# XMC的编译和使用

XMC的代码官方代码地址为:[https://github.com/monero-classic/monero](https://github.com/monero-classic/monero) ,目前的最新版本为[v0.11.1.0](https://github.com/monero-classic/monero/releases/tag/v0.11.1.0)。

## XMC非GUI钱包的编译:

OSX系统的编译, 以OSX 10.13.4为例:

1.安装依赖库: brew install cmake jmuncaster/header-only/cppzmq

2.打开monero文件夹: cd monero

3.创建build文件夹: mkdir build

4.打开build文件夹: cd build

5.使用cmake生成makfile等文件: cmake ..

6.编译生成可执行文件: make \(此处可以使用-j参数以增加编译速度，-j表示用来编译的核心数，例如make -j4表示使用四个CPU核心进行编译\)

Ubuntu系统的编译,以ubuntu 16.04为例:

1.安装依赖库: sudo apt install libssl-dev libboost-all-dev cmake libzmq3-dev

2.开打monero文件夹: cd monero

3.创建build文件夹:mkdir build

4.打开build文件夹: cd build

5.使用cmake生成makefile等文件: cmake ..

6.编译生成可执行文件: make \(此处可以使用-j参数以增加编译速度，-j表示用来编译的核心数，例如make -j4表示使用四个CPU核心进行编译\)

OSX和Ubuntu系统编译成功后，都会生成五个可执行文件，分别是: moneroclassic-blockchain-export，moneroclassic-blockchain-import，moneroclassic-wallet-cli，moneroclassic-wallet-rpc 和 moneroclassicd

Window系统的编译:

1.下载并安装MSYS2 environment 下载链接: [http://repo.msys2.org/distrib/x86\_64/msys2-x86\_64-20180531.exe](http://repo.msys2.org/distrib/x86_64/msys2-x86_64-20180531.exe)

2.

## XMC GUI钱包的编译:

OSX系统的编译, 以OSX 10.13.4为例:

1.下载并安装qt5, 下载链接为: [https://download.qt.io/archive/qt/5.10/5.10.1/](https://download.qt.io/archive/qt/5.10/5.10.1/) ，将qt5安装在home路径下

2.配置qt5的路径，将**export PATH=$PATH:$HOME/Qt5.10.1/5.10.1/clang64/bin**_ _添加到**.bash\_profile**的末尾

3.下载GUI钱包源代码，网页链接为:[https://github.com/monero-classic/monero-gui](https://github.com/monero-classic/monero-gui)

4.打开monero-gui文件夹: **cd monero-gui**

5.运行**./build.sh**编译

编译完成后，会在monero-gui/build/release/bin/monero-wallet-gui.app/Contents/MacOS路径下生成可执行文件**monero-wallet-gui**和**monerod**

常见问题

如果使用boost1.67.0\_1可能会出现以下error:

> `/Users/xiaobin/code/monero-gui/monero/contrib/epee/include/syncobj.h:37:10: fatal error:`
>
> `'boost/thread/v2/thread.hpp' file not found`

解决方法是将/usr/local/Cellar/boost/1.67.0\_1/include/boost/thread目录中的thread.hpp复制到/usr/local/Cellar/boost/1.67.0\_1/include/boost/thread/v2文件夹下:

> `cp /usr/local/Cellar/boost/1.67.0_1/include/boost/thread/thread.hpp /usr/local/Cellar/boost/1.67.0_1/include/boost/thread/v2`

ubuntu系统的编译

1.下载并安装qt5, 下载链接为: [https://download.qt.io/archive/qt/5.10/5.10.1/](https://download.qt.io/archive/qt/5.10/5.10.1/)，将qt5安装在默认路径下

2.配置qt5的路径，将**export PATH=$PATH:$HOME/Qt5.10.1/5.10.1/gcc\_64/bin**_ _添加到**.bashrc**的末尾

3.**source .bashrc**

4.安装依赖包**sudo apt install libreadline-dev libgl-dev**

5.运行**./build.sh**编译

windows系统的编译

