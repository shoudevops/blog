---
title: Linux 安裝
categories: Linux
tags: linux
date: 2020-04-07 17:38:41
---

介紹安裝步驟時會以 **Ubuntu 16.04 LTS 伺服器版本** 進行，並以VMWare虛擬機示範安裝，有興趣也可以使用最新版本進行安裝練習，觀念上都是相同的。

Ubuntu 下載位置：[https://www.ubuntu-tw.org/modules/tinyd0/](https://www.ubuntu-tw.org/modules/tinyd0/)
{% asset_img linux-download.jpg Download Linux %}

<!-- more -->

### Linux Kernel 版號

透過以下指令可以查看Linux Kernel的版號
```
uname -r
```
> 4.4.0-142-generic
主版本.次版本.釋出版本-修改版本

### Ubuntu 版號

Ubuntu 16.04 LTS
> Ubuntu 年份.月份 LTS(Long-term support)
> Ubuntu的LTS支援五年更新

Ubuntu 16.04及之前版本預設桌面是Unity，18.04開始是Gnome3，但可以手動安裝Unity並切換。

### Ubuntu 安裝

先在VMWare建立一台虛擬機（BIOS使用UEFI模式，避免在用中文語系安裝時出現錯誤），硬體規格選擇最小的即可，再把下載的Ubuntu映像檔放入虛擬光碟機中，開啟虛擬機時就會出現安裝畫面。

#### 選擇第一個 **Install Ubuntu Server** 進行Ubuntu的安裝程序
{% asset_img grub-screen.jpg GNU GRUB %}
- OEM install (for manufacturers)：提供給電腦製造商（Asus, Acer, MSI…等）使用
- Install MAAS xxx：安裝雲端套件（如：Google Cloud SDK）
- Check disc for defects：檢查目前使用的安裝程式是否正常
- Rescue a broken system：修復毀損的作業系統
- Boot and Install with the HWE kernel：使用 HWE kernel進行安裝<br/>（HWE Kernel：HWE Kernel版本僅在發佈後六個月提供安全性更新，下一個HWE Kernel會被自動升級。最新的HEW Kernel版本是下一個LTS的主要版本的Kernel版本。）

#### 選擇安裝流程的顯示語系，也會是安裝完成後預設的系統語系
{% asset_img select-a-language.jpg 選擇安裝與系統預設語系_Select a language %}
> *選擇中文或英文都可以，選擇中文到安裝完成後，還需要自行安裝中文語言套件包，否則終端機中文會顯示不出來。*

#### 選擇你的所在地點（other → Asia → Taiwan）
{% asset_img select-your-location.jpg 選擇所在地點_Select your location %}

#### 設定語言環境（因步驟2. 選擇英文，在步驟3. 選地點時，Ubuntu 沒有合適的語言環境選項，就需要自行設定）
{% asset_img configure-locales.jpg 設定語言環境_Configure locales %}
> *這裡選擇`United States`就可以。*

#### 設定鍵盤（選`Yes`系統會詢問幾個文字是否有出現在鍵盤上，選`No`會手動選擇鍵盤）
{% asset_img configure-the-keyboard.jpg 是否指定鍵盤佈置_Detect keyboard layout? %}
> 下圖是選擇`NO`之後出現的手動選擇鍵盤畫面
{% asset_img configure-the-keyboard-2.jpg Country of origin for the keyboard %}
{% asset_img configure-the-keyboard-3.jpg Keyboard layout %}

#### 設定網路（主機名稱）
{% asset_img configure-the-network.jpg Enter the hostname s%}

#### 設定使用者全名（這裡不是登入的username）
{% asset_img set-up-users-and-passwords.jpg 設定使用者全名_Full name for the new user %}

#### 設定使用者帳戶名稱（這裡才是登入的username）
{% asset_img set-up-users-and-passwords-2.jpg 設定使用者帳戶名稱 Username for your account %}

#### 設定使用者登入密碼
{% asset_img set-up-users-and-passwords-3.jpg 設定使用者登入密碼 Choose a password for the new user %}
再次輸入密碼驗證
{% asset_img set-up-users-and-passwords-4.jpg 再次輸入密碼 Re-enter password to verify %}

#### 設定是否加密`家目錄`（一般使用的情況下不需要加密，若系統毀損資料還救得回來）
{% asset_img set-up-users-and-passwords-5.jpg 加密家目錄 Encrypt your home directory %}
> 在銀行或是金融業等使用的伺服器安全性需求較高的時候，就需要加密家目錄。

#### 設定時區（有連上網路的情況下，一般都會自動校正所在地的時區）
{% asset_img configure-the-clock.jpg 設定時區 Configure the clock %}

#### **分割磁區**
- `Guided` 開頭的會整個根目錄分割一個磁碟，不會依照資料夾來分割（不想管那麼多可以直接選這個）
- `LVM` 是動態分配磁碟的功能，若目前分割的空間不足，可以再動態增加，不用重新分割
- `Manual` 是手動分配各資料夾要掛載到哪個磁碟、多少容量
{% asset_img partition-disks.jpg 分割磁碟_Partition disks %}
**這裡會示範手動分配磁碟**（自動分配應該沒什麼好示範吧…）
選擇掛載到虛擬機的磁碟
{% asset_img partition-disks-2.jpg 手動分配磁碟 %}
會出現詢問`是否要建立一個空的分割表在這個磁碟上`，選擇`Yes`
{% asset_img partition-disks-3.jpg 建立空的分割表_new empty partition table %}
選擇`FREE SPACE`的選項（容量看虛擬機掛載的硬碟空間大小而有不同的顯示）
{% asset_img partition-disks-4.jpg 選擇磁碟_Select a disk %}
選擇`建立新的Partition`
{% asset_img partition-disks-5.jpg 建立新的分割磁碟_Create a new partition %}
輸入要分配的磁區空間（這裡要分配給/boot 資料夾，只有開機的時候會用到，給300MB即可）
{% asset_img partition-disks-6.jpg 分配空間_New partition size %}
詢問要分割的磁碟要在可用空間的開頭還是結尾，選擇`Beginning`就好
{% asset_img partition-disks-7.jpg 磁碟起始位置_Location for the new partition %}
編輯磁碟相關的資訊（基本上就是改`Mount point`到指定的路徑就好），編輯完成後選`Done setting up the partition`
{% asset_img partition-disks-8.jpg 設定磁碟_Partition settings %}
比較懶的做法就把`boot`跟`usr`另外分割出來，其它都分給`root`，再按`Finish partitioning ...`的選項就完成
- 如果BIOS是UEFI格式，要再多分一個ESP(EFI System Partition)格式的空間
- SWAP 置換空間不一定要分割，用途只有在記憶體不足的時候才會利用硬碟空間當作記憶體使用
{% asset_img partition-disks-9.jpg 分割表_Partition table %}
> 可以再分割其它的資料夾磁碟，但測試用的就20GB，其它如：`/home`, `/bin`, `/etc`等其它目錄要如何分割，就看機器的用途來做配置

確認是否要依照分割表的內容寫入到磁碟，選擇`Yes`就會開始執行磁碟分割並安裝系統
{% asset_img partition-disks-10.jpg 確認分割表並寫入磁碟_Write the changes to disks? %}

#### 設定HTTP Proxy
過程中會詢問是否需要透過`HTTP Proxy`連到網路，不需要的話留空就好
{% asset_img configure-the-package-manager.jpg HTTP Proxy %}

#### 設定系統更新
詢問如何管理系統更新，就看個人如何安排，示範就選擇`No automatic updates`
{% asset_img configuring-tasksel.jpg 管理系統更新方式_Manage upgrades on this system %}

#### 可選擇的軟體套件
可以選擇希望安裝的套件軟體，示範最小安裝，僅安裝`OpenSSH Server`可以使用SSH協定進行連線
{% asset_img software-selection.jpg 選擇安裝套件軟體_Choose software to install %}

#### 安裝完成！
將安裝檔從（虛擬）光碟機中移除再選擇`Contunue`重新開機，就會進到Ubuntu的登入畫面了～
{% asset_img finish-the-installation.jpg 完成安裝_Finish the installation %}
{% asset_img login-screen.jpg 登入畫面_Login %}