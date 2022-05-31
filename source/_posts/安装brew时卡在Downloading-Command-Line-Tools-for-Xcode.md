---
title: 安装brew时卡在Downloading Command Line Tools for Xcode
date: 2022-05-31 19:09:43
tags: mac
---

Press RETURN/ENTER to continue or any other key to abort:
==> /usr/bin/sudo /usr/sbin/chown -R kingsley:admin /usr/local/Homebrew
==> Searching online for the Command Line Tools
==> /usr/bin/sudo /usr/bin/touch /tmp/.com.apple.dt.CommandLineTools.installondemand.in-progress

卡在这一步骤时，可以去https://developer.apple.com/download/more/上登陆，下载对应版本（Xcode-11.4.1）的Command Line Tools ，然后手动安装。