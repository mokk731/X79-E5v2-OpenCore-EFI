## OpenCore-EFI设置

https://www.yuque.com/hejianzhao/zgnsc5/xnriw6

https://geekdaxue.co/read/hejianzhao@zgnsc5/xnriw6
   
https://dortania.github.io/OpenCore-Install-Guide/config.plist/ivy-bridge.html#acpi


------------------------------------------------------------------------------------------

解锁CFG



https://65536.io/2024/04/742.html 使用ControlMsrE2解锁BIOS的CFG Lock选项

    FS0: ControlMsrE2.efi unlock


https://www.zdynb.cn/2020/jie-suo-cfg-lock.html 解锁CFG Lock

------------------------------------------------------------------------------------------

提取DSDT

https://imacos.top/2019/07/22/1409/  小白也能看懂的入门教程DSDT/SSDT/ROM提取完整步骤编译拆分补丁除错实现笔记本电脑电池显示

https://blog.xjn819.com/post/opencore-guide.html
使用 OpenCore 引导黑苹果

尽管提取原始DSDT的方法非常多，我认为 CLOVER 的提取方法是最方便并且靠谱的。我们需要一个空的U盘或者空的ESP分区，我的教程是非常偏向小白的，所以这里提取我也会用到windows，以及Diskgenius这个软件，做最简单的示范。
放入我从黑果小兵镜像包提取出来的EFI放进去。这是一个 clover 引导，但并不能引导你的系统，只能提取 DSDT。
插上U盘，重启，通过U盘引导，看到Clover界面，我们按F4，这样原始的DSDT文件就收集好了。
重新通过OC引导进入系统，我们打开U盘，EFI/Clover/ACPI/Orgin下，有我们的原始ACPI内容，我们只需要DSDT.aml这个就行了


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
    OpenShell    ControlMsrE2

NVRAM--Add

    7C436110-AB2A-4BBB-A880-FE41995C9F82 类型：Dictionary

    boot-args:   -v debug=0x100 keepsyms=1 npci=0x3000 nvda_drv_vrl=1  alcid=1

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
        启动参数vsmcgen=1

PI

      xeon W-3245M  macpro7.1

UEFI--Drivers

    ■ 这里只需放入2个.efi驱动程序
      ● HfsPlus.efi
      ● OpenRuntime.efi

      
