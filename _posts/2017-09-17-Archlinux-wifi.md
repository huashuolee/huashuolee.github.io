---
layout: post
title: Archlinux Raspberry 开机自动连接wifi，遇到的问题汇总
categories: Archlinux Raspberry
description: Archlinux 开机自动连接wifi
---

## Archlinux 开机自动连接WIFI

### 问题列表


1. 使用wifi-menu 无法连接wifi报错：  
【原因分析】因为interface is up， 先把interface关闭，再使用wifi-menu    
【解决方法】
{% highlight shell %}
    1. sudo ip link set wlp2s0 down  
    2. sudo wifi-menu
    {% endhighlight %}
2. 开机自动连接wifi失败的原因。  
【原因分析】之前配置的时候失败了，导致现在一直失败，而且我把原来的profile(比如叫做 wlan0-fail)都删除了。导致根本没办法disable。  
【解决方法】
    1. 使用wifi-menu成功连接无线， 在/etc/netctl/下得到正常的profile，比如叫做 wlan0-test
    2. sudo netctl enable wlan0-test 开机自启
    3. cp wlan0-test wlan0-fail, sudo netctl disable wlan0-fail（复制一个原来的fail的profile并disable）
    4. sudo reboot

###  常用命令

{% highlight shell %}
* systemctl --failed  
* systemctl list-unit-files --type=service
* systemctl start/stop/reload   
* systemctl enable/reenable/disable 开机自动启动
{% endhighlight %}
