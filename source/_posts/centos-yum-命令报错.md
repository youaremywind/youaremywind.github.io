---
title: Centos8使用yum命令报错
date: 2022-06-01 13:09:41
tags: centos
---

今天想起来还有台服务器，于是准备安装一下docker,回顾一下之前学习的知识。

执行命令：
```shell
curl -sSL https://get.daocloud.io/docker | sh
```
运行了结果报错：Failed to download metadata for repo ‘AppStream’: Cannot download repomd.xml: Cannot download repodata/repomd.xml: All mirrors were tried
那么百度一下：

原因：2022年1月1日起CentOS官方将不再对CentOS 8提供服务支持,虽然系统可以正常使用,但CentOS 8的yum源已经移除无法使用了,使用yum安装会报错

按顺序执行一下命令即可解决：
1、执行如下命令先将之前的yum文件备份：
```shell
rename '.repo' '.repo.bak' /etc/yum.repos.d/*.repo
```
2、运行以下命令下载最新的repo文件：
```shell
wget https://mirrors.aliyun.com/repo/Centos-vault-8.5.2111.repo -O /etc/yum.repos.d/Centos-vault-8.5.2111.repo
```
```shell
wget https://mirrors.aliyun.com/repo/epel-archive-8.repo -O /etc/yum.repos.d/epel-archive-8.repo
```
3、运行以下命令替换repo文件中的链接：
```shell
sed -i 's/mirrors.cloud.aliyuncs.com/url_tmp/g'  /etc/yum.repos.d/Centos-vault-8.5.2111.repo &&  sed -i 's/mirrors.aliyun.com/mirrors.cloud.aliyuncs.com/g' /etc/yum.repos.d/Centos-vault-8.5.2111.repo && sed -i 's/url_tmp/mirrors.aliyun.com/g' /etc/yum.repos.d/Centos-vault-8.5.2111.repo
```
```shell
sed -i 's/mirrors.aliyun.com/mirrors.cloud.aliyuncs.com/g' /etc/yum.repos.d/epel-archive-8.repo
```
4、运行以下命令重新创建缓存,若没报错,则正常了
```shell
yum clean all && yum makecache
```

结果又报错了
Errors during downloading metadata for repository 'epel-archive':
  - Curl error (6): Couldn't resolve host name for http://mirrors.cloud.aliyuncs.com/epel-archive/8/Everything/x86_64/repodata/repomd.xml [Could not resolve host: mirrors.cloud.aliyuncs.com]
Error: Failed to download metadata for repo 'epel-archive': Cannot download repomd.xml: Cannot download repodata/repomd.xml: All mirrors were tried
那再百度下：
因为所用系统为Centos 8版本，暂时（此时为2022-03-16）已停止更新相应依赖，

于是按照下面操作，解决问题

1、备份源文件夹
```shell
mv /etc/yum.repos.d /etc/yum.repos.d.bak
```
2、创建源文件目录
```shell
mkdir -p /etc/yum.repos.d
```
3、下载新的yum源
```shell
curl https://mirrors.aliyun.com/repo/Centos-vault-8.5.2111.repo > /etc/yum.repos.d/Centos-vault-8.5.2111.repo
```
```shell
curl https://mirrors.aliyun.com/repo/epel-archive-8.repo > /etc/yum.repos.d/epel-archive-8.repo
```
4、重建缓存
```shell
yum clean all && yum makecache
```
最后成功解决！！

参考网站：
https://blog.csdn.net/burgerh/article/details/123098751

https://blog.csdn.net/qq_39835505/article/details/124840390