---
title: 树莓派如何使用USB转RJ45千兆有线网卡
layout:  post  
categories: Raspberry
description: 树莓派如何使用USB转千兆网卡
---  
使用USB转千兆有线网卡提高树莓派的网络性能  
 

## Summary
树莓派的网口只有百兆，已经无法满足平时使用的需求了。正好手里有2个usb转RJ45的千兆有线网卡

## Steps
1. 把网线，转换器，usb连接好
2. lsusb
```shell
Bus 001 Device 006: ID 05e3:0702 Genesys Logic, Inc. USB 2.0 IDE Adapter [GL811E]
Bus 001 Device 007: ID 0bda:8153 Realtek Semiconductor Corp. RTL8153 Gigabit Ethernet Adapter
Bus 001 Device 005: ID 05e3:0610 Genesys Logic, Inc. 4-port hub
Bus 001 Device 004: ID 046d:c534 Logitech, Inc. Unifying Receiver
Bus 001 Device 003: ID 0424:ec00 Standard Microsystems Corp. SMSC9512/9514 Fast Ethernet Adapter
Bus 001 Device 002: ID 0424:9514 Standard Microsystems Corp. SMC9514 Hub
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
```
你会发现 RTL8153 Gigabit Ethernet Adapter 已经被正确识别到，OK驱动支持，咱们就不用费劲装驱动了。
3. 自动获取ip地址
```shell
cd /etc/systmed/network
```
你会发现有个默认的eth0.network,
```shell
cp eth0.netwrok eth1.network
sudo vim eth1.network
按照下面的内容进行修改
[Match]
Name=eth1
[Network]
DHCP=yes
```
4. 重启服务
```shell
sudo systemctl restart systemd-networkd.service
```

## Testing
用iperf测试一下带宽,总的来说都比树莓派自带百兆网口快很多
1. 绿联千兆网卡，芯片AX88179，实测带宽200M，京东售价79RMB，使用时不稳定
2. IT-CEO千兆网卡，芯片RTL8153，实测带宽300M，京东售价99RMB，推荐使用

### 参考文章
* https://wiki.archlinux.org/index.php/Systemd-networkd#Basic_DHCP_network
