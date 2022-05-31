---
title: mac恢复模式u盘拷文件到系统磁盘
date: 2019-10-18 13:02:19
tags: mac
---

之前写的那篇clean my mac 卸载 teamviewer 导致系统不能开机了 。那么怎么将文件传进去呢？方法很多两台mac连着 然后传文件 因为这个线一般人都没有，所有pass 。
1、我是使用丢在服务器上，然后联网下载。注意文件的权限，http访问不到那个资源，curl会把403页面下下来了，改成了tar后缀。
2、网上的方法是使用 U 盘拷的，比如说需要的文件夹 TeamViewerAuthPlugin.bundle 就在 /Volumes/u盘名字/ 里面，我要拷到 /Volumes/Macintosh HD/Library/Security/SecurityAgentPlugins/ 路径下。如果提示 Macintosh HD 是 read-only，那就拷到 /Volumes/Macintosh HD - Data/Library/Security/SecurityAgentPlugins/ 路径下，没有文件夹的话就创建文件夹，这个路径是不用 sudo的。