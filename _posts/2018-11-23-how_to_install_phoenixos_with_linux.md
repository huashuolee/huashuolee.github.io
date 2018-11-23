---
title: Linux系统下如何安装phoenixos
layout:  post  
categories: phoenixos
description: linux系统下如何安装phoenixos
---


## How to install PhoenixOS on Ubuntu

1. Create a root directory
```shell
sudo mkdir -p /PhoenixOS/data
```

2. Extract the android_x86_64.7z and copy all the files to "PhoenixOS" folder      
![screenshot](/images/posts/phoenixos_installation/screenshot_install_phoenixos.png)

3. Generate boot menu
```shell
sudo vim /etc/grub.d/40-custom
```
and add below content,
```shell
menuentry 'Phoenix OS' --class android-x86 {
# replace the "hd0,gpt5" to your own config
set root='hd0,gpt5'
#search --file /Phoenixos/kernel
linux /PhoenixOS/kernel quiet root=/dev/ram0 SRC=/PhoenixOS vga=auto androidboot.selinux=permissive buildvariant=userdebug
initrd /PhoenixOS/initrd.img
}
```
regenerate boot configuration file
```shell
sudo grub-mkconfig -o /boot/grub/grub.cfg
```

4. Reboot  
![screenshot](/images/posts/phoenixos_installation/success.png)
