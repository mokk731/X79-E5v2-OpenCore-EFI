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

    

