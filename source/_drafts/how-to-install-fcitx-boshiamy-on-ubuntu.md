---
title: Ubuntu-20.04 安裝嘸蝦米輸入法
categories: Linux
tags: linux
---
Ubuntu-20.04 安裝fcitx 嘸蝦米

分別需要安裝fcitx 系統與嘸蝦米的table

1. 開啟終端機輸入以下指令安裝

```command
sudo apt-get install fcitx fcitx-m17n
sudo apt-get install fcitx-table-boshiamy
```

<!-- more -->

2. 設定輸入法系統

開啟系統`設定值`選`地區和語言`，開啟`管理安裝的語言`介面

{% asset_img system-settings-locate-and-lanugage.png System-Settings %}

在語言支援的視窗下方`鍵盤輸入法系統`選擇`fcitx`

{% asset_img language-support-fcitx.png Language-Support %}

重開機或是重新登入，就會在系統工具列上看到`Fcitx`的圖示。