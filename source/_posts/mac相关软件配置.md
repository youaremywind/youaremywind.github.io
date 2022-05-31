---
title: mac相关软件配置
date: 2022-05-31 17:39:39
tags: mac
---
每次使用新的mac电脑，都需要安装和配置一大堆东西，那就都记录在这里吧，方便查看。

### U盘启动盘制作
电脑升级了最新的系统之后感觉有点卡，于是打算降级到Catalina。
官方是不支持降级的，那只能刷机了。
```shell
sudo /Volumes/Install\ macOS\ Catalina/Install\ macOS\ Catalina.app/Contents/Resources/createinstallmedia --volume /Volumes/macos
```
### iterm2
iTerm2 的安装，直接在官网下载安装。

官网地址： http://iterm2.com/downloads.html
其实自带终端也挺好的，用iterm2的原因是：
最初看见了这个视频
https://www.bilibili.com/video/BV1cf4y157sv?spm_id_from=333.337.search-card.all.click

### 配置 vim高亮显示
```
vim ~/.vimrc
//增加一行  syntax on
```

### oh-my-zsh
- linux alias 是命令的一种别称，输入
alias
可以看到像下面这样的结果：
alias vi="vim"
也即，输入vi后，被自动定向到vim这个命令了。alias的作用就是，可以简写命令。
- 一些插件
   + zsh-syntax-highlighting shell 命令可以高亮显示，便捷的知道你输入的命令是否正确。
   + zsh-autosuggestions 命令行自动补全插件

### brew
```shell
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```
#### 替换brew.git
```shell
cd "$(brew --repo)"
git remote set-url origin https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/brew.git
```
#### 替换homebrew-core.git
```shell
cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core"
git remote set-url origin https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/homebrew-core.git
```
#### 刷新源
brew update

#### 查看源
brew config

### GitHub 添加 SSHkey 
git config --global user.name "用户名"
git config --global user.email "邮箱"
ssh-keygen -t rsa -C "邮箱"
cat /Users/xxxx/.ssh/id_rsa.pub
添加到github
详情可以参考https://www.jianshu.com/p/1bb662f8b8d3