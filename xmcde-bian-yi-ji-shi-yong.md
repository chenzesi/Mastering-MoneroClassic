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



OSX和Ubuntu系统编译成功后，都会生成四个可执行文件，分别是:

Window系统的编译:

## XMC GUI钱包的编译:

OSX系统的编译, 以OSX 10.13.4为例:



