# X79-H67-E5v2-OpenCore-EFI
X79-H67-E5v2-OpenCore-EFI,Hackintosh

OpenCore_0.7.7



## 我的硬件表：

CPU :  E5-2650 V2

主板 ： X79-H67  山寨板 

内存 ： DDR3 ECC 1333 8G*2

显卡 ： GTX650 1G  GK107-450 免驱动

声卡 ： Realtek ALC887

网卡 ： RTL8111

SSD ：  120G sata ssd

bios ： AMI uEFI


本项目在 [DmitriyyyyS/Asus-H67](https://github.com/DmitriyyyyS/Asus-H67) 基础上，优化改动。感谢DmitriyyyyS的无私分享。


1, 基于OpenCore  0.7.7

2, 增加了RTL8111网卡驱动，  

3, 改动Realtek ALC声卡驱动,alcid=1,id要自己试，改动。

4, uefi-drivers-OpenUsbKbDxe.efi 改成false  。

5, 不管BIOS的 CFG Lock 是否已解锁， 都可以正常引导。


[3代老主机安装黑苹果catalina 10.15.7的思路](https://www.bilibili.com/read/cv13039059)

选择catalina版本是因为苹果官方并不支持3代安装big sur，虽然黑苹果没有这个限制，可以改smbios机型安装big sur，但其实3代真不适合big sur，catalina也非常够用了 。

