---
title: Archlinux + Raspberry 打造NAS  samba篇 
layout:  post  
categories: Archlinux Raspberry  
description: Archlinux 自动挂载移动硬盘，开机自动启动smb服务  
---


## Archlinux + Raspberry 打造NAS: samba篇

树莓派自动挂载硬盘，并开启smb服务。

### 开机自动挂在移动硬盘ntfs
1. 安装ntfs-3g
```shell
sudo pacman -S ntfs-3g
```
2. 修改fstab
```shell
sudo vim /etc/fstab
```
```
#
# /etc/fstab: static file system information
#
# <file system>	<dir>	<type>	<options>	<dump>	<pass>
/dev/mmcblk0p1  /boot   vfat    defaults        0       0
/dev/sda1       /mnt/tmp ntfs-3g defaults 0 0
```
说明，把/dev/sda1 挂在到/mnt/tmp 目录下，type为ntfs-3g
3. OK ，搞定，以后每次开机，树莓派都会自动挂在移动硬盘。请相应的修改参数，以便适合自己的系统

### 开启samba服务
1. 安装samba
```shell
sudo pacman -S samba
```
2. 配置
```shell
vim /etc/samba/smb.conf
```
配置文件末尾添加
```shell
[myshare]
   comment = video and audio
   path = /mnt/tmp
   public = yes
   browsable = yes
   writable = yes
   printable = no
   guest ok = yes
   create mask = 0765
```
保存并退出
3. 重启samba服务
```shell
sudo systemctl restart smbd.service
```
配置生效，这样局域网内，树莓派上的samba共享就建成了。
4. 开机自启
```shell
sudo systemctl enable smbd.service
```
