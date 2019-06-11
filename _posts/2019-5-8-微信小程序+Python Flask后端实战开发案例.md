---
layout:     post
title:      微信小程序+Python Flask后端实战开发案例
subtitle:   微信小程序+Python Flask后端实战开发案例
date:       2019-05-08
author:     BOBO
header-img: img/post-bg-re-vs-ng2.jpg
catalog: true
tags:
    - 小程序
---

# 微信小程序安装
## 因为作者操作系统是Ubuntu16.04 所以在安装小程序开发平台时也踩了不少坑 
### 首先
#### 下载项目和初始化
```
git clone https://github.com/cytle/wechat_web_devtools.git
```
##### 下载的文件大小大概800多mb
##### 所以我为大家准备了压缩包 方便大家快速下载大概400mb左右
网盘地址链接: https://pan.baidu.com/s/1dgWK8dx8S6TyDgxr1P8vUw 提取码: ifeb 复制
```
cd wechat_web_devtools # 解压文件并进入文件目录
```
```
 # 自动下载最新 `nw.js` , 同时部署目录 `~/.config/wechat_web_devtools/`
./bin/wxdt install
```
#### 启动
```
./bin/wxdt # 启动
```
#### 这时还没有完,如果在系统中没有wine这个软件,那么在代码渲染时会报错,所以没有就要安装wine
#### wine安装
##### 建议安装wine1.6
```
sudo apt-get install wine1.6
# 安装的时候会出现选择 用键盘的左右建操控 然后回车选yes
```
```
查看显示wine-1.6.2
命令:wine --version
```
```
# 安装完记得配置
winecfg 
```

