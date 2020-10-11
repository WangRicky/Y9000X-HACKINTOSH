# Y9000X-hackintosh

**Y9000X hackintosh 黑苹果 EFI**

---
**由于目前的机型为16,4，可能导致安装时出现低版本的系统无法正常安装的问题，请使用10.15.6镜像安装。**

~~实践证明，此款笔记本无法安装双面颗粒的SSD，升级SSD的朋友们选购时需注意~~
安装双面SSD时，需取下原本SSD下面的一个黑色橡胶块，双面胶很牢固，需小心操作

---
更新记录
* 新增了触控板热补丁，基于本机原始DSDT制作，实现GPIO中断工作模式，采用预制变量法禁用原生备，无需重命名。
* 更新OC版本为0.6.2，同步更新了驱动
* 更改机型为16,4（**请注意，这是更符合i7版本的机型，其他CPU型号使用前请自行判断风险**），以获得更合适的机型模拟电源策略（长期测试发现风扇会安静一些），**更改机型的同时请注意USB定制，本次更新同时更新了USBPort.kext**。新增启动参数``igfxagdc=0``，解决TYPE-C直连DP显示器，TYPE-C转HDMI显示器输出问题
* 移除了csr-active-config参数，此参数导致SIP状态为unknown，改为在恢复模式中通过命令``csrutil disable`` 关闭SIP。
* 更新oc至0.5.9，更新了一些驱动，由于高分屏文字引导模式效果比较差，所以使用了官方的图形化引导界面
* 修正了蓝牙驱动配置，此前升级了驱动文件，遗漏了config.plist中的配置
* ~~更新了仿冒EC设备补丁，放弃EC重命名~~经长时间测试，笔记本还是适合直接重命名；同时去除了一些不必要的重命名
* 新增ALC声卡驱动延迟加载参数，解决时声卡可能不可用问题
* 将机型改为14,1，雷电转HDMI正常，感谢[@hx2nn](https://github.com/hx2nn)
* 添加了屏蔽PM981a的patch
---
**`config.plist`中的个人的机器三码信息已删除，需要自己生成后填入，网友反馈，三码如果不填，会导致开机后屏幕亮度很低的情况**

CFG Lock 已解锁，本人配置CFG Lock的offset为0x3E,需要修改SaSetup和CPUSetup中对应值，改完后Hackintool显示CFG Lock已解锁。

可按照[此教程进行操作](http://bbs.pcbeta.com/viewthread-1845189-1-1.html)

**修改BIOS ROM有风险，请谨慎操作**

目前的config.plist是按照CFG LOCK解锁后配置的，如未解锁，请设置`AppleCpuPmCfgLock`和`AppleXcpmCfgLock`为true（之前升级oc到0.5.7的时候这两个选项错误的设置为了`false`,但使用起来却没发现有影响，个人也不清楚具体原因，如有网友知道原理的，请不吝赐教）

~~声卡和雷电转HDMI需要等待BIOS更新，官方论坛已经发起了有关外放和雷电的需求调研，希望大家可以去投票[链接地址](https://club.lenovo.com.cn/thread-5672284-1-1.html)~~


* 按照[黑果小兵](https://blog.daliansky.net/DW1820A_BCM94350ZAE-driver-inserts-the-correct-posture.html)的DW1820A蓝牙教程添加驱动
* 添加了4k显示补丁，显存2048M，原生HiDPI显示
* 加入了DW1820a的device property驱动，可以支持apple watch自动解锁 

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

* 扬声器问题目前处于无解状态，Y9000X的功放经过了放大器，此设备目前无驱动。
---
<img src="https://i.loli.net/2020/09/06/kVi3MrZCbp6ABjX.jpg" height="180"/>


**感谢每一位赞赏的朋友**

| 昵称 | 时间                  |
|----|---------------------|
| VT | 2020-09-10 21:05:26 |
| hx2nn | 2020-09-19 09:17:21 |
| doubleeyes | 2020-09-21 13:42:43 |
| 蒋悦 | 2020-09-27 10:01:47 |



