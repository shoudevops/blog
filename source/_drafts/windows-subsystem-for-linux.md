---
title: Windows Subsystem for Linux(WSL) 環境配置
categories:
- Windows
- WSL
tags:
- linux
- windows
- wsl
---
原先在尋找Windows 有什麼好用的Terminal 軟體，就找到了WSL ，一個能直接在Windows 上使用Linux 指令操作系統。
本篇文章簡單紀錄如何配置WSL 環境，後續會在其它文件針對好用的工具進行說明。

### WSL 原理
想要瞭WSL 背後運作的原理，可以參考：[Windows Subsystem for Linux Overview](https://docs.microsoft.com/zh-tw/archive/blogs/wsl/windows-subsystem-for-linux-overview)這篇官方文章，或是這篇：[Windows for Linux Nerds](https://blog.jessfraz.com/post/windows-for-linux-nerds/)一位Microsoft員工的文章。

<!-- more -->

基本上是可以讓Linux ELF64 binary文件透過WSL 在Windows 運行的元件，包含User Mode 與Kernel Mode，
主要包括：
1. User Mode 的Session Manager Service處理Linux Instance 生命週期
2. Pico Provider 驅動元件(lxss.sys, lxcore.sys)透過轉換Linux 系統調用來模擬Linux kernel
3. Pico Processes 管理未修改的User Mode Linux(e.g. /bin/bash)

透過在Pico Processes中放置未修改的Linux binary文件，使Linux 系統調用可以導向到Windows Kernel，
lxss.sys, lxcore.sys驅動元件將Linux 系統調用轉換為Windows NT 的APIs 並模擬Linux Kernel
{% asset_img wsl-components.jpg WSL Components %}

更多細節可以參閱原文。

### 啟用WSL
在新版（1909）的Windows 版本中，啟用WSL 不再需要開啟開發者模式，
只要直接從【控制台】→【程式和功能】→【開啟或關閉Windows 功能】中，
將【適用於Linux 的Windows 子系統】功能打勾就能開啟：
{% asset_img enable-wsl-with-ui.jpg Enable WSL with Control Panel %}

也可以透過PowerShell 以系統管理員身份下指令：
```
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
```

### 安裝WSL Distro
開啟Microsoft Store 搜尋Linux，可以找到所有WSL 散發版本：
{% asset_img store-wsl-distro.jpg WSL Distro in Microsoft Store %}

如果無法使用 Microsoft Store 應用程式，也可以按一下下列連結，下載並手動安裝 Linux 散發版本：
+ [Ubuntu 20.04](https://aka.ms/wslubuntu2004)
+ [Ubuntu 18.04](https://aka.ms/wsl-ubuntu-1804)
+ [Ubuntu 16.04](https://aka.ms/wsl-ubuntu-1604)
+ [Debian GNU/Linux](https://aka.ms/wsl-debian-gnulinux)

其它版本與安裝方法可以到[官網查看](https://docs.microsoft.com/zh-tw/windows/wsl/install-manual)
安裝後只算完成第一步，接下來還必須從【Microsoft Store】或【開始】中打開對應的Linux 散發版本，
本文以【Ubuntu】做示範，開啟後等待數分鐘的初始化，
接著設定好Linux User 的帳號、密碼即可完成安裝，並會自動進入Ubuntu 環境
{% asset_img initial-linux.jpg Initial and install Linux %}

也可以開啟`PowerShell`或`Command Prompt`，輸入下列指令進入Ubuntu
```
wsl
```

WSL 環境配置就到這裡完成了，開始享受在Windows 使用Linux Command吧！