## 解锁CFG



https://65536.io/2024/04/742.html 使用ControlMsrE2解锁BIOS的CFG Lock选项

    FS1: ControlMsrE2.efi unlock



### 提取CFG Lock 地址

https://www.zdynb.cn/2020/jie-suo-cfg-lock.html 解锁CFG Lock

    下面是所有需要准备的工具：
    FWPTW64.exe AMI BIOS通刷的工具
    下载地址：https://comsystem-tlt.ru/obzori/me-txe-region
    RU UEFI或DOS图形界面操作BIOS隐藏选项的工具
    下载地址：http://ruexe.blogspot.com（翻墙才能打开）
    AMIBCP.exe 打开AMI BIOS 修改的工具（这个在官网中下载不到，希望有渠道的朋友提供下最新的版本）
    AFUWIN64.exe AIM官方刷BIOS工具（只支持官方未经修改的BIOS刷入）
    下载地址：https://ami.com/en/products/firmware-tools-and-utilities/bios-uefi-utilities/
    UEFITool 查找BIOS中相关变量（字串）的工具：
    下载地址：https://github.com/LongSoft/UEFITool/releases
    IRFExtractor.exe 解释UEFI Tool二进制成文本的工具
    下载地址：https://github.com/LongSoft/Universal-IFR-Extractor/releases
    CloverBootloader 黑果引导
    下载地址：https://github.com/CloverHackyColor/CloverBootloader/releases
    
    提取主板BIOS
    管理员权限运行下列命令：FPTW64.exe -D 备份文件名.rom -bios

    提取BIOS信息
    使用UEFITool这个工具,选择File > Search（或Ctrl + F快捷键）弹出搜索框，点到GUID 项并在” Search scope”中勾选”Header only”，粘贴GUID:899407D799FE43D89A2179EC328CAC21（这段GUID其实就是BIOS中Setup项的特殊标识，因为不管CFG Lock、 
    BIOS Lock、DVMT还是Speed Shift都是在Setup下面的）。然后会出现这样的信息：
    GUID pattern “899407D7-99FE-43D8-9A21-79EC328CAC21” found as “D7079489FE99D8439A2179EC328CAC21” in Setup at header-offset 00h
    双击这段信息，会自动将Setup 的位置找出来，这时需要在找到的Setup
    
    选择子项目：Setup--compressed section--minsetupresoucesection,
    
    那里点右键，选择Extract as is… ，把提取的Setup模块（**.sct或**.bin）保存到相应文件夹

    接下来，我们需要把该模块转换成我们能读懂的信息。我们需要借助IFRExtractor这个工具，直接点击右侧加载模块按钮，再点击Extract，转换模块为TXT文本，并保存到相应文件夹，
    
    寻找需要的偏移量
    此时用文本工具打开，并查找CFG 即可看到如下信息：
    One Of: MMCFG BASE, VarStoreInfo (VarOffset/VarName): 0x11D, VarStore: 0x1, QuestionId: 0x29, Size: 1, Min: 0x0, Max 0x0, Step: 0x0 

    得到地址：
    VarStoreInfo (VarOffset/VarName): 0x11D, VarStore: 0x1, 

----------------------------------------------------------------------------------------

### modGRUBShell 解锁CFG Lock

1, Download modGRUBShell and place it in the EFI/OC/Tools folder. Add it to the Misc → Tools section of config.plist.

2, Boot into OpenCore and select the modGRUBShell option.

3, Enter the following values:

Disable CFG Lock:

    setup_var 0x11D 0x0

    实际：原0x1，改为0x0
    
    
