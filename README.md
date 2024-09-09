# 前言-你需要知道的一些东西

> ### 此教程面向小米10系列，其他小米设备也可以参考
>
> ### 电脑系统以Windows为主，演示系统：Windows 11 23H2

### <span id="device_Code">机型代号 </span>：

**Mi10：(Umi)**

**Mi10Pro：(Cmi)**

**Mi10/10Pro  2 in 1：(Ucmi)**

**Mi10U：(Cas)**

------

# 关于解锁

如果您是MIUI系统，直接在电脑上下载小米解锁工具按着官方的步骤来

如果您是澎湃系统，请自行在网上搜索"澎湃解BL锁"解决

若想跳过168小时可以去看看有没有人秒解，当然，这需要钞能力

# 系统介绍

> ### 主要有安卓13(A13)和安卓14(A14)两大版本
>

### 系统有什么区别？怎么选？

> ### A13主要是稳定，省电，追求功耗的可选此。
>
> ### A14主要为了满血澎湃，追求澎湃新特性新功能的选此。
>
> ### A13有MIUI14的官改和移植，HyperOS的官改和移植
>
> ### A14只有HyperOS的移植
>
> ### A13移植自动亮度有问题，会出现打开手电筒屏幕亮度拉满的情况

#### Cmi：

- **A13：**

	**MIUI：官改，红米Note13Pro移植，小米13U移植**

	**澎湃：官改，小米12X移植**

- **A14澎湃：小米12SU移植，13U移植，14U移植**

#### Umi/Cas：

- **A13：红米Note13Pro移植MIUI，官改澎湃，小米12X移植澎湃**

- **A14澎湃：小米12SU移植，13U移植，14U移植**



**A13MIUI推荐13u移植和note13p移植，前者丝滑，后者完美没有bug，澎湃推荐12x移植**

**A14的12su相对省电，13u和14u现在功能特性都差不多，14u多了个定位卫星**

**养老就12x移植**



如有Carwith等需求且要a13的请选12x移植

目前没有太多新包值得移植，最后打磨完毕后再有任何bug请自行解决或回退版本

带NFC2.0的包可能会导致NFC异常，不建议选择



## <span id="sys_Format">EXT4与EROFS的区别与内核</span>

EXT4使用官方内核，EROFS使用TV的VK内核

EROFS不使用官方内核是因为HyperOS系统官方默认开启墓碑v2机制。 

小米10系列官方系统内核为4.19版本，只支持墓碑v1机制，系统墓碑挂载会提示不完整。，而TV大佬的第三方内核可以开启完整的墓碑v2机制，所以使用TV内核。 

想上车内核可以咨询群内管理@The Voyager （QQ：727127746）有更多新功能使用，并且持续优化调度

# 刷机教程

## <span id="flash_rec">（可选）刷入第三方Recovery（REC）</span>

> ## 绝大部分人选择TWRP作为第三方REC使用，故此教程使用TWRP作为演示，其他REC也可按着此教程操作

### 请先将手机关机，按住电源键和音量下键进入fastboot模式，连接电脑

### 方法一：在群文件或其他地方下载一键刷入TWRP并解压运行

### 方法二：下载好第三方Recovery用搞机助手等工具刷入

### 方法三：传统命令刷入，接下来的步骤需要使用到fastboot命令，若没配置adb请[点击这里](#adb_install)查看教程

