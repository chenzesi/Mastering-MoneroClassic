# XMC的编译和使用

XMC的代码官方代码地址为:[https://github.com/monero-classic/monero](https://github.com/monero-classic/monero) ,目前的最新版本为[v0.11.1.0](https://github.com/monero-classic/monero/releases/tag/v0.11.1.0)。

## XMC非GUI钱包的编译:

OSX系统的编译, 以OSX 10.13.4为例:

1.安装依赖库: brew install cmake

2.打开monero文件夹: cd monero

3.创建build文件夹: mkdir build

4.打开build文件夹: cd build

5.使用cmake生成makfile等文件: cmake ..

6.编译生成可执行文件: make \(此处可以使用-j参数以增加编译速度，-j表示用来编译的核心数，例如make -j4表示使用四个CPU核心进行编译\)

Ubuntu系统的编译,以ubuntu 16.04为例:

1.安装依赖库: sudo apt install libssl-dev libboost-all-dev cmake

2.开打monero文件夹: cd monero

3.创建build文件夹:mkdir build

4.打开build文件夹: cd build

5.使用cmake生成makefile等文件: cmake ..

6.编译生成可执行文件: make \(此处可以使用-j参数以增加编译速度，-j表示用来编译的核心数，例如make -j4表示使用四个CPU核心进行编译\)

OSX和Ubuntu系统编译成功后，都会生成五个可执行文件，分别是: moneroclassic-blockchain-export，moneroclassic-blockchain-import，moneroclassic-wallet-cli，moneroclassic-wallet-rpc 和 moneroclassicd

Window系统的编译:

## XMC GUI钱包的编译:

OSX系统的编译, 以OSX 10.13.4为例:

1.下载并安装qt5, 现在链接为: [https://download.qt.io/archive/qt/5.10/5.10.1/](https://download.qt.io/archive/qt/5.10/5.10.1/) ，将qt5安装在home路径下

2.配置qt5的路径，将**export PATH=$PATH:$HOME/Qt5.10.1/5.10.1/clang64/bin**_ _添加到**.bash\_profile**的末尾

3.下载GUI钱包源代码，网页链接为:[https://github.com/monero-classic/monero-gui](https://github.com/monero-classic/monero-gui)

4.打开monero-gui文件夹: **cd monero-gui**

5.运行**./build.sh**编译

编译完成后，会在monero-gui/build/release/bin/monero-wallet-gui.app/Contents/MacOS路径下生成可执行文件monero-wallet-gui和monerod

ubuntu系统的编译，以ubuntu16.04为例:

windows系统的编译

## GUI钱包的使用:

![](/assets/gui-wallet1.png)![](/assets/gui-wallet2.png)

