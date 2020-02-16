# Y9000X-hackintosh

**Y9000X hackintosh 黑苹果 EFI**

目前已更换`opencore`引导,版本号0.5.3，支持10.15.3

**`config.plist`中的个人的机器三码信息已删除，需要自己生成后填入**

**将机型改为14,1，雷电转HDMI正常，感谢[@hx2nn](https://github.com/hx2nn)**

声卡和雷电转HDMI需要等待BIOS更新，官方论坛已经发起了有关外放和雷电的需求调研，希望大家可以去投票[链接地址](https://club.lenovo.com.cn/thread-5672284-1-1.html)

* 按照[黑果小兵](https://blog.daliansky.net/DW1820A_BCM94350ZAE-driver-inserts-the-correct-posture.html)的DW1820A蓝牙教程添加驱动
* 添加了4k显示补丁，显存2048M，原生HiDPI显示
* 去除了多余的驱动和patch
* 加入了DW1820a的device property驱动，可以支持apple watch自动解锁 
* 添加了屏蔽PM981a的patch
* 添加了雷电接口补丁，type-c扩展坞以太网卡工作正常

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


