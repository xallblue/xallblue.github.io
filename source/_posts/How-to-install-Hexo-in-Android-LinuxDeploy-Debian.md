---
title: 在Android/LinuxDeploy Debian上安装hexo的坑
date: 2017-07-31 18:58:12
tags: 安装nodejs npm hexo
---
__要注意版本__
在Android/LinuxDeploy Debian上安装hexo之前，先要看一下nodejs和npm的版本是不是偏旧。
如果是用系统自带的安装sudo apt-get install nodejs npm，用node -v看一下版本，应该是0.10版的，需要更新为目前的6.x。
到官网上下载最新的binary文件，比如下载下来的文件是node-v6.11.1-linux-armv7l.tar.xz，而对于.tar.xz的文件解压方法如下：
_xz -d node-v6.11.1-linux-armv7l.tar.xz_
这个命令运行之后，node-v6.11.1-linux-armv7l.tar.xz变为了node-v6.11.1-linux-armv7l.tar，之后再用
_tar -xvf node-v6.11.1-linux-armv7l.tar_
运行上述命令之后，就能生成一个node-v6.11.1-linux-armv7l文件夹，解压成功，可以放在/opt下。
___
先备份一下原来的版本
_sudo mv /usr/local/bin/node /usr/local/bin/node.bak_
_sudo mv /usr/local/bin/npm /usr/local/bin/npm.bak_
方便起见，文件夹改个短名
_sudo mv /opt/node-v6.11.1-linux-armv7l /opt/nodev6_
建立符号链接
_sudo ln -s /opt/nodev6/bin/node /usr/local/bin/node_
_sudo ln -s /opt/nodev6/bin/npm /usr/local/bin/npm_
___
查看nodejs和npm版本正常，安装运行hexo
_sudo npm install hexo-cli -g_
_hexo --version_
_hexo init blog_
_cd blog_
_npm install_
___
_hexo n "something"_
编辑完后生成静态页面
_hexo g_
本地服务器查看一下，http://localhost:4000
_hexo s_
***
发布到github上，编辑好\_config.yml文件，确定已安装deploy组件，没有的话运行一下
_sudo npm Install hexo-deployer-git --save_
现在可以发布了
_hexo d_
