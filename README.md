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

### X79-H67-E5v2-my20241103.rar

本项目在 [DmitriyyyyS/Asus-H67](https://github.com/DmitriyyyyS/Asus-H67) 基础上，优化改动。感谢DmitriyyyyS的无私分享。


1, 基于OpenCore  0.7.7

2, 增加了RTL8111网卡驱动，  

3, 增加了Realtek ALC声卡驱动,alcid=1,ALC887 id要自己试，改动。
                        
    0x100202, 0x100302, layout 1, 2, 3, 5, 7, 11, 13, 17, 18, 20, 33, 40, 50, 52, 53, 87, 99

4, uefi-drivers-OpenUsbKbDxe.efi 改成false  。

5, 不管BIOS的 CFG Lock 是否已解锁， 都可以正常引导。

6,  MLB，SystemSerialNumber，SystemUUID 三码是原作者的，要重新改.

7， 能进入安装菜单，但多次试安装masos,不成功。可能少了SDT-IMEI，，，，

------------------------------------------------------------------------------------------

### OpenCore_X79_X99_Xeon_E5_2650v2-nguyenphucdev.zip


本项目在 [nguyenphucdev/OpenCore_X79_X99_Xeon_E5_2650v2](https://github.com/nguyenphucdev/OpenCore_X79_X99_Xeon_E5_2650v2) 基础上，优化改动,但进不了菜单，OC版本不兼容，只能用原版。感谢nguyenphucdev的无私分享。


1, 基于OpenCore  0.6.1     ， xeon W-3245M C16T32  macpro7.1   ，202012

2, 能成功安装macos,但重启后，不能进入macos 自动重启, Misc--Security--SecureBootModel 原定 j160- 10.15.1 (19B88)  ，要安装的是10.15.7，， 想改Disabled，但OC版本不兼容，只能用原版。

   用Hackintool瞎搞一通，有时重启后，能进入macos

3， https://geekdaxue.co/read/hejianzhao@zgnsc5/xnriw6

    Ivy Bridge 3XXX
    SDT-IMEI（6系主板才需要，例如H61主板、H67主板、P67主板、Z68主板）





------------------------------------------------------------------------------------------

优化改动目标：

https://github.com/AwSomeSiz/Atermiter_X79G_Hackintosh   OpenCore 0.8.0  ,    X79G and Xeon E5-1650 v2   RX 570 4GB ,   用OpenCore 0.8.8，打开有错误

https://github.com/antipeth/EFI-Motherboard-X79-OpenCore-Hackintosh   ,   OpenCore 0.7.7   huanan-x79  E5-2450v2   HD 7750 1G  ,  用OpenCore 0.8.8，打开没错误, #####


https://github.com/DmitriyyyyS/Asus-H67 , OpenCore  0.7.7 ，Asus-H67  Intel Xeon 3270  GT 710 (Kepler)   ,用OpenCore 0.8.8，打开有错误, 改了可以通过， 能进入安装菜单，但多次试安装masos,不成功。可能少了SDT-IMEI


------------------------------------------------------------------------------------------





出现跑码：   OC: Grabbed zero system-id for SB, this is not allowed

处理：      设置Misc--Security--SecureBootModel--Disabled



出现跑码：  Panic diags file unavailable, panic occurred prior to initialization

处理：     尝试1：更改kext加载顺序，更改后VirtualSMC.kext -> SMCSuperIO.kext -> SMCProcessor.kext，看看有没有效果。


------------------------------------------------------------------------------------------

[3代老主机安装黑苹果catalina 10.15.7的思路](https://www.bilibili.com/read/cv13039059)

    选择catalina版本是因为苹果官方并不支持3代安装big sur，虽然黑苹果没有这个限制，可以改smbios机型安装big sur，但其实3代真不适合big sur，catalina也非常够用了 。

    由于是3代ivy brige架构搭配6系芯片组，需要在apci里添加SSDT-IMEI.aml，否则可能会出现错误。如果是7系芯片组则不需要。

    配置核显加速的AAPL,ig-platform-id为07002601，因为核显并不输出图像，所以只作为运算加速。

    h61有些主板用的是比较冷门的sata控制器，所以SATA-unsupported.kext最好加上，

    关于usb的驱动，其实一个USBInjectAll.kext就搞掂了。

    另外，因为是免驱的nv显卡，引导参数记得加上nvda_drv_vrl=1，

    机型可以选imacpro1,1，我这边选的是imac15,1，相差并不大。 
    

https://imacos.top/2019/07/22/1409/  小白也能看懂的入门教程DSDT/SSDT/ROM提取完整步骤编译拆分补丁除错实现笔记本电脑电池显示

https://www.yuque.com/hejianzhao/zgnsc5/xnriw6

https://geekdaxue.co/read/hejianzhao@zgnsc5/xnriw6
   
https://dortania.github.io/OpenCore-Install-Guide/config.plist/ivy-bridge.html#acpi


https://65536.io/2024/04/742.html 使用ControlMsrE2解锁BIOS的CFG Lock选项

    FS0: ControlMsrE2.efi unlock


https://imacos.top/2019/07/22/1409/  小白也能看懂的入门教程DSDT/SSDT/ROM提取完整步骤编译拆分补丁除错实现笔记本电脑电池显示

https://www.zdynb.cn/2020/jie-suo-cfg-lock.html 解锁CFG Lock


------------------------------------------------------------------------------------------

ACPI--ADD

    SSDT-PM （可进入MacOS的再安装）
    SSDT-EC
    SSDT-IMEI （6系主板才需要，例如H61主板、H67主板、P67主板、Z68主板）




DeviceProperties--Add

    PciRoot(0x0)/Pci(0x2,0x0) 类型：Dictionary
    AAPL,ig-platform-id 类型：Data
    0A006601 这是台式机HD 4000的示例
    07006201 	Used when the iGPU is only used for computing tasks and doesn't drive a display

    PciRoot(0x0)/Pci(0x16,0x0)
    如果要将Ivy Bridge CPU与6系列主板（即H61，B65，Q65，P67，H67，Q67，Z68）配对，则需要这样做，特别是为了欺骗您的IMEI设备。请注意，此属性是无论是否使用SSDT-IMEI，仍然需要。
    device-id 类型：Datar
    3A1E0000
    注意：如果您使用的是7系列主板（例如B75，Q75，Z75，H77，Q77，Z77），则不需要这样做

    PciRoot(0x0)/Pci(0x1b,0x0) 类型：Dictionary
    可以立即删除此属性
    在NVRAM——Add——7C436110-AB2A-4BBB-A880-FE41995C9F82——boot-args增加alcid=xxx参数，将覆盖存在的所有其他布局ID，请查看这里并确定您的声卡型号，然后找到对应的参数。https://github.com/acidanthera/AppleALC/wiki/Supported-codecs
    例如，声卡ALC892，alcid=xxx参数，可以设置为alcid=1参数




 Kernel--Add    不用修改
 
    ■ 加载顺序    像Lilu这样的kext必须先加载，后再加载VirtualSMC，AppleALC，WhateverGreen，使用ProperTree工具可自动完成
    ■ 如果不想加载某个Kext，可以把Enabled设置为False

    
 Kernel--Quirks

    ■ AppleCpuPmCfgLock：YES    
      ● 如果在BIOS中禁用了CFG-Lock，则不需要
    ■ AppleXcpmCfgLock：YES    
      ● 如果在BIOS中禁用了CFG-Lock，则不需要
    ■ CustomSMBIOSGuid：NO    
      ● 对UpdateSMBIOSMode自定义模式执行GUID修补。
    ■ DisableIOMapper：YES    
      ● 如果在BIOS中禁用了VT-D，则不需要，如果BIOS没有这一项就需要开启
    ■ DisableLinkeditJettison：YES   
      ● 允许Lilu和其他具有更可靠的性能，而无需keepsyms = 1
    ■ DisableRtcChecksum：NO    
      ● 适用于在重启/关机后收到BIOS重置或发送到安全模式的用户，阻止AppleRTC写入主校验和（0x58-0x59）
    ■ ExtendBTFeatureFlags：NO
      ● 对于非Apple / Fenvi卡连续性问题有帮助
    ■ LapicKernelPanic：NO    
      ● HP惠普机器需要YES设置
    ■ LegacyCommpage：NO
      ● 解决了macOS中对64位CPU的SSSE3要求，该要求主要与64位Pentium 4 CPU（即Prescott）有关
    ■ PanicNoKextDump：YES
      ● 允许在发生内核紧急情况时读取内核紧急情况日志
    ■ PowerTimeoutKernelPanic：YES
      ● 通过macOS Catalina中的Apple驱动程序（尤其是数字音频）帮助修复与电源更改有关的内核崩溃
    ■ XhciPortLimit：YES
      ● 最好创建USB map映射

  
      

 Misc--Security    这项很重要，请不要跳过
 
    ■ AllowNvramReset：YES    类型：Boolean
      ● 允许在启动选择器中以及按Ctrl+Alt+P+R
    ■ AllowSetDefault：YES    类型：Boolean
      ●  允许CTRL + Enter和CTRL + Index在选择器中设置默认启动设备
    ■ ApECID: 0
      ● 保留默认值
    ■ AuthRestart：NO
      ● 重启时不需要启用经过身份验证FileVault2密码
    ■ BootProtect：Bootstrap
      ● 允许在EFI / OC / Bootstrap中使用Bootstrap.efi代替BOOTx64.efi
      ● 对于希望使用rEFInd引导或避免从Windows覆盖BOOTx64.efi的用户很有用
    ■ DmgLoading：Signed
      ● 确保仅限签名DMGs才加载
    ■ ExposeSensitiveData：6
      ● 显示更多的调试信息，需要OpenCore的调试版本
    ■ Vault：Optional    类型：String
      ● 务必设置为Optional，否则您会后悔
      ● 请注意，区分大小写
    ■ ScanPolicy：0    类型：Number
    ■ SecureBootModel：Default    类型：String
      ● 这是一个单词，区分大小写，如果您不希望安全启动，则设置为“ Disabled”（即，您需要Nvidia的Web驱动程序）
      ● 通常把这项删除


 Misc--Tools
 
    ■ 用于运行OC调试工具，例如shell，ProperTree的快照功能将为您添加这些内容，请您忽略


NVRAM--Add

    7C436110-AB2A-4BBB-A880-FE41995C9F82 类型：Dictionary

    boot-args
        -v
            这将启用详细模式，该模式显示启动时滚动显示的所有幕后文本，而不是Apple徽标和进度条。对于任何Hackintosher来说，这都是无价之宝，因为它可以让您深入了解启动过程，并可以帮助您识别问题，问题扩展等
        debug=0x100
            这会禁用macOS的看门狗，这有助于防止内核崩溃时重启。这样，您可以收集一些有用的信息，并按照提示解决问题
        keepsyms=1
            这是debug= 0x100的辅助设置，它告诉OS还在内核崩溃时打印符号。这样可以对引起崩溃的原因提供更多有用的说明
        alcid=1
            用于设置AppleALC的layout-id，请参阅本页DeviceProperties—>PciRoot(0x0)/Pci(0x1b,0x0) 设置
        nvda_drv_vrl=1 
            用于在Sierra和HighSierra的Maxwell和Pascal卡上启用Nvidia的Web驱动程序

UEFI--Drivers

    ■ 这里只需放入2个.efi驱动程序
      ● HfsPlus.efi
      ● OpenRuntime.efi

      

    

