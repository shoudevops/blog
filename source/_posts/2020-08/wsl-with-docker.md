---
title: Docker on WSL
categories: Windows
tags:
  - wsl
  - docker
date: 2020-08-03 14:30:18
---

本篇教學會說明如何在WSL 下使用Docker 指令：
主要針對以下步驟說明：
1. 開啟Windows Hyper-V
2. 安裝與設定Docker Desktop for Windows
3. WSL 安裝Docker

<!-- more -->

### 開啟Windows Hyper-V
開啟Hyper-V 的方式有分為指令與UI 操作，這裡僅介紹UI 操作
在【控制台】可以找到【程式和功能】
{% asset_img controlpanel_programs.jpg 程式與功能 %}

左邊選單可以找到【開啟或關閉Windows 功能】
{% asset_img programs_open_close_windows.jpg 開啟或關閉Windows 功能 %}

【Windows 功能】視窗內將【Hyper-V】勾選
{% asset_img windows_functions_hyper_v.jpg 勾選Hyper-V %}

按下【確定】後，Windows 會自動下載必要檔案進行安裝，並要求重新啟動，重新啟動後就可以進行下個步驟

### 安裝與設定Docker Desktpo for Windows
到Docker Hub的[Docker Desktop for Windows](https://hub.docker.com/editions/community/docker-ce-desktop-windows/)
點擊【Get Stable】下載安裝檔
{% asset_img docker_get_stable.jpg Get Stable %}

安裝步驟就一直點【Next】就好，就不再描述，之後就可以在WSL 安裝Docker

### WSL 安裝Docker
進到WSL 的Terminal ，並執行下列指令安裝Docker
```
sudo apt update
sudo apt install docker.io
sudo usermod.aG docker $USER
```

安裝完成後，會發現不管下什麼指令，都會出現錯誤訊息：
```
docker: Cannot connect to the Docker daemon at unix:///var/run/docker.sock. Is the docker daemon running?. See 'docker run --help'.
```
這是因為WSL 本身無法支援Docker Engine（WSL2有支援）。
若希望能在WSl 中運行Docker，就需要將Docker Client expose 到Windows 的Docker Engine（這就是需要安裝Docker Desktop for Windows）

開啟`Docker Desktop for Windows` 的`Settings` 介面，並在`General` 中勾選
```
Expose daemon on tcp://localhost:2375 without TLS
```
{% asset_img docker_expose_daemon.jpg Expose daemon %}

之後將以下指令加入到`~/.profile` 中：
```
export DOCKER_HOST=127.0.0.1:2375
```
{% asset_img add_to_profile.jpg Add command to profile %}

並將該檔案更新
```
source ~/.profile
```

就可以執行Docker 指令了！

{% asset_img docker_command.jpg Docker Version %}