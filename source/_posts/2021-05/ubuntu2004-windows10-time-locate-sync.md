---
title: Ubuntu-20.04 與Windows 10 系統時間同步
categories: Linux
tags: linux
date: 2021-05-03 09:17:41
---

安裝Ubuntu-20.04 時，已經有設定系統的時區，這時候Ubuntu 的系統時候是正確的；
但切換到Windows 10，會發現系統時間少了8小時。

### 概念

UTC時間，即`Universal Time Coordinated`，稱為`世界協調時間`
GMT時間，即`Greenwich Mean Time`，稱為`格林威治平均時間`

<!-- more -->

Windows 與Unix/Linux 看待系統硬體時間的方式是不同的：
- Windows 10 的系統時間會將BIOS的時間設為本地時間，所以Winodws系統的時間會跟BIOS同步
- Unix/Linux/Mac OS 會將BIOS的時間當作UTC時間，因此系統啟動後會在BIOS 時間再加上時區時間

基於以上第二點，當你在Unix/Linux/Mac OS 的系統中，將系統的時候設置正解後，其實是在BIOS 時間減掉時區時間。

例如：
Asia/Taipei 的時區是+08：00 ，所以設定好Unix/Linux/Mac OS 的時間後，會在BIOS 時間減去八小時，
所以切換成Windows 10 系統後，會發現時間慢了八小時。

### 作法

1. 讓Ubuntu-20.04 自動向`NTP Server(Network Time Protocol)` 取得正確的時間

    sudo apt-get install ntpdate
    sudo ntpdate time.windows.com

2. 讓Ubuntu-20.04 將正確的時間寫到`Hardware Clock`，讓Windows 10 可以從`Hardware Clock` 讀到正確的時間。