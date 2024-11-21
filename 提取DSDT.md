## 提取DSDT

https://imacos.top/2019/07/22/1409/  小白也能看懂的入门教程DSDT/SSDT/ROM提取完整步骤编译拆分补丁除错实现笔记本电脑电池显示

https://blog.xjn819.com/post/opencore-guide.html
使用 OpenCore 引导黑苹果


尽管提取原始DSDT的方法非常多，我认为 CLOVER 的提取方法是最方便并且靠谱的。我们需要一个空的U盘或者空的ESP分区，我的教程是非常偏向小白的，所以这里提取我也会用到windows，以及Diskgenius这个软件，做最简单的示范。
放入我从黑果小兵镜像包提取出来的EFI放进去。这是一个 clover 引导，但并不能引导你的系统，只能提取 DSDT。
插上U盘，重启，通过U盘引导，看到Clover界面，我们按F4，这样原始的DSDT文件就收集好了。
重新通过OC引导进入系统，我们打开U盘，EFI/Clover/ACPI/Orgin下，有我们的原始ACPI内容，我们只需要DSDT.aml这个就行了
