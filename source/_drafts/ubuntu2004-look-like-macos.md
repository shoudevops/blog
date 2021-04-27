---
title: 讓Ubuntu-20.04 介面像Mac OS
categories: Linux
tags: linux
---

Ubuntu 是Linux發行版中好用的桌面版本之一，
本文章會說明如何自訂Ubuntu 20.04，讓它看起看像是Mac OS，
使用者也可以依自己的喜好與興趣調整其它功能或介面佈局。

### 安裝必要的套件
在自訂Ubuntu之前，這個步驟是必須的，Ubuntu-20.04 的介面是採用Gnome，
因此安裝Gnome Tweaks工具可以讓使用者調整和修改Ubuntu的外觀和行為。

<!-- more -->

1. 先用快捷鍵打開Terminal

    Ctrl + Alt + T

2. 輸入下列指令

```
sudo apt update && sudo apt upgrade
sudo apt install gnome-tweaks -y
```

3. 安裝`GNOME Shell Extension`套件
這個套件可以讓Ubuntu 增加更多功能。

```
sudo apt install gnome-shell-extensions -y
```

4. 安裝`Gnome Extension`

到[Gnome Extensions](https://extensions.gnome.org/)網站安裝`User Themes`的擴充套件；
{% asset_img gnome-extensions.png Gnome Extensions %}
如果在首頁沒看到，可以用`Search for extensions...`的欄位進行搜尋。

5. 開啟`User Themes`

`User Themes`的功能是可以讓使用者套用自定義的主題，打開`Gnome Tweaks`工具，
選擇擴充套件之後，可以看到`User Themes`的項目，打開即可套件自定義的主題。
{% asset_img open-the-user-themes.png Open the User Themes %}

### 套用Mac OS GTK 主題

上述步驟都完成後，現在是進入讓Ubuntu 看起來像Mac OS的第一步，
以下會說明如何套用Mac OS的主題、應用圖示、鼠標。

1. 下載主題

在[Gnome-Look](https://www.gnome-look.org/browse/cat/135/order/latest/)網站，有很多主題、壁紙、鼠標、圖示…等可以提供下載，
在Ubuntu-20.04要選擇`GTK3/4 Themes`類型的主題，這裡用[WhiteSur GTK Theme](https://www.gnome-look.org/p/1403328/)示範
{% asset_img whitesur-gtk-theme-download.png Download WhiteSur Theme %}

2. 套用主題

下載後將壓縮檔的內容解開到`~/.themes`路徑
（如果找不到路徑可用`Ctrl + H`顯示隱藏的資料夾和文件，還是看不到的話請自行建立資料夾）
{% asset_img home-dir-themes.png ~/.themes %}

重新開啟`Tweaks`工具，選擇外觀，將`應用程式`與`Shell`選擇`WhiteSur-dark`，會即時的看到變化。
{% asset_img app-shell-whitesur-theme.png WhiteSur-dark %}


### 套用Mac OS 圖標

目前的主題已經讓您的Ubuntu畫面看起來像Mac OS，下一步是讓應用程式的圖示也像是Mac OS，
套用圖示的步驟與套用主題類似。

1. 下載圖示

到[Gnome-Look](https://www.gnome-look.org/browse/cat/132/order/latest/)網站下載需要的圖示，這裡用[WhiteSur icon theme](https://www.gnome-look.org/p/1405756/)示範
{% asset_img whitesur-icon-download.png Download WhiteSur Icon %}

2. 套用圖示

下載後將壓縮檔內容解開到`~/.icons`路徑，看不到請自行建立資料夾
{% asset_img home-dir-icons.png ~/.icons %}

重新開啟`Tweaks`工具，選擇外觀，將`圖示`選擇`WhiteSur-dark`，會即時的看到變化。
{% asset_img icon-whitesur-theme.png WhiteSur-dark %}

### 套用Mac OS 鼠標

鼠標平時是比較看不出來的，但為了完整性，連鼠標也一併替換吧！

1. 下載鼠標

到[Gnome-Look](https://www.gnome-look.org/browse/cat/107/order/latest/)網站下載需要的鼠標，這裡用[WhiteSur cursors](https://www.gnome-look.org/p/1411743/)示範
{% asset_img whitesur-cursor-download.png Download WhiteSur Cursor %}


2. 套用鼠標

下載後將壓縮檔內容解開到`~/.icons`路徑，與圖示的路徑相同
{% asset_img home-dir-cursors.png ~/.icons %}

重新開啟`Tweaks`工具，選擇外觀，將`游標`選擇`WhiteSur-cursors`，會即時的看到變化。
{% asset_img cursors-whitesur-theme.png WhiteSur-cursor %}

### 調整Ubuntu Dock 為Mac OS Dock

這個步驟會說明如何調整與Mac OS 的Dock 相似的Dock，
Linux 提供了許多第三方的選擇，例如：`Plank`、`Cairo Dock`、`Dash to Dock`…等，
但這裡會介紹在不安裝第三方的情況，將原始的Dock 調整類似於Mac OS Dock。

1. 調整系統設定

開啟系統的`設定值`
{% asset_img system-settings.png 系統設定值 %}

到`外觀`選項，在Dock下打開`自動隱藏Dock`(`Auto-hide the Dock`)、
`螢幕上的位置`(`Position on screen`)改成`下`(`Bottom`)
{% asset_img system-settings-dock.png Dock設定 %}

2. 設定Dock 自定義參數指令

```
gsettings set org.gnome.shell.extensions.dash-to-dock extend-height false
gsettings set org.gnome.shell.extensions.dash-to-dock dash-max-icon-size 40
```

指令輸入完之後就會得到如下圖的效果
{% asset_img customized-dock-command.png Dock自定義設定 %}

### 設定Top Bar會自動隱藏

Ubuntu預設的`Top Bar`會固定在畫面的上方，會有壓縮到整個畫面的感覺，
透過`Gnome Shell Extensions`，安裝`Hide Top Bar`套件隱藏，
並設定鼠標覆蓋原位置的時候出現。

1. 搜尋`Hide Top Bar`套件

到[Gnome Shell Extensions](https://extensions.gnome.org/)的網站，
在`Search for extensions...`欄位搜尋`hide top bar`。
{% asset_img hide-top-bar-extension.png Hide Top Bar %}

2. 安裝`Hide Top Bar`套件

上個步驟搜尋到`Hide Top Bar`之後點擊進入，點擊畫面右上方的`OFF`，
會跳出安裝的視窗，點擊安裝。
{% asset_img install-hide-top-bar-extension.png Install Hide Top Bar %}

3. 設定`Hide Top Bar`

安裝之後會看到`Top Bar`被隱藏了，要設定鼠標移過去後會自動滑下出現
開啟`Tweaks`工具，選擇`擴充套件`項目，看到`Hide top bar`，按下設定按鈕
{% asset_img tweaks-hide-top-bar.png Setting Hide Top Bar %}

打開`Show panel when mouse approaches edge of the screen`，就會看到效果了。
{% asset_img show-panel-when-mouse-approaches.png Show Top Bar panel %}

### 設定視窗標題列按鈕

視窗標題列的`縮到最小`、`放大最大`、`關閉`的按鈕Ubuntu 預設是在視窗右上角
修改到左上角會更像是Mac OS

打開`Tweaks`工具，選擇`視窗標題欄`，在`標題列按鈕`底下的位置改成`左側`就會看到效果了。
{% asset_img window-top-colume-button.png 標題題按鈕 %}

---

以上修改完成後，大致上都會跟Mac OS的介面類似了，
桌面的壁紙或是系統的字型也可以修改跟Mac OS相同。