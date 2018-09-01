---
title: nodejs & node & npm & n & nvm 安装
date: 2018-08-31 16:42:27
tags:
categories:
- [install & config]
- [front-end]
---

## 介绍
#### nodejs
node.js 是 javascript 的一种运行环境，是对 Google V8 引擎进行的封装。是一个服务器端的 javascript 的解释器。
reactNative 开发过程中所需要的代码库。
安装 nodejs 的时候会包含 npm。

#### node
node 和 nodejs 其实是同一个东西，查看会发现，一般一个是另一个的软链接而已。

#### npm
是 nodeJs 的包管理工具，npm 管理对应 nodeJs 的第三方插件。
* 安装 npm 一定要先安装 nodejs 吗？
npm is an app written entirely in JavaScript and depends very heavily on Node.js APIs (and other pure-JavaScript packages that in turn depend on Node.js APIs). Because Node.js is a scripting platform running a dynamic language (just like Python, Ruby, or Perl), apps written atop it need to have access to the binary to run. Having Node installed is a prerequisite for that reason. Because this is how npm works.


#### nvm & n
n 是 nodejs 的版本管理工具,管理nodejs版本和npm版本。
nvm 是 mac 上的，Linux 上可以使用 n。
<!--more-->

## 系统版本
* ubuntu 16.04

## 安装方式
* 去官网直接下载：
https://nodejs.org/en/
* 使用`apt-get`安装
*

### 直接使用`apt-get`安装nodejs & npm
`sudo apt-get install nodejs`
`sudo apt-get install npm`
但是会发现安装的版本不是最新的，是很低的版本，但接下来可以使用n做版本管理。
当然也可以直接去官网下载最新的版本，或者添加其他源来下载最新的版本。


### 使用npm管理安装包
* 使用npm install的包位置:
https://stackoverflow.com/questions/5926672/where-does-npm-install-packages
1) global libraries:
可以使用`npm list -g`查看安装包位置，
默认在`/usr/local/lib/node_modules`中
2) non-global libraries:
可以使用`npm list`查看安装包的位置，一般在当前目录下。


### 使用n(mac上可以使用nvm)管理node版本
* 前提是必须安装了npm
可以使用刚才`sudo apt-get install npm`的方式先安装一个低版本的npm。

* 安装n:
`sudo npm install n -g`
发现n被安装在了`/usr/local/lib/node_modules`中

* 使用n下载nodejs:
查看所有可安装的版本:
`n list`
安装使用nodejs的版本号为version的版本：
`sudo n version`
安装使用nodejs的stable版本:
`sudo n stable`
安装使用nodejs的latest版本:
`sudo n latest`
安装使用nodejs的lts(long term support)版本：
`sudo n lts`

* nodejs & node
但是安装完成之后会发现`node --version`已经是最新的了，但是`nodejs --version`还是老版本的。
使用`which node`和`which nodejs`查看可以看到：
node的位置是`/usr/local/bin`，而nodejs的位置是`/usr/bin`。这是因为使用`sudo apt-get install nodejs`的时候在`/usr/bin`下建立了node和nodejs可执行文件，但是使用`sudo n version`安装的时候在`/usr/bin`下只生成了node的可执行文件，并没有nodejs。
**使用`echo $PATH`可以看到，`/usr/local/bin`的优先级是高于`/usr/bin`的**，所以在`/usr/local/bin`中有node的时候，选择了这个node，但是`/usr/local/bin`没有nodejs，所以选择了`/usr/bin`中的nodejs。
解决办法也很简单，在`/usr/local/bin`中建立一个nodejs的软链接就可以了：`sudo ln -s /usr/local/bin/node /usr/local/bin/nodejs`

* `sudo n version`安装的包在哪里
发现`/usr/local/bin`中也只有当前使用的一个node版本，而`/usr/local/bin/npm`中的npm也是一个软链接指向了`/usr/local/lib/node_modules/npm`（这个位置是`npm install -g`的默认位置），这里也只有当前使用的npm版本，那么安装的那么多版本放在哪里了？
n install的工作方式是这样的：在安装的时候，n 会先将指定版本的 node 存储下来，然后将其复制到我们熟知的路径 /usr/local/bin。而存储的位置在安装的时候可以看到，在`/usr/local/n/version`，每次激活一个版本就会将该版本对应的node和npm复制到对应的`/usr/local/bin/node`和`/usr/local/lib/node_modules/npm`的位置。
