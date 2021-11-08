# Y9000X-hackintosh

**Y9000X hackintosh 黑苹果 EFI**

---
主要更新记录
* 安装 ALCPlugFix-Swift 来修复扬声器切换异常问题, 终端使用以下命安装或卸载 ALCPlugFix
```
  bash -c "$(curl -fsSL https://gitee.com/YasuStudio/fix-speaker-y9000x/raw/master/FixSpeaker-Y9000X.sh)"
```
* 更新OC版本为0.7.5，支持Big Sur & Monterey
* [Sulisong](https://github.com/WangRicky/Y9000X-HACKINTOSH/pull/73)提供了一种睡眠唤醒死机的解决方案，但会牺牲HDMI音频功能，大家自行选择
* 升级big sur，支持内屏4k@60
* 解决了外接显示器音频输出问题，感谢[laoxiajiadeyun](https://github.com/laoxiajiadeyun)
* 使用`SSDT-PNLF-CFL.aml`来兼容10代CPU，感谢[EugeneSnikhovskiy](https://github.com/EugeneSnikhovskiy)，[carsonlius](https://github.com/carsonlius)。
* 新增了读卡器驱动
* 新增了触控板热补丁，基于本机原始DSDT制作，实现GPIO中断工作模式，采用预制变量法禁用原生备，无需重命名。
* 更改机型为16,4（**请注意，这是更符合i7版本的机型，其他CPU型号使用前请自行判断风险**），以获得更合适的机型模拟电源策略（长期测试发现风扇会安静一些），**更改机型的同时请注意USB定制，本次更新同时更新了USBPort.kext**。新增启动参数``igfxagdc=0``，解决TYPE-C直连DP显示器，TYPE-C转HDMI显示器输出问题
---
**配置** 
* 主板 HM370
* CPU i7-9750H
* 分辨率：4K
* 硬盘：PM981a（黑苹果无解，自行添加了东芝RD10）
* 网卡:intel AX200(已更换DW1820A) 

前期准备

---
**更换硬盘**

**更换网卡为dw1820a**

**关闭secure boot**

**切换硬盘模式为 AHCI**

**由于目前的机型为16,4，可能导致安装时出现低版本的系统无法正常安装的问题，请使用10.15.6镜像安装。**

* pm981a无法安装黑苹果，所以必须更换或增加硬盘，**安装双面SSD时，需取下原本SSD下面的一个黑色橡胶块，双面胶很牢固，需小心操作**。由于有pm981a存在，系统在访问pm981a硬盘文件时会导致死机重启。必须拆下三星的这块硬盘或者屏蔽这块硬盘。本efi默认屏蔽这块硬盘且pm981在第一硬盘位，如果你选择直接拆下这块硬盘，请删除efi/clover/acpi/patched/SSDT-DNVMe.aml文件，oc对应路径为`EFI/OC/ACPI/SSDT-DNVMe.aml`。
* 如使用其他网卡（自带AX200等），可删除DeviceProperties-->PciRoot(0x0)/Pci(0x1d,0x5)/Pci(0x0,0x0)节点，并将以下博通网卡和蓝牙的kext：`AirportBrcmFixup.kext`,`BrcmBluetoothInjector.kext`,`BrcmFirmwareData.kext`,`BrcmPatchRAM3.kext`的`Enabled`属性改为`False`，intel网卡的驱动可以使用[这个仓库](https://github.com/OpenIntelWireless/itlwm)
* 目前的config.plist是按照CFG LOCK解锁后配置的，如未解锁，请设置`AppleCpuPmCfgLock`和`AppleXcpmCfgLock`为true，本人配置CFG Lock的offset为0x3E,需要修改SaSetup和CPUSetup中对应值，改完后Hackintool显示CFG Lock已解锁，可按照[此教程进行操作](http://bbs.pcbeta.com/viewthread-1845189-1-1.html)， **修改BIOS ROM有风险，请谨慎操作**
* **`config.plist`中的个人的机器三码信息已删除，需要自己生成后填入，网友反馈，三码如果不填，会导致开机后屏幕亮度很低的情况**
# 本EFI特色
* 兼容了10代CPU集显
* 基于本机原始DSDT制作了触控板热补丁，实现GPIO中断工作模式，采用预置变量法禁用原生备，无需重命名
* 使用重命名EC方式，笔记本更适合重命名而非仿冒EC控制器
* 按照[黑果小兵](https://blog.daliansky.net/DW1820A_BCM94350ZAE-driver-inserts-the-correct-posture.html)的DW1820A蓝牙教程添加驱动，加入了DW1820a的device property驱动，可以支持apple watch自动解锁
* 添加了4k显示补丁，显存2048M，原生HiDPI显示
* 屏蔽PM981a，防止访问pm981a导致的系统不稳定
* ~~移除了csr-active-config参数，此参数导致SIP状态为unknown，如需关闭SIP,可在恢复模式中通过命令``csrutil disable`` 关闭~~,SIP全关闭会导致无法检测到OTA更新，已恢复此参数。
* 声卡加入延迟启动参数`alc-delay`,启动后声卡不加载的情况大幅度降低
# 工作

* 4k显示，背光调节正常 
* 耳机，麦克风，摄像头
* Wi-Fi 蓝牙 handoff airdrop
* 触控板全手势支持，工作模式为GPIO中断
* 电源管理，USB接口正常
* 读卡器
* type-c接口可以正常接U盘，接type-c扩展坞以太网卡、HDMI，DP工作正常
* 外接显示器音频输出正常

感谢[@hx2nn](https://github.com/hx2nn)，最初TYPE-C转HDMI没有驱动时，提供了14,1机型解决了问题。

# 不工作

**指纹**

**fn热键**

~~**扬声器**~~
~~官方论坛已经发起了有关外放和雷电的需求调研，希望大家可以去投票[链接地址](https://club.lenovo.com.cn/thread-5672284-1-1.html)~~

* ~~扬声器问题目前处于无解状态，Y9000X的功放经过了放大器，此设备目前无驱动，并且此设备挂在在INTEL智音下，基本处于无解状态，等外放的朋友可以死心了，有生之年系列~~
---
<img src="https://i.loli.net/2020/09/06/kVi3MrZCbp6ABjX.jpg" height="180"/>


**感谢每一位赞赏的朋友**

| 昵称 | 时间                  |
|----|---------------------|
| VT | 2020-09-10 21:05:26 |
| hx2nn | 2020-09-19 09:17:21 |
| doubleeyes | 2020-09-21 13:42:43 |
| 蒋悦 | 2020-09-27 10:01:47 |
| 夏末ソ夜微涼べ | 2020-10-12 15:13:01 |
| Peter | 2020-10-19 22:40:32 |
| 老夏家的云 | 2020-11-15 19:36:33 |
| 云天明 | 2021-03-08 09:14:12 |
| hx7869hx| 2021-11-01 11:40:03 |


