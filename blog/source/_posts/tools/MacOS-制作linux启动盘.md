---
title: MacOS 制作 linux 启动盘
top: 0
date: 2020-03-22 22:24:00
tags: tools
# thumbnail: /../images/frontend.png
toc: true
# comment: true
categories:
---

最近需要学习 MIT 的 Operating System Engineering 课程，需要 ubuntu 的实验环境，正好家里有台旧笔记本，常常因为运行 windows 造成发热自动关机，正常情况下使用 linux 应该还好一些。手上只有 Mac 去做启动盘，虽然简单但是也有一个坑，记录一下

<!-- more -->

## 准备

-   大于 4g 优盘
-   linux 系统 iso 镜像 `ubuntu-amd64.iso`

## 格式化 usb 硬盘

-   打开 Mac 磁盘管理工具，点击优盘，选择抹去
-   ![抹掉硬盘](/../images/tools/mac-iso-tool.png)

## 取消磁盘挂载

```
# 终端执行以下命令
# 列出磁盘，找到你usb硬盘的盘符
diskutil list

# 输出如下：可以看到usb硬盘为/dev/disk2
/dev/disk0 (internal):
   #:                       TYPE NAME                    SIZE       IDENTIFIER
   0:      GUID_partition_scheme                         251.0 GB   disk0
   1:                        EFI EFI                     314.6 MB   disk0s1
   2:                 Apple_APFS Container disk1         250.7 GB   disk0s2

/dev/disk1 (synthesized):
   #:                       TYPE NAME                    SIZE       IDENTIFIER
   0:      APFS Container Scheme -                      +250.7 GB   disk1
                                 Physical Store disk0s2
   1:                APFS Volume Macintosh HD            125.9 GB   disk1s1
   2:                APFS Volume Preboot                 67.5 MB    disk1s2
   3:                APFS Volume Recovery                1.0 GB     disk1s3
   4:                APFS Volume VM                      6.4 GB     disk1s4

/dev/disk2 (external, physical):
   #:                       TYPE NAME                    SIZE       IDENTIFIER
   0:     FDisk_partition_scheme                        *16.0 GB    disk2
   1:                       0xEF                         6.4 MB     disk2s2

# 取消usb硬盘的挂载
diskutil unmountDisk /dev/disk2
```

## 导入镜像

```
# 执行如下命令，注意 xxx 为你的系统名称
sudo dd if=~/Users/xxx/Downloads/ubuntu-amd64.iso of=/dev/disk2 bs=2m

# if是镜像文件路径，of是导入的目的磁盘
# bs是读写快的大小，太小会增大io，降低效率，一般1m～2m即可。

# 成功会提示
1014+1 records in
1014+1 records out
2126544896 bytes transferred in 814.543111 secs (2610721 bytes/sec)
```

同时系统会弹出一个错误的窗口，是因为 Linux 的分区格式是 ext，在 macOS 系统下无法识别才会报错，但是其实一个支持 UEFI 引导的 Ubuntu 启动优盘已经制作成功了，点击 Ignore 忽略或者 Eject 退出 U 盘

## 注意：

上面的路径最好是 linux iso 镜像的绝对地址，我放在 Mac 的 Downloads 里`sudo dd if=~/Downloads/ubuntu-amd64.iso of=/dev/disk2 bs=2m`，虽然有教程说可以直接使用，但是我这边会报错 `dd: /Downloads/ubuntu-amd64.iso: No such file or directory`，必须在 /Downloads 的前面加上 /Users/xxx 才可行。
