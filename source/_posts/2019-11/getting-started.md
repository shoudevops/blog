---
title: Python 入門
categories: Python
tags:
- python
- installed
date: 2019-11-20 11:23:24
---
這裡將會介紹`Python` 的安裝與文字編輯器，並且執行第一支程式：`hello_world.py`

### 設定程式開發環境
目前Python 有兩個主要版本：`Python2` 和`Python3`。如果電腦都裝了這兩個版本，建議使用`Python3`；
若還沒安裝`Python`，請直接安裝`Python3` 就好，這樣才能使用到最新版本的功能。

---

<!-- more -->

### 執行Python 程式片段
`Python` 本身內建了一個在終端視窗內執行的直譯器，讓我們不用儲存完整的程式碼，就能直接在其中執行程式片段。
{% asset_img pythonIDLE.jpg Python IDLE %}
在直譯器內輸入
```
print("Hello World!")
```
輸入後按下 Enter 鍵即可執行，就能得到如上圖的結果`Hello World!`
如果這個簡單的程式能在系統中順利執行，那表示其它編寫的`Python` 程式也都能執行了。

---

### 不同作業系統中的 Python
`Python` 是個跨平台的程式語言，可以在所有的主要作業系統中執行。
任何`Python` 程式都可以在任何安裝了`Python` 的系統上執行。

#### Python3 下載與安裝
`Python3` 最新源碼，二進制文件，新聞資訊等可以在`Python` 的官網查看到：
Python官網：[https://www.python.org/](https://www.python.org/)
Python文件：[https://www.python.org/doc/](https://www.python.org/doc/)

#### 在Unix & Linux 中的Python
在`Ubuntu 16.04.5 LTS`之後的版本都有預載`Python3.5`，輸入以下指令可以知道系統的`Python3`版本為何
```
$ python3 --version
Python 3.5.2
```

#### 在 Windows 安裝Python
先檢查系統上是否已經有安裝`Python`，開啟命令提示字元，輸入`python`(p是小寫)按下Enter鍵，
若出現錯誤訊息「'python' 不是內部或外部命令、可執行的程式或批次檔。」，
就表示系統可能沒有安裝`Python`。

遇到以上情況，請先下載和安裝Windows 版的`Python` 程式。
開啟`Python 3.7.5` 的下載頁([https://www.python.org/downloads/release/python-375/](https://www.python.org/downloads/release/python-375/))，
再依照Winodws作業系統的版本下載對應的版本。
例如Windows 64位元，可下載 `Windows x86-64 executable install`版本。

下載後請執行它，出現安裝畫面時，請勾選「Add Python 3.7 to PATH」方塊，這樣安裝時會正確的設定好系統的環境變數。
接著點擊「Customize installtion」(不要點Install Now)。
{% asset_img install_python3_7_5_step1.jpg 安裝Python 3.7.5 %}

下個步驟請勾選全部選項
{% asset_img install_python3_7_5_step2.jpg 安裝Python 3.7.5 %}

再來要勾選「Install for all users」(很重要！才會完整設定到環境變數與C:\Program Files\Python37的資料夾)，
下面的「Precompile standard library」項目會自動勾起。
下個畫面按下「Install」就可以開始安裝了。
{% asset_img install_python3_7_5_step3.jpg 安裝Python 3.7.5 %}
安裝完畢後的視窗直接按「Close」即可。

接著開啟命令提示字元，輸入`python`：
{% asset_img cmd_python.jpg Python 命令提示字元 %}

也可以在「開始」功能中搜尋IDLE(Python 3.7 64-bits)：
{% asset_img pythonIDLE_3_7_5.jpg PythonIDLE %}

---

資料參考：
1. [RUNOOB.COM](https://www.runoob.com/python/python-tutorial.html)
2. [Python Crash Course, 1st Edition](https://nostarch.com/pythoncrashcourse2e)