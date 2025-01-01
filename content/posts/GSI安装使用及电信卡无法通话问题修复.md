---
title: "GSI 安装使用及电信卡无法通话问题修复"
date: 2022-09-12
tags: ["搞机", "安卓"]
categories: 技术
---

> 本文搬运自原个人博客。  
> 因年代久远，电信卡修复方案在最近的 GSI 刷机包中可能无法使用。刷基于 Android 12 的包应该是能用的。  
> 安装前提条件：一台能使用 fastboot 命令的电脑，一台支持 Project Treble 并已解锁 Bootloader 的手机

## 下载

首先判断设备是否支持 Project Treble，然后下载 GSI 镜像。需要注意的是，一般同一个 GSI 镜像会有多个不同版本，大致区别如下：

| 后缀     | 对应               |
| -------- | ------------------ |
| A64      | AArch64 架构 CPU   |
| ARM64    | ARM64 架构 CPU     |
| b        | a/b 分区           |
| a        | aonly 分区         |
| g        | 带有谷歌全家桶     |
| v        | 不带有谷歌全家桶   |
| N        | 不自带超级用户权限 |
| S        | 自带超级用户权限   |
| slim     | 精简版本           |
| vndklite | 带有 vndk 支持     |

例如需要使用 ARM64 架构，a/b 分区，带有谷歌套件的 crDroid 8.5，则应选择：

```
crDroid-8.5-arm64_bgN-Unofficial.img.xz
```

## 刷入

第一次刷入可能需要在官方系统下进行，之后则不需要。

确保电脑上有安装 fastboot，可通过 `fastboot -v` 检测。在手机上进入 fastboot 模式并连接电脑，在电脑上执行：

```
fastboot reboot fastboot
```

手机将会重启进入 fastbootd 模式。将下载好的 GSI 文件解压，直至单个 img 文件。随后执行：

```
fastboot erase system
fastboot flash system 解压的/文件/位置路径
```

在命令运行结束之后，清除 data 并重启：

```
fastboot erase userdata
fastboot reboot
```

### 无法开机？

无法开机的原因有很多。可以重复一遍以上操作，判断是否为操作失误。若并非操作失误，检查 GSI 包后缀是否与自己的手机相匹配，尤其是架构和分区类型。另外，可以更换无 vndklite 后缀的 GSI 包刷入测试。

## 电信卡的使用

按照以下流程操作：

1. 打开设置
2. 选择 Phh Treble Settings
3. 选择 IMS features
4. 勾选 Force the presence of 4G calling
5. 点击 Install IMS APK
6. 等待下载完成后，在通知中心点击安装并重启
7. 打开设置
8. 选择 网络和互联网
9. 点击 互联网
10. 点击第一项旁边的齿轮
11. 下滑找到 VoLTE
12. 关闭并重新打开（重启手机后需要再次重开该选项）
