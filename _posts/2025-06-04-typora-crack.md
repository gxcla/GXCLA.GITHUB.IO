---
title: Typora 0.11.18 版本破解
layout: post
category: article
description: 网上各种Typora破解补丁，不能放心食用，自己折腾了一下Typora 0.11.18 破解过程，没有任何补丁，可以放心食用！
---

# 安装

网上各种Typora破解补丁，不能放心食用，自己折腾了一下Typora 0.11.18 破解过程，没有任何补丁，可以放心食用！

1.软件

找到官网的安装包 typora-update-x64-1117.exe

2.更改默认位置

软件默认安装到C盘中，打开windows电脑中的win+R ，输入regeidt ，找到

`计算机\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion`

windows更改软件默认安装位置
64位：ProgramFilesDir
32位：ProgramFilesDir (x86)

3.删除 profile.data

typora安装之后，会在C:\\[Users]\AppData\Roaming\Typora 文件夹下生成一个profile.data文件，键入`%appdata`可以找到，这个文件用于判断是否版本过期，先删除它

4.注册表权限

拒绝Typora的所有权限 ，win+R ，输入regeidt ，找到 `计算机\HKEY_CURRENT_USER\Software\Typora` 右键拒绝所有权限