1. 下载第三方Recovery，可以是群里的，也可以是其他地方的，推荐skkk的TWRP，或者去酷安@mi_block的帖子里下载对应机型的REC（[点此跳转](https://www.coolapk.com/feed/45189101?shareKey=ZGEzYzNkOTViNjU5NjZjOWU0NjU~&shareUid=4400238&shareFrom=com.coolapk.market_13.4.1)）

2. 解压出来下载的Recovery.img，查看是否支持boot临时启动，以skkk的TWRP为例

   <img src="image\TWRP_name_label.png" alt="TWRP_name_label" />

   **带有REC标签为只能刷入Recovery分区使用，带有BOOT标签则支持临时启动，同时存在则表示两种方法均可**

3. 打开DOS窗口（Terminal，PowerShell，CMD均可），输入"fastboot devices"查看有没有设备连接

   若显示"< waiting for any device >"或什么都没显示请检查手机是否进入fastboot 模式，尝试安装驱动（群内下载），更换或使用数据线另一面，更换USB 2.0接口

   <img src="image\fastboot-devices.png" alt="fastboot-devices" />

   若显示多个设备请断开其他多余的连接，只保留需要刷入的那一个设备

   <img src="image\fastboot-devices_only.png" alt="fastboot-devices_only" />只有一个设备

4. 若使用临时启动方式，请输入"fastboot boot 路径名\\rec.img"（可将img文件直接拖拽到窗口中）<img src="image\fastboot-boot_path.png" alt="fastboot-boot_path" />

   回车出现"Finished"字样即为成功，手机会自动打开TWRP，点击"**高级-刷入当前TWRP**"即为刷入完成

5. 刷入Recovery分区，请输入"**fastboot flash recovery 路径名\\rec.img**" 并回车

   若是**VAB设备**，请先输入"fastboot flash recovery_a 路径名\\rec.img" 

   回车后再输入"fastboot flash recovery_b 路径名\\rec.img" 并回车，确保ab两个分区都刷入第三方REC
   最后手动重启或在电脑输入"fastboot reboot recovery"进入Recovery模式



## 刷入系统

**前言：此教程为从零开始刷机教程，请根据自己需求选择观看。**

**需要准备：系统包，电脑/手机TWRP。**

**此教程将说明：线刷/卡刷/半卡刷(ADB Sideload)**

**点此跳转对应刷入方式：**[线刷](#usb_flash)		[卡刷](twrp_flash)		[半卡刷](#2in1_flash)

<img src="image\system-package_name.jpg" alt="system-package_name" style="zoom: 80%;" />

**文件名为：Ext4_cmi_Mi10Pro_Cdrs_HyperOS1.0.15.0.UMACNXM(13U移植)_A14_da608.zip**

**分别为：系统格式 机型代号 机型名称 cdrs 系统版本 安卓版本 MD5校验码** 

[系统格式详情点此跳转](#sys_Format)		[机型代号详情点此跳转](#device_Code)

## <span id="usb_flash">线刷</span>

**首先请先检查您的系统包确认是否完整（[如何检查请点这里](#check_File)**）

1. 请先请现在群文件下载USB_Drive驱动并安装

2. 首先要把压缩包解压，并存放在一个位置，**路径中不能有中文和括号，如果有请删除它们**

3. 手机启动到fastboot模式并连接电脑，点击Cdrs一键线刷工具Flash.bat，并根据提示输入数字，最后等待重启即可

   <img src="image/fastboot-Flash.png" alt="fastboot-Flash" />

## <span id="twrp_flash">卡刷</span>

**首先请先检查您的系统包确认是否完整（[如何检查请点这里](#check_File)**）

**以下为第一次刷入所需的步骤**

1. 电脑下载好包 手机进rec，清除-右下角格式化data，输入yes，打✓
2. 等格式化完毕，重启一下rec。 （这操作是为了解密内置储存）
3. rec模式-手机连接电脑，把包复制进内置存储。
4. 刷完返回rec主页，清除-右下角格式化data，输入yes，打✓

**----- 以上为第一次输入所需步骤，以下为后续刷入步骤**

1. 手机下载好rom包，记住下载路径
2. 进入rec主页-安装，找到你记得路径，选择刷机包，滑动刷入，按提示操作
3. 重启开机

**出现一系列挂载失败的红字请无视，重启出现未安装系统请无视**

**只要出现“安装耗时******秒****”，上方显示<u>成功</u>即为刷入成功**
安装完成一般如下图所示

<img src="image\TWRP_flash.png" alt="TWRP_flash" style="zoom: 10%;" />


## <span id="2in1_flash">半卡刷(ADB Sideload)</span>

**首先请先检查您的系统包确认是否完整（[如何检查请点这里](#check_File)），并且确定已经配置ADB环境([点此查看如何配置](#adb_install))**

1. 手机进入rec界面，点击高级，ADB Sideload，滑动滑块

   <img src="C:\Users\shiyu\Desktop\CdrsRoms\image\ADB-Sideload.png" alt="ADB-Sideload" style="zoom:33%;" />

2. 连接电脑，在黑窗口输入"adb sideload 文件完整路径"(**不要解压，直接用zip压缩包**)

3. 回车，剩下的在手机上操作即可



# Root相关

## 使用Root的三种方式

### 出厂A13开始就要修补init_boot.img，A12及以下的修补boot.img

### Magisk（面具）

包自带Delta面具(即Kitsune Mask)，想要升降级就修补环境刷入即可

线刷指令：fastboot flash 对应分区 img镜像（[刷入方式详见刷入第三方rec](#flash_rec)）、



想刷其他面具版本可以参考：https://magiskcn.com/magisk-change

也可以下载并安装需要的面具，在原面具中把自动响应改为允许并给新面积root权限，最后到新面具修补即可

相关链接：[Magisk原版仓库](https://github.com/topjohnwu/Magisk)		[Kitsune Mask (Delta仓库)](https://github.com/HuskyDG/magisk-files)		[Magisk Alpha仓库](https://install.appcenter.ms/users/vvb2060/apps/magisk/distribution_groups/public)

### KernelSU（KSU）

**若使用KSU则原来所有Magisk模块都会被清楚，请自行考虑**

1. 准备支持KSU的内核，并下载安装KSU管理器（[点此跳转](https://github.com/tiann/KernelSU/releases)）
2. 刷入内核即可使用（若设备里有Magisk可以点击卸载Magisk-完全卸载即可）

相关链接&其他安装方法：https://kernelsu.org/zh_CN/guide/what-is-kernelsu.html

### Apatch



## 如何隐藏Root

## 关于模块想说的话

非必要不要刷一些玄学的优化模块，少刷模块别养蛊，**谨防格机模块，谨防格机模块，谨防格机模块，**救砖模块都救不了

# 备份相关

# 线刷官方教程-救砖

# 如何替换基带

**注意！请备份原基带！无论是多系统工具箱备份字库还是复制大法，请务必备份，推荐备份字库！请确保基带可在本机使用！** 

1. mt管理器进入/vendor/firmware_mnt/image/（没有备份请先备份！） 

2. 打开飞行模式，将下载好的基带文件替换进去 

3. 关闭飞行等一段时间（30秒），有信号了重启两次（其实一次就行，不知道为什么都说两次） 
  受当地网络环境和运营商的影响，请自行寻找合适的基带，请确保基带可在本机使用，请务必备份数据！

  推荐多系统工具箱备份整个字库！ 

# 常见问题

## 声音不大，音质一般

请将音质音效里的场景选择切换为人声

## <span id="check_File">如何校验文件完整性</span>

**在刷机或进行重要且有风险的操作之前，我们建议先校验文件确保其完整性**

<img src="image\TWRP-package_name.jpg" alt="TWRP-package_name" />

以文件名为 <u>[REC_BOOT]3.7.1_12-Mi10Pro_FBEv2_v8.6_A14-cmi-skkk_9d23a457.zip</u> 的文件为例

其中<u>9d23a457</u>为校验码，得到这串字符后我们便可去进行文件的校验和比对

#### 校验使用的操作系统（点击跳转）：[Windwos](#windows_Check)	[Android](#android_Check)	[Linux](#linux_Check)

-----

### <span id="windows_Check">Windows</span>

打开cmd，输入"**certutil -hashfile <文件名称(绝对路径)> MD5**"，回车即可校验

<img src="image\windows_check-md5.png" alt="windows_check-md5" />

红色框选处为命令，绿色即为得到的结果，将结果与文件对比，**数值完全一致即为完整，数值不一样则需要重新下载**



### <span id="android_Check">Android</span>

以MT管理器为例，**长按文件，依次点击属性-校验，比对md5是否与文件一致，不一致请重新下载后再次比对**<img src="C:\Users\shiyu\Desktop\CdrsRoms\image\android_check-md5.jpg" alt="android_check-md5" style="zoom:33%;" />





## 为什么线刷刷不进去

请排查您的问题，USB_Driver驱动有没有安装，是否为USB2.0数据线和接口，系统文件是否完整

## 为什么线刷电脑没反应，无法输入

请将手机进入fastboot模式并连接电脑

## <span id="adb_install">如何安装ADB</span>

1. [点此跳转到下载界面并下载对应系统的 Platform-Tools 工具包](https://developer.android.google.cn/tools/releases/platform-tools?hl=zh-cn#downloads)

2. 将下载好的压缩包解压出来，存放位置和命名随意，但请注意**不能删除或修改这个路径里的任意文件夹或文件**例如我存放在了"C:\D\develop\ADB\\"

   <img src="image\Platform-Tools_folder.png" alt="Platform-Tools_folder" />这个目录**此后这个路径和文件夹不能进行任何更改，否则按照接下来的步骤重新配置**

3. 打开这个文件夹并在顶部把路径**复制**下来

   <img src="image\adb-path_copy.png" alt="adb-path_copy" />

4. 按下Win键，在搜索栏输入"环境变量"打开或者依次打开"设置-系统信息-高级系统设置"，再点击环境变量，在**系统变量**中找到Path并双击打开

   <img src="image\environment-variable_path.png" alt="environment-variable_path" />

5. 点击"新建按钮"或点击下方空白栏，**将复制的路径粘贴进去，并一路点击确定**

6. 最后使用**Win+R键输入"cmd"回车**，在黑窗口输入**"adb version"**，若出现版本号即为成功配置<img src="image\cmd_adb-version.png" alt="cmd_adb-version" />

## FTP传输
