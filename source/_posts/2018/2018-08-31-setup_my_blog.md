---
title: Hexo + Next + github + Atom 博客搭建
date: 2018-08-29 19:29:27
tags:
categories:
- [install & config]
- [front-end]
---

## 使用的系统及版本
* ubuntu 16.04

## 安装需要
* git管理工具 & github帐号
* nodejs & npm

## nodejs & npm 安装

## Hexo安装

## github配置

## Next配置

## Atom做后台管理

### 插入图片
* 直接在source目录下新建一个images文件夹，存放`image.jpg`
因为使用了二级域名`/blog`,所以
`![](/blog/images/image.jpg)`
* 在`_config.yml`中
只在文章页面可以正常显示，在主页面无法显示：
`<img src="image.jpg">`,`![](/blog/images/image.jpg)`
在主页面也可以正常显示：
`{% asset_img image.jpg %}`
