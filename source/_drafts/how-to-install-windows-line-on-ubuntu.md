---
title: 如何在Ubuntu-20.04 安裝Windows Line
categories: Linux
tags: linux
---
Line 通訊軟體目前除了在手機的雙平台中使用，也可以在Windows、Mac OS 和Chrome 系統上執行。
若要在Ubuntu 上使用電腦版Line 的作法，最方便的作法是用Chomre 瀏覽器的擴充功能達成，
但只有文字訊息的功能，無法使用像是`記事本`、`相簿`…等功能。

而本文章的作法，可以讓你在Ubuntu-20.04 上安裝Windows 版本的Line軟體，可以使用電腦版完整的功能。

<!-- more -->

### Wine

- Wine 能讓您在Linux 上運行許多Windows 程式

#### 安裝Ubuntu 版本的Wine

1. 從`Ubuntu Software`搜尋`wine`並安裝
2. 透過command line

```command
wget https://dl.winehq.org/wine-builds/winehq.key
sudo apt-key add winehq.key
sudo apt-add-repository 'https://dl.winehq.org/wine-builds/ubuntu/'
```

#### 初始設定

Wine 安裝完成後，會建立一個假的Windows C: drive，能在其中安裝Windows 的應用程式，
可以輸入以下指令查看Windows 的設定

```command
winecfg
```

#### 用Wine 安裝Line

1. 下載Windows 版本的Line 安裝檔(LineInst.exe)
2. 打開Terminal，到Line 安裝檔的路徑下
3. 輸入指令安裝Line

```command
wine LineInst.exe
```

這時會看到Line的安裝視窗，接著就像安裝Windows Line相同的步驟執行即可。

#### 執行Line

安裝完成後，Line 的執行檔通常會在`~/.wine/drive_c/`的路徑下，後面的路徑就會跟Windows相同，
完整的路徑就會像是：

    /home/username/.wine/drive_c/users/username/'Local Settings'/'Application Data'/LINE/bin/LineLauncher.exe"

記得再將username換成自己的user name即可。

要執行的指令就會是`wine application-path-app.exe`，就是上面的路徑前面加上`wine`就行了。

    wine /home/username/.wine/drive_c/users/username/'Local Settings'/'Application Data'/LINE/bin/LineLauncher.exe"

### 自訂Line 捷徑

上面有提到如何用指令開啟Line 程式，但每次要開啟都要輸入指令還是有些不方便，
其實可以使用自訂捷徑的方式，將這些非常規的軟體放入`應用程式列表`中，以後要開啟Line就會放便許多。

在`~/.local/share/applications`路徑下新增一個捷徑檔

```command
sudo vim ~/.local/share/applications/Line.desktop
```

捷徑檔的內容如下：

```
[Desktop Entry]
Encoding=UTF-8
Name=Line
Exec=wine /home/username/.wine/drive_c/users/username/'Local Settings'/'Application Data'/LINE/bin/LineLauncher.exe"
Icon=/home/username/.icons/line.png
Terminal=false
Type=Application
Categories=Chat;
```

- Name: 軟體名稱
- Exec: 軟體的執行方式
- Icon: 軟體圖示的路徑，Google 搜尋`line icon`就可以找到Line圖示
- Type: 該物件屬於Application
- Categories: 該程式的分類，分類的[相關規範](https://specifications.freedesktop.org/menu-spec/latest/apa.html)

存檔離開後，就可以在`應用程式列表`中找到Line 的軟體捷徑了。

---

參考文件：

[Wine](https://help.ubuntu.com/community/Wine)
[Ubuntu 自訂應用程式捷徑](https://notes.wadeism.net/linux/326/)