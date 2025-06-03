---
title: 如何查看内存条是几代？ddr3还是ddr4
layout: post
category: article
---
## 一、外观

每一代的内存条模组卡槽的位置不同。可以通过卡槽的位置稍有差异来判断，这样的设计以便防止将模组安装到不兼容的主板或平台中。

![](https://cdn.GXC.LA/images/986dec176899e510fb3094c.png)

## 二、任务管理器

在Windows系统中查看计算机内存是几代，无需依赖第三方工具，仅需借助系统自带工具即可。

对于Windows 10或11用户，请执行以下操作：

1. 同时按下Ctrl+Alt+Del，选择“任务管理器”。

2. 转至“性能”选项卡，然后选择“内存”。


在“速度”一栏中，内存频率区间在1600~2400MHz的表示DDR3，同时内存大标题旁标注“DDR3”。相反，频率区间在2133~4400MHz的内存则为DDR4，具体如3200MHz，这通常被推断为DDR4类型，。

## 三、命令工具

更精确的确认需要借助WMIC命令行工具

1.按下Win+R键，输入cmd ，然后回车，打开CMD窗口

2.在CMD窗口中输入下方查询代码，然后回车

```
wmic memorychip get Speed,SMBIOSMemoryType
```

3.查看SMBIOSMemoryType值，24对应DDR3，26对应DDR4，34对应DDR5。

![](https://cdn.GXC.LA/images/p97173733.jpg)

通过以上步骤，可以直观地在Windows系统中判断出计算机所使用的内存类型，即DDR5、DDR4或DDR3。
