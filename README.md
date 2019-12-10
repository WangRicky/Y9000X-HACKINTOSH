# Y9000X-hackintosh

**Y9000X hackintosh 黑苹果 efi**

声卡和雷电转HDMI需要等待BIOS更新，官方论坛已经发起了调查，希望大家可以去投票[链接地址](https://club.lenovo.com.cn/thread-5672284-1-1.html)

**TYPE-C转以太网卡转换器，需要在启动至clvoer时，方向键选择停止倒计时后插入，方可稳定工作，热拔插的情况下，以太网卡会很不稳定，时断时续**

**配置** 
* 主板 HM370
* CPU i7-9750H
* 分辨率：4K
* 硬盘：PM981a（黑苹果无解，自行添加了东芝RC500）
* 网卡:intel AX200(黑苹果无解，已更换DW1820A) 

支持10.14

10.15系统未测试

* 按照[黑果小兵](https://blog.daliansky.net/DW1820A_BCM94350ZAE-driver-inserts-the-correct-posture.html)的DW1820A蓝牙教程添加驱动
* 添加了4k显示补丁，显存2048M，原生HiDPI显示
* 去除了多余的驱动和patch
* 加入了DW1820a的device property驱动，可以支持apple watch自动解锁 
* 添加了屏蔽PM981a的patch
* 添加了雷电接口补丁，type-c扩展坞以太网卡工作正常



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
* 雷电接口可以正常接U盘，接type-c扩展坞以太网卡工作正常

# 不工作

**指纹**

**fn热键**

**扬声器**

**雷电转接hdmi，dp 和 VGA**

* 音频尝试了自制Applealc驱动，扬声器节点为0x17，路径为0x02>0x17，均确认无误，编译的applealc正常驱动，外放无声，网友反馈此机型除Windows外，Linux、macOS系统扬声器均无法正常工作。

* 外接显示器刚需的朋友，~~建议使用AirPlay投屏设备，USB外接显示卡设备个人不推荐~~，网络环境对此影响非常大，而且无法使用HackinTool注入显示器EDID，现阶段建议使用USB外置显示卡,如果displaylink芯片不支持4k输出，外置显示器的HiDPI无法开启。


