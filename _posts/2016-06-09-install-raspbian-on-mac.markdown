---
layout: post
title:  "Mac下给SD卡安装 Raspbian 系统"
date:   2016-06-09
desc: "install Raspbian to micro-sd on mac"
keywords: "mac,install,raspbian,micro-sd"
categories: [Life]
tags: [Raspbian]
icon: icon-debian
---

## 1、安装

### 系统下载地址

插入SD卡，使用 df 查看当前已经挂载的卷

```
$ df
Filesystem    512-blocks      Used Available Capacity  iused   ifree %iused  Mounted on
/dev/disk1     233269248 218788512  13968736    94% 27412562 1746092   94%   /
devfs                374       374         0   100%      648       0  100%   /dev
map -hosts             0         0         0   100%        0       0  100%   /net
map auto_home          0         0         0   100%        0       0  100%   /home
/dev/disk2s1    31100416      4992  31095424     1%        0       0  100%   /Volumes/Pi
```

因为已经命名了SD卡为 Pi ，所以SD卡的分区对应的设备文件为：/dev/disk2s1

使用diskutil unmount卸载

```
$ diskutil unmount /dev/disk2s1
Volume Pi on disk2s1 unmounted
```

diskutil list 确认设备 我买的是16G的卡

```
$ diskutil list
/dev/disk2
   #:                       TYPE NAME                    SIZE       IDENTIFIER
   0:     FDisk_partition_scheme                        *15.9 GB    disk2
   1:                 DOS_FAT_32 Pi                      15.9 GB    disk2s1
```

使用dd命令将系统镜像写入

PS /dev/disk2s1是分区，/dev/disk2是块设备，/dev/rdisk2是原始字符设备

```
$ dd bs=4m if=pi.img of=/dev/rdisk2
781+1 records in
781+1 records out
3276800000 bytes transferred in 194.134151 secs (16879050 bytes/sec)
```
