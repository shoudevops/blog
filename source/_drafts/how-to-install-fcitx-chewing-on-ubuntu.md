---
title: Ubuntu-20.04 安裝Fcitx 新酷音
categories: Linux
tags: linux
---

Ubuntu-20.04 安裝Fcitx 新酷音輸入法

如果已經安裝過Fcitx 輸入法系統，

只需要再安裝新酷音輸入法就可以使用。

1. 開啟終端機輸入以下指令安裝

```command
sudo apt-get install fcitx fcitx-chewing
```

<!-- more -->

2. 設定輸入法系統

開啟系統`設定值`選`地區和語言`，開啟`管理安裝的語言`介面

{% asset_img system-settings-locate-and-lanugage.png System-Settings %}

在語言支援的視窗下方`鍵盤輸入法系統`選擇`fcitx`

{% asset_img language-support-fcitx.png Language-Support %}

重新開機或是重新登入使設定生效。

3. 設定與嘸蝦米輸入法切換

在`系統工具列`點擊`Fcitx`的圖示，並選擇`設定目前輸入法`

會開啟`輸入法設定`視窗

{% asset_img input-setting.png 輸入法設定 %}

如果習慣預設是`英文輸入法`、第一次切換後是`嘸蝦米輸入法`、再切換後是`新酷音輸入法`

可以按照上圖的順序設定

`Ctrl + Space`後會切換到`嘸蝦米輸入法`
`Ctrl + Shift`會再切換到`新酷音輸入法`

詳細設定可以在上圖下方的設定圖示內自訂。
