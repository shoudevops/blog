---
title: ASUS G14 安裝Ubuntu-20.04.02 設定
categories: Linux
tags: Linux
---
網路上找到的教學文章或是討論串大部份都是針對`Ubuntu-20.04.01 LTS` 的顯示卡設定，
`Ubuntu-20.04.01 LTS` 版本的`Linux Kernel`是`5.4`，
目前(2021/07)最新的長期支援版本是`Ubuntu-20.04.02`，使用的`Linux Kernel`是`5.8`，
已經有支援`AMD RYZEN 4000 SERIES`的CPU，因此少了很多必要的設定步驟。

紀錄一下安裝的時候踩過什麼坑。

## 安裝Ubuntu-20.04.02 LTS

會看到許多文章或討論會提到，使用USB 開機時，要在GRUB 畫面按`"E"`，
在`quiet splash` 後面加上`nomodeset modporbe.blacklist=nouveau`，
但是在`Ubuntu-20.04.02 LTS` 不需要，正常依照需求安裝系統就好。

## 移除系統預裝的Nvidia Driver

```shell
sudo apt-get remove --purge '^nvidia-.*'
sudo apt autoremove
sudo apt-get install ubuntu-desktop
sudo update-grub
```

重啟系統

## 安裝AMD 官方驅動

[Radeon Software for Linux 20.20 Release Note](https://www.amd.com/en/support/kb/release-notes/rn-amdgpu-unified-linux-20-20)，這裡可以下載對應Linux系統的驅動

下載、解壓縮、安裝

```shell

# 可以在上面連結確認有沒有新版本發佈
wget https://drivers.amd.com/drivers/linux/amdgpu-pro-20.20-1098277-ubuntu-20.04.tar.xz

# 解壓縮
tar -xvf amdgpu-pro-20.20-1098277-ubuntu-20.04.tar.xz

# 安裝
cd amdgpu-pro-20.20-1098277-ubuntu-20.04/
sudo ./amdgpu-install -y

# 如果 sudo ./amdgpu-install -y 有出現amdgpu-dkms的錯誤，就先移除
cd /usr/bin && sudo amdgpu-uninstall

# 再回到解壓縮後的路徑，用下面的指令安裝
sudo apt-get install --no-dkms
```

重啟系統

## 安裝Nvidia 驅動

直接用PPA安裝

```shell
sudo add-apt-repository ppa:graphics-drivers/ppa
sudo apt-get update

# 讓Ubuntu 選擇合適的Driver 安裝
sudo ubuntu-drivers autoinstall

# 設定Nvidia 不是主要使用的GPU
sudo vim /usr/share/X11/xorg.conf.d/10-nvidia.conf

# 在Section "OutputClass"段落內加入
Option "PrimaryGPU" "No

# Update GRUB
sudo update-grub
```

重啟系統

用Glxinfo 確認顯示卡狀態

```shell
sudo apt-get install mesa-utils

# Nvidia
__NV_PRIME_RENDER_OFFLOAD=1 __GLX_VENDOR_LIBRARY_NAME=nvidia glxinfo | egrep "(OpenGL vendor|OpenGL renderer|OpenGL version)"

# AMD Radeon
glxinfo | egrep "(OpenGL vendor|OpenGL renderer|OpenGL version)"

# 加入alias 到 ~/.bashrc 或~/.zshrc
alias prime-run="__NV_PRIME_RENDER_OFFLOAD=1 __GLX_VENDOR_LIBRARY_NAME=nvidia __VK_LAYER_NV_optimus=NVIDIA_only"
```

需要用Nvidia 顯示啟動軟體時，就在command 前面加上`prime-run`

```shell
# 確認Nvidia 顯卡運作狀態
prime-run glxinfo | egrep "(OpenGL vendor|OpenGL renderer|OpenGL version)"
```

{% asset_img confirm_nvidia_status.png 確認獨顯運作狀態 %}

```shell
# 確認AMD 內顯運作狀態
glxinfo | egrep "(OpenGL vendor|OpenGL renderer|OpenGL version)"
```

{% asset_img confirm_nvidia_status.png 確認內顯運作狀態 %}

---
## 參考：
