---
title: Windows Terminal 搭配WSL
categories: Windows
tags:
- windows
- wsl
---
Windows 內建的終端機軟體除了`命令提示字元(command prompt)`、`PowerShell`以外，
現在多了新的選擇：**`Windows Terminal`**
Windows Terminal 有命令提示字元與PowerShell 的Shell 層可以選擇，
另外也支援[WSL(Windows Subsystem for Linux)](https://shoudevops.github.io/Windows/windows-subsystem-for-linux/)，可以預設開啟Windows Terminal 即進入到WSL，
也可以針對每一種不同的Shell 層的字型、字體大小做設定，個人覺得是一套蠻不錯的終端機軟體。

<!-- more -->

{% asset_img windows-terminal.jpg Windows Terminal %}

### 從Microsoft Store 下載、安裝
開啟Microsoft Store 搜尋`Windows Terminal` ，點擊【取得】→【安裝】
安裝完畢後，可以點擊【啟動】執行Windows Terminal
{% asset_img microsoft-store-windows-terminal.jpg Microsoft Store %}

### 啟動並設定Windows Terminal
啟動Windows Terminal 後，會出現一個像是命令提示字元的視窗，
如果是剛下載並開啟，預設使用的Shell 層應該會是命令提示字元，
要新增其它類型的Shell ，可以點擊視窗標題列的`箭頭`
{% asset_img windows-terminal-mark.jpg Windows Terminal %}

如果沒有安裝其它終端機，應該只會看到`Windows PowerShell`、`命令提示字元`、`Azure Cloud Shell`
點擊【設定】會開啟預設的文字編輯器，內容是關於Windows Terminal 的相關設定
在第11行會看到：
```
"defaultProfile": "{574e775e-4f2a-5b96-ac1e-a2962a402336}"
```
在Value 欄位的`guid`，代表預設開啟Windows Terminal 所使用的Shell
截取一段`Windows PowerShell` 的list 內容：
```
{
    // Make changes here to the powershell.exe profile.
    "guid": "{61c54bbd-c2c6-5271-96e7-009a87ff44bf}",
    "name": "Windows PowerShell",
    "fontFace": "MesloLGS NF",
    "fontSize": 14,
    "commandline": "powershell.exe",
    "hidden": false
}
```
將Windows PowerShell `"guid"`的`"{61c54bbd-c2c6-5271-96e7-009a87ff44bf}"` 複製，
到第11行的`defaultProfile` 的`guid` 覆蓋貼上，關掉Windows Terminal 再重啟後，就會看到出現的是Windows PowerShell
要預設哪一種Shell ，將list 內的對應Shell name 的guid 貼上到defaultProfile 就行。

#### 以系統管理員身分執行（Run as Administrator）Windows Terminal
可以在【開始】搜尋`Windows Terminal`，在右邊會有【以管理員身份執行】的選項，
但每次要執行前都要做一次這個動作，不是很方便，因此可以將Windows Terminal 釘選到工具列
之後就可以在工具列的`Windows Terminal` 圖示按滑鼠右鍵，再對第一個Windows Terminal 選項按滑鼠右鍵，
就會出現【以系統管理員身分執行】的選項了
{% asset_img windows-terminal-run-as-administrator.jpg Run as Administrator %}

### 從PowerShell 或命令提示字元 進入WSL
開啟Windows Terminal ，要查看目前安裝的WSL Distro版本，可輸入下列指令
```
wsl -l
```
要進入WSL ，可輸入wsl 指令
```
wsl
```
用`uname -a` 指令驗證是不是已經進到WSL
{% asset_img windows-terminal-into-wsl.jpg Into WSL %}

### 配置好用的Terminal 工具與介面
有用過macOS 或Linux 的應該對zsh 不陌生，接下來會說明如何安裝與配置zsh 與相關工具

#### 系統更新
```
sudo apt update && sudo apt upgrade -y
```
{% asset_img wsl-update-upgrade.jpg Update and Upgrade %}

#### 安裝ZSH
安裝指令
```
sudo apt-get install zsh -y
```
{% asset_img wsl-install-zsh.jpg Install ZSH %}

查看shell 清單裡有沒有zsh
```
cat /etc/shells
```
{% asset_img cat-shells.jpg Check shells list %}

找出zsh 的安裝位置
```
which zsh
```
{% asset_img which-zsh.jpg Find zsh location %}

更改預設的shell 為zsh，會要求輸入使用者密碼
```
chsh -s /usr/bin/zsh
```
{% asset_img switch-to-zsh.jpg Switch to zsh %}

#### 安裝oh-my-zsh
執行下列指令後，會詢問是否更換預設的shell 到zsh，再輸入y 同意
```
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```
{% asset_img install-oh-my-zsh.jpg Install oh-my-zsh %}

同意後會要求輸入使用者密碼，之後就會出現oh-my-zsh的畫面了
{% asset_img installed-oh-my-zsh.jpg Installed oh-my-zsh %}

#### 安裝PowerLevel10k 主題
```
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git $ZSH_CUSTOM/themes/powerlevel10k
```

修改 ~/.zshrc 的ZSH_THEME
```
vim ~/.zshrc
```

找到ZSH_THEME，將內容改成powerlevel10k
```
ZSH_THEME="powerlevel10k/powerlevel10k"
```
{% asset_img edit-zsh-theme.jpg Edit ZSH_THEME %}

將下列字型下載後安裝到Windows 裡(C:\Windows\fonts)
+ [MesloLGS NF Regular.ttf](https://github.com/romkatv/dotfiles-public/raw/master/.local/share/fonts/NerdFonts/MesloLGS%20NF%20Regular.ttf)
+ [MesloLGS NF Bold.ttf](https://github.com/romkatv/dotfiles-public/raw/master/.local/share/fonts/NerdFonts/MesloLGS%20NF%20Bold.ttf)
+ [MesloLGS NF Italic.ttf](https://github.com/romkatv/dotfiles-public/raw/master/.local/share/fonts/NerdFonts/MesloLGS%20NF%20Italic.ttf)
+ [MesloLGS NF Bold Italic.ttf](https://github.com/romkatv/dotfiles-public/raw/master/.local/share/fonts/NerdFonts/MesloLGS%20NF%20Bold%20Italic.ttf)

輸入下列指令進行介面的交互式設定
```
p10k configure
```
進來設定模式後，應該會看到一些亂碼，這是因為還沒有針對這個Shell 的字型做設定
這裡先按q 跳出設定
{% asset_img p10k-configure-unread.jpg 亂碼 %}

在Windows Terminal 按`ctrl + ,`或是在標題列的下箭頭可以找到【設定】選項
會開啟文字編輯器，從list 內找到你的WSL ，加入剛剛的字型設定，也可以自訂字體大小
```
"fontFace": "MesloLGS NF",
"fontSize": 14,
```
{% asset_img setting-font.jpg Setting font and font size %}
加入後存檔離開文字編輯器，並且再到Windows Terminal 輸入一次設定指令
```
p10k configure
```
剛剛看到的亂碼就會出現圖案了
{% asset_img p10k-configure-encode.jpg 解決亂碼 %}

再來的設定就依個人喜好進行挑選，就不再囉嗦了！

設定完成後就會出現華麗的命令列模式
{% asset_img p10k-setting-done.jpg Settings Done! %}

開始享受 Command Line 的環境吧！