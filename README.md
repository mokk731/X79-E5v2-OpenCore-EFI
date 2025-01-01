# X79-H67-E5v2-OpenCore-EFI
X79-H67-E5v2-OpenCore-EFI,Hackintosh



## 我的硬件表：

CPU :  E5-2650 V2 . 3代ivy brige

主板 ： X79-H67  山寨板 

内存 ： DDR3 ECC 1333 8G*2

显卡 ： GTX650 1G  GK107-450 免驱动

声卡 ： Realtek ALC887

网卡 ： RTL8111

SSD ：  tigo 120G sata ssd

bios ： AMI uEFI

![macos202411](https://github.com/mokk731/X79-E5v2-OpenCore-EFI/blob/main/mac202411.jpg)

------------------------------------------------------------------------------------------

### X79-H67-E5v2-DmitriyyyyS-my20241103.rar

本项目在 [DmitriyyyyS/Asus-H67](https://github.com/DmitriyyyyS/Asus-H67) 基础上，优化改动。感谢DmitriyyyyS的无私分享。


    1, 基于OpenCore  0.7.7

    2, 增加了RTL8111网卡驱动，  

    3, 增加了Realtek ALC声卡驱动,alcid=1,ALC887 id要自己试，改动。
                        
    0x100202, 0x100302, layout 1, 2, 3, 5, 7, 11, 13, 17, 18, 20, 33, 40, 50, 52, 53, 87, 99

    4, uefi-drivers-OpenUsbKbDxe.efi 改成false  。

    5, 不管BIOS的 CFG Lock 是否已解锁， 都可以正常引导。

    6,  MLB，SystemSerialNumber，SystemUUID 三码是原作者的，要重新改.

    7， 能进入安装菜单，但多次试安装macos,不成功。可能少了SDT-IMEI，，，，


### X79-H67-E5v2-DmitriyyyyS20250101.zip

    1, 升级OpenCore  0.7.8
    2. ACPI--ADD 全删，换X79_E5_2650v2-nguyenphucdev 的
    ３．Kernel--Add，　加入SMCSuperIO.kext.  VoodooTSCSync.kext
    4. Kernel--Quirks  :
       AppleCpuPmCfgLock：YES
       AppleXcpmCfgLock：YES
       DisableIOMapper：YES
       DisableLinkeditJettison：YES
       PanicNoKextDump：YES
       PowerTimeoutKernelPanic：YES
       XhciPortLimit：YES
    5. SecureBootModel： Disabled
    6. boot-args:   -v debug=0x100 keepsyms=1 npci=0x3000 alcid=1
    7. 三码空白
    8. 能进入安装菜单，但多次试安装macos,不成功,安装到一半，就自动重启， 还没到选国家。


------------------------------------------------------------------------------------------

### X79_E5_2650v2-nguyenphucdev-my20241118.rar


本项目在 [nguyenphucdev/OpenCore_X79_X99_Xeon_E5_2650v2](https://github.com/nguyenphucdev/OpenCore_X79_X99_Xeon_E5_2650v2) 基础上，优化改动,但进不了菜单，OC版本不兼容，只能用原版。感谢nguyenphucdev的无私分享。


1, 基于OpenCore  0.6.1     ， xeon W-3245M C16T32  macpro7.1   ，202012

2, 能成功安装macos,但重启后，不能进入macos 自动重启, Misc--Security--SecureBootModel 原定 j160- 10.15.1 (19B88)  ，要安装的是10.15.7，， 想改Disabled，但OC版本不兼容，只能用原版。

   用Hackintool瞎搞一通，有时重启后，能进入macos

3， 有完整的ACPI:  SSDT-PM， SSDT-EC，SSDT-IMEI,SSDT-RTC0-RANGE

    https://geekdaxue.co/read/hejianzhao@zgnsc5/xnriw6
    Ivy Bridge 3XXX
    SDT-IMEI（6系主板才需要，例如H61主板、H67主板、P67主板、Z68主板）

### 改动：

    1，升级到 OpenCore  0.7.8
    
    2，修改：

    DeviceProperties--Add
    PciRoot(0x0)/Pci(0x16,0x0)

    Kernel--Quirks
    DisableLinkeditJettison：YES 

    Misc--boot 
    PickerMode:External

    Misc--Security
    SecureBootModel: Disabled

    NVRAM--Add
    boot-args:   -v debug=0x100 keepsyms=1 npci=0x3000 nvda_drv_vrl=1  alcid=1


 能进入安装菜单，但多次试安装macos,不成功。安装到一半，就自动重启， 还没到选国家。


------------------------------------------------------------------------------------------

### x79-e5-2670-gtx650-cheneyveron20250101.zip

本项目在 [cheneyveron/clover-x79-e5-2670-gtx650](https://github.com/cheneyveron/clover-x79-e5-2670-gtx650) 基础上，优化改动。感谢cheneyveron的无私分享。



### 改动：

    1. 基于 OpenCore 0.6.4(2020-12-7)   iMacPro1,1    iMacPro1,1    Intel Xeon W-2140B CPU @ 3.20 GHz

    2. 原EFI,能进入选系统菜单，但不能进入安装菜单，

    3. 升级OC0.7.8 ,瞎改动一通， 能进入安装菜单，但多次试安装macos,不成功. 安装到一半，就自动重启， 还没到选国家。
    
    4. UEFI--Drivers. 删除错误。

    5. Kernel--Quirks  :
       AppleCpuPmCfgLock：YES
       AppleXcpmCfgLock：YES
       DisableIOMapper：YES
       DisableLinkeditJettison：YES
       PanicNoKextDump：YES
       PowerTimeoutKernelPanic：YES
       XhciPortLimit：YES

    6. PI : 三码改空白
    
  


一、macOS 11 Big Sur特别说明:

注意：Big Sur的支持并不完善，建议先另分一个区安装测试，没问题后再升级。有修正想法的朋友们，欢迎PR。

如果不需要升级Big Sur，请直接到Release下载旧版本EFI即可。

1. DSDT改动
由于寨板版型众多，此处列举的未必全面。请根据EFI/OC/ACPI/DSDT-SAMPLE.aml或者DSDT-SAMPLE2.aml对照修改自身DSDT。

感谢 @szcxs 提供了示例DSDT。

1) 三个变量的默认值修改：
Name (BRL, 0xFF)
Name (MBB, 0xCC000000)
Name (MBL, 0x34000000)
由于这三个变量初始值未必一致，所以请自行搜索BRL，MBB，MBL修改。

2) Processor方法
有些主板的第二个参数原本是统一的0x00，需要改成下面的：

C000-C00F 映射 0x00-0x0F
C010-C01F 映射 0x10-0x1F
C100-C10F 映射 0x20-0x2F
C110-C11F 映射 0x30-0x3F
C200-C20F 映射 0x40-0x4F
C210-C21F 映射 0x50-0x5F
C300-C30F 映射 0x60-0x6F
C310-C31F 映射 0x70-0x7F
举例：

映射前：Processor (C005, 0x00, 0x00000410, 0x06)

映射后：Processor (C005, 0x05, 0x00000410, 0x06)

注1：2.49版本的BIOS中已经修复了此问题。
注2：DSDT Patch因主板而异。
3) 屏蔽设备^UNC0
直接删除，或者在它的_STA方法里返回(Zero)

我未能用SSDT屏蔽该设备，请求对ACPI规范熟悉的朋友们的帮助。

由于不推荐使用别人的dsdt，在此建议各位自行提取并修改DSDT。

二、OpenCore 说明

遵循OC的哲学，我会试图最小化改动来适应macOS。但是未必适合各位的主板。

最小化的改动包含如下内容：

1. ACPI部分

        加载按照上面说明修改过的DSDT.
        如果需要变频，则加载自己处理器的SSDT-1.aml. 如果不是2630L V2，请到attachments/SSDT-1中自行查找。
2. Kernel部分
 
        Lilu.kext :用于注入其他驱动
        VirtualSMC.kext :模拟SMC。不使用它也可以将AppleSmcIo置为true
        VoodooTSCSync.kext :必须，否则卡第二阶段。修复CPU线程同步问题。
        WhateverGreen.kext :用于修复可能存在的显示问题
        AppleALC.kext :用于声音输出。也可以使用VoodooHDA代替。
        RealtekRTL8111.kext :有线网卡驱动
        USBMap.kext :USB端口映射文件。Big Sur下, USBInjectAll.kext未必能用，请使用这里的工具生成。
        CPUFriend.kext & CPUFriendDataProvider.kext :注入频率信息。
3. UEFI/Drivers
   
        HfsPlus.efi :用于识别HFS+格式分区
        OpenRuntime.efi :OpenCore核心环境
4. 其他Quirk
   
        AllowNvramReset: true。否则无法重置nvram。
        AllowSetDefault: true。否则无法使用Ctrl + 数字键设置默认系统。
        BootProtect: None。
        SecureBootModel: Disabled。
   
5. Vault：Optional。以上三个关闭OC安全启动功能。

6. boot-args：-v keepsyms=1 debug=0x100 npci=0x3000，必须添加npci=0x3000



------------------------------------------------------------------------------------------





优化改动目标：

https://github.com/AwSomeSiz/Atermiter_X79G_Hackintosh   OpenCore 0.8.0  ,    X79G and Xeon E5-1650 v2   RX 570 4GB ,   用OpenCore 0.8.8，打开有错误

https://github.com/antipeth/EFI-Motherboard-X79-OpenCore-Hackintosh   ,   OpenCore 0.7.7   huanan-x79  E5-2450v2   HD 7750 1G  ,  用OpenCore 0.8.8，打开没错误, #####


https://github.com/DmitriyyyyS/Asus-H67 , OpenCore  0.7.7 ，Asus-H67  Intel Xeon 3270  GT 710 (Kepler)   ,用OpenCore 0.8.8，打开有错误, 改了可以通过， 能进入安装菜单，但多次试安装masos,不成功。可能少了SDT-IMEI  #####


------------------------------------------------------------------------------------------


[3代老主机安装黑苹果catalina 10.15.7的思路](https://www.bilibili.com/read/cv13039059)

    选择catalina版本是因为苹果官方并不支持3代安装big sur，虽然黑苹果没有这个限制，可以改smbios机型安装big sur，但其实3代真不适合big sur，catalina也非常够用了 。

    由于是3代ivy brige架构搭配6系芯片组，需要在apci里添加SSDT-IMEI.aml，否则可能会出现错误。如果是7系芯片组则不需要。

    配置核显加速的AAPL,ig-platform-id为07002601，因为核显并不输出图像，所以只作为运算加速。

    h61有些主板用的是比较冷门的sata控制器，所以SATA-unsupported.kext最好加上，

    关于usb的驱动，其实一个USBInjectAll.kext就搞掂了。

    另外，因为是免驱的nv显卡，引导参数记得加上nvda_drv_vrl=1，

    机型可以选imacpro1,1，我这边选的是imac15,1，相差并不大。 
    

------------------------------------------------------------------------------------------

出现跑码：   OC: Grabbed zero system-id for SB, this is not allowed

    处理： 设置Misc--Security--SecureBootModel--Disabled



出现跑码：  Panic diags file unavailable, panic occurred prior to initialization

    处理： 尝试1：更改kext加载顺序，更改后VirtualSMC.kext -> SMCSuperIO.kext -> SMCProcessor.kext，看看有没有效果。


黑苹果安装到一半重启

    virtualsmc要加启动参数vsmcgen=1

FS3:
ControlMsrE2.efi unlock

nvda_drv_vrl=1 

Ivy Bridge  ACPI  

    SSDT-PM 装好MacOS再装这个
    SSDT-EC
    SSDT-IMEI
    6系列主板的Ivy Bridge架构的CPU需要这个文件


------------------------------------------------------------------------------------------

    

