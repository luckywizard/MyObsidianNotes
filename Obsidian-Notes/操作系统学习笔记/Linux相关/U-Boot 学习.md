## 一、U-Boot 简介
### 1.1 U-Boot（Universal Boot Loader）
__Bootloader__ 是在操作系统运行之前执行的一段小程序。通过这段小程序，可以初始化硬件设备、建立内存空间的映射表，从而建立适当的系统软硬件环境，为最终调用操作系统内核做好准备。 
>[!note]- bootloader处理过程
芯片上电以后先运行一段 bootloader 程序。bootloader会先初始化 DDR 等外设，然后将 Linux 内核从flash (NAND，NOR FLASH， SD， MMC 等)拷贝到 DDR 中， 最后启动 Linux 内核。


U-Boot是一种bootloader，由于bootloader是基于特定硬件平台实现的。因此，不同的处理器架构和板卡都有不同的bootloader。uboot 官方的 uboot 源码是给半导体厂商准备的， 半导体厂商会根据自己的芯片进行移植，然后维护一个为其设计的芯片定制的 uboot 版本。这个定制版对自家的芯片支持会很全，虽然 uboot 官网的源码中一般也会支持他们的芯片，但是绝对是没有半导体 厂商自己维护的 uboot 全面。
>[!note] U-Boot源码
>U-Boot官方网址： http://www.denx.de/wiki/U-Boot/
>Xilinx 维护的 uboot 版本： https://github.com/Xilinx/u-boot-xlnx 
其下载地址为： https://github.com/Xilinx/u-boot-xlnx/releases


对于 ZYNQ 而言， 在引导过程中， 先运行 FSBL 来设置 PS，然后运行 U-Boot 用于加载 Linux 内核映像并引导 Linux，所以 uboot 对于 zynq 而言是第二阶段引导程序， FSBL 是第一阶段引导程序。xilinx-v2018.3 当中版本号 2018.3  是 xilinx 自己维护的一个版本号，并不是 U-Boot 官方对应的版本号， xilinx-v2018.3 版本号使用的 U-Boot 官方版本号为 2018.01。 __Xilinx 维护的版本号与我们所使用的 petalinux 版本相对应， 如果不对应可能会出现某些问题。__


uboot 基本支持了 Xilinx 当前所有可以运行 Linux 的芯片，而且支持各种启动方式，比如 EMMC、 NAND、 NOR FLASH 等等，这些都是 uboot 官方所不支持的。如果是我们自己做的板子就需要修改 Xilinx官方的 uboot，使其支持我们自己做的板子。你也可以在购买了第三方开发板以后使用半导体厂商提供的 uboot， 只不过有些外设驱动可能不支持， 需要自己移植， 这个就是我们常说的 uboot 移植。


### 1.2 U-Boot 初次编译
执行如下命令编译 uboot：  
```bash
petalinux-build -c u-boot
```


### 1.3 U-Boot 烧写与启动
uboot 编译好以后就可以烧写到板子上使用了。我们将 u-boot.elf 文件打包到 ZYNQ 的启  
动文件 BOOT.BIN 中，在终端中输入如下命令： 
```bash
petalinux-package --boot --fsbl --fpga --u-boot --force
```
  
生成 BOOT.BIN 文件后， 将该工程 image/linux 目录下的 BOOT.BIN 文件拷贝到 SD 卡的第  
一个分区也即 FAT32 分区。

![[Pasted image 20220625202356.png]]

第 1 行是 uboot 版本号和编译时间，可以看出，当前的 uboot 版本号是 2018.01，编译时  
间是 2020 年 11 月 5 日上午 2 点 5 分。  
第 3~5 行是开发板相关信息，可以看出当前使用的开发板名称为“ Navigator Development  
Board”，核心板为“ Xilinx Zynq” ，核心板的芯片版本为 3.1。  
第 6 行提示 I2C 已经初始化完毕。  
第 7 行提示当前板子的 DRAM（内存）为 1GiB，如果是 7010 的核心板的话内存为 512MiB。  
第 8 和第 9 行提示当前有两个 MMC/SD 卡控制器： mmc@e0100000 和 mmc@e0101000，且  
mmc@e010000 接的是 SD(TF)卡， mmc@e0101000 接的是 eMMC。
第 10 检测到 QSPI--w25q256，大小为 32MB。  
第 11~13 是标准输入、标准输出和标准错误所使用的终端，这里都使用串口(serial)作为  
终端， serial@e0000000 对应的就是开发板的 USB 调试串口。  
第 17~19 行是网口信息，提示我们当前使用的是 eth0 这个网口， ZYNQ 支持两个网口。  
第 24~29 行，开发板 PS 网口正在通过 dhcp 获取 IP 地址。  
第 30 行是倒计时提示，默认倒计时 4 秒，倒计时结束之前按下回车键就会进入 Uboot 命  
令行模式。如果在倒计时结束以后没有按下回车键，那么 Linux 内核就会启动， Linux 内核一  
旦启动， uboot 就会寿终正寝。这个就是 uboot 默认输出信息的含义。  
如果在启动时看到 uboot 打印出：“ Warming-bad CRC， using default environment”，  
说明 uboot 没有在存放环境变量的固态存储器（一般为 Flash） 中找到有效的环境变量，只好  
使用编译时定义的默认环境变量。如果 uboot 存放环境变量的固态存储器的驱动没问题，那么  
只要运行 saveenv 就可以把默认环境变量写入固态存储器，下次启动就不会有这个警告了，当  
然了，也可以忽略该警告。



### 1.4 U-Boot 命令使用
![[Pasted image 20220625202623.png]]



## 二、U-Boot 顶层 Makefile 详解



