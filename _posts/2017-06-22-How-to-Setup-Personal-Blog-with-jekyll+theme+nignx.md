---
title: 如何是搭建博客（jekyll + 自定义主题 + nignx）
layout: post
categories: jekyll other
description: vps+nginx+jekyll 搭建自己私人博客的全过程
---


## 如何搭建自己的博客

### 一 购买vps
给大家推荐几个我自己使用过的VPS，体验上都还可以，  
搬瓦工，budgetVM， 阿里云

### 二 安装jekyll
1. 安装Ruby
    1. 安装rvm  
        https://www.rvm.io/  
```shell
     $gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB  
     $curl -sSL https://get.rvm.io | bash -s stable
```
    2. 安装Ruby  
        rvm install 2.4 (当前ruby2.4是最新版本)  
    3. 注意事项：  
        * 不需要sudo
        * 需要更新一下环境变量或者重启计算机才能使用rvm
2. 安装jekyll
```shell
        $ gem install jekyll  
        $ jekyll new myblog  
        $ cd myblog
        $ jekyll build --watch &
        $ jekyll serve （http://localhost:4000 仅本地预览）
```

### 三 安装nginx（以ubuntu为例）
1. ADD KEY   
```shell
    wget http://nginx.org/keys/nginx_signing.key  
    sudo apt-key add nginx_signing.key
```
2. ADD source    
```shell
deb http://nginx.org/packages/ubuntu/ codename nginx
deb-src http://nginx.org/packages/ubuntu/ codename ngin  
```
其中 codename 见下表  

Version|Codename|	Supported Platforms
          ---|---|---
        12.04	|precise|	x86_64, i386
        14.04	|trusty	|x86_64, i386, aarch64/arm64
        16.04	|xenial	|x86_64, i386, ppc64el, aarch64/arm64
        16.10	|yakkety	|x86_64, i386  

### 四 Nignx与jekyll结合
1. 配置nginx  
`vim /etc/nginx/config.d/defautl.conf`  
在server{} 代码块中 修改
  * `listen 800;`
  * `location /{   
    root /xxxx/xxxx/myblog/\_site; }`
2. 重启nginx  
`sudo nginx -s reload`

### 五 更换主题
到现在为止我们的博客已经新建完成了。但是现在是最简单的博客。连首页都没有，文章之间跳转链接都没有，不过别担心，我们可以用借鉴别人的代码
1. git clone https://github.com/mzlogin/mzlogin.github.io.git
2. cp 所有的文件到我们的博客目录， myblog
3. cd myblog && gem install  
4. jekyll build
5. 预览一下，是不是已经换了码志的主题了.

### 六 修改配置
1. 删除_post, image目录下的内容
2. 修改_config.yml, about.md 等。
3. 请参考https://github.com/mzlogin/mzlogin.github.io
