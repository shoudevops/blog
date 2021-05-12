---
title: 將 Ubuntu-20.04 家目錄資料夾路徑改為英文
categories: Linux
tags: linux
date: 2021-05-12 08:55:51
---

在安裝Ubuntu 時，為了方便理解安裝步驟的敘述，會將語系改為好理解的非英文語系，
但系統安裝完成後，會發現`/home/username/` 路徑下的資料夾語言也會變成非英文，
例如：`下載`、`圖片`之類的。

這樣在終端機操作的時候需要切換輸入法非常不方便，
以下教學如何將這些資料夾名稱轉換成英文。

<!-- more -->

1. 開啟終端機輸入以下指令

```command
export LANG=en_US
xdg-user-dirs-gtk-update
```

輸入完成後會出現`Update standard folders to current language?`的視窗，
提示會從什麼語言改為英文。

接著按下`Update Names`，資料夾名稱就會改成英文了。
若原其它語言的資料夾內有檔案的話，該資料夾不會被改語言，且原檔案會保留，
這時候只要手動搬移檔案，再將原其它語言資料夾刪除即可。

2. 重新開機

重新開機進到桌面後，會再跳出一次`Update standard folders to current language?`的視窗，
這時候將`Don't ask me the again`勾選，並按下`Keep Old Names`，
這樣資料夾語言會維持英文，並且不會再跳出該視窗。
