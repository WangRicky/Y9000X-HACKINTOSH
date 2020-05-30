# Y9000X-hackintosh

**Y9000X hackintosh 黑苹果 EFI**

目前已更新10.15.5，`opencore`引导版本号0.5.7

CFG LOCK已解锁，本人配置CFG LOCKCFG Lock的offset为0x3E,需要修改SaSetup和CPUSetup中对应值，改完后Hackintool显示CFG Lock已解锁。

可按照[此教程进行操作](http://bbs.pcbeta.com/viewthread-1845189-1-1.html)

**修改BIOS ROM有风险，请谨慎操作**

目前的config.plist是按照CFG LOCK解锁后配置的，如未解锁，请设置`AppleCpuPmCfgLock`和`AppleXcpmCfgLock`为true（之前升级oc到0.5.7的时候这两个选项错误的设置为了`false`,但使用起来确没发现有影响，个人也不清楚具体原因，如有网友知道原理的，请不吝赐教）

**新增ALC声卡驱动延迟加载参数，解决时声卡可能不可用问题**

~~最新版的触控板驱动有问题，导致触控板无法使用，已回退，本机测试可正常使用~~

**已更新最新版触控板驱动，修改了配置文件，现驱动正常**

**`config.plist`中的个人的机器三码信息已删除，需要自己生成后填入**

**将机型改为14,1，雷电转HDMI正常，感谢[@hx2nn](https://github.com/hx2nn)**

~~声卡和雷电转HDMI需要等待BIOS更新，官方论坛已经发起了有关外放和雷电的需求调研，希望大家可以去投票[链接地址](https://club.lenovo.com.cn/thread-5672284-1-1.html)~~


* 按照[黑果小兵](https://blog.daliansky.net/DW1820A_BCM94350ZAE-driver-inserts-the-correct-posture.html)的DW1820A蓝牙教程添加驱动
* 添加了4k显示补丁，显存2048M，原生HiDPI显示
* 加入了DW1820a的device property驱动，可以支持apple watch自动解锁 
* 添加了屏蔽PM981a的patch

**配置** 
* 主板 HM370
* CPU i7-9750H
* 分辨率：4K
* 硬盘：PM981a（黑苹果无解，自行添加了东芝RC500）
* 网卡:intel AX200(黑苹果无解，已更换DW1820A) 

前期准备
---

**更换硬盘**

* pm981a无法安装黑苹果，所以必须更换或增加硬盘。由于有pm981a存在，系统在访问pm981a硬盘文件时会导致死机重启。必须拆下三星的这块硬盘或者屏蔽这块硬盘。本efi默认屏蔽这块硬盘且pm981在第一硬盘位，如果你选择直接拆下这块硬盘，请删除efi/clover/acpi/patched/SSDT-DNVMe.aml文件 。

**更换网卡为dw1820a**

关闭intel VT

关闭secure boot

切换硬盘模式为 AHCI


# 工作

* 4k显示，背光调节正常 
* 耳机，麦克风，摄像头
* wifi 蓝牙 handoff airdrop
* 触控板全手势支持
* 电源管理 USB接口正常
* type-c接口可以正常接U盘，接type-c扩展坞以太网卡、HDMI，DP工作正常

# 不工作

**指纹**

**fn热键**

**扬声器**

* 音频尝试了自制Applealc驱动，扬声器节点为0x17，路径为0x02>0x17，均确认无误，编译的applealc正常驱动，外放无声，网友反馈此机型除Windows外，Linux、macOS系统扬声器均无法正常工作。


