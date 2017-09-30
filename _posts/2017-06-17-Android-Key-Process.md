---
layout: post
title: 【转】Android关键进程 
categories: Android
description: Android 关键进程
---


###### 参考：http://gityuan.com/about/

## PS 命令简介: 


1. 安卓PS命令接口的源 码在 system/core/toolbox/ps.c
2. 字段含义：
    * user：进程的当前用户，
    * PID， process ID
    * ppid-process parent id
    * vsize-VirtualSize
    * RSS-
3. 需要搜索的问题?
    * 什么是用户时间，什么是系统时间。什么是进程消耗的CPU时间


## 系统启动架构图：
Loader --> Kernel --> Native --> Framework --> App

![系统架构图](/images/posts/android-boot.jpg)

## 关键进程：
* 父进程，在所有进程中，以父进程姿态存在的进程  ，
     1. kthreadd：所有内核进程的父进程，
     2. init：所有用户进程的父进程，
     3. zygote：所有上层java进程的父进程
* 关键进程：
    1. system_server: 有zygote孵化而来，托起整个java framework的所有service，如，AMS,PMS；
    2. mediaserver， 由init孵化而来，托起整个多媒体C++ framework的所有service，如，audioflinger，
    3. mediaplayerservice； servicemanager： 有init孵化而来，是整个binder架构（IPC）的大管家，所有大大小小的service都需要先请示servicemanager

## 2号进程：
kthradd进程，是linux系统的内核进程，是所有内核进程的鼻祖，内核进程都不存在子进程与子线程，并且所有的内核进程的用户都是root

进程名|解释
------|-----
ksoftirqd|软中断
kworkder|内核工作县城
Migration|迁移进程
watchdog|看门狗
binder|进程间通信
rcu_sched|内核同步时加锁
perf|内核下系统调试工具
netns|网络虚拟化
mpm|
writeback|处理cache数据的刷新工作
system|
irq|中断
kgsl-events|图形驱动
spi|总线驱动
therm_core:noti|
msm_thermal:hot|


## 1号进程：
init进程（1号进程），是Linux系统的用户空间进程，或者说是android的第一个用户空间进程。

进程名 | 进程文件 | 作用
-------|-------|-----
zygote | /system/bin/app_process  | java界第一个进程，分32bit和64bit
servicemanager | /system/bin/servicemanager  | binder的守护进程
media | /system/bin/mediaserver  | 多媒体服务进程
ueventd|/sbin/ueventd|ueventd守护进程
healthd|/sbin/healthd|电池的守护进程
logd|/system/bin/logd|log的守护进程
adbd|/sbin/adbd|adb进程，socket IPC
lmkd|/system/bin/lmkd|lowmemorykiller守护进程
vold|/system/bin/vold|volume守护进程
netd|/system/bin/netd|network守护进程
debuggerd|/systme/bin/debuggerd|用于调试程序异常退出
ril-daemon|/system/bin/rild|Radio Interface Layer的守护进程
installd|/system/bin/installd|安装守护进程
surfaceflinger|/system/bin/surfaceflinger|UI帧相关的进程
