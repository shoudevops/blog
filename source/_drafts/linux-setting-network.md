---
title: Linux 網路設定
categories: Linux
tags: 
- linux
- networking
---
以上一篇安裝的Ubuntu 16.04 LTS為例，說明作業系統安裝完成後，如何設定網路

### 查詢目前網路卡與網路資訊

用`ifconfig`或`ip a`可以查詢目前網路的資訊

{% asset_img network-ifconfig.jpg 用ifconfig指令查詢 %}

<!-- more -->

- `ens33` 是虛擬機建立時提供給它的網路卡一，整個區塊都是這張網路卡的資訊
- `lo` 是Loopback，能用來作為測試作業系統內部迴圈所用的一個網域
- `inet addr: 172.16.122.132` 是目前`ens33`這張網路卡所取得的私有IP
- `Bcast: 172.16.122.255` 是目前172.16.122.xxx這個網段下的廣播IP
- `Mask: 255.255.255.0` 是網路遮罩的十進位表示方法

### 設定 Network interfaces, DNS

Ubuntu 16版與Ubuntu 18版設定的檔案不同，因此這裡會分開介紹

#### Ubuntu 16.04 LTS

```
vi /etc/network/interfaces
```

開啟`interfaces`這個檔案後，可以看到目前網路的預設內容

{% asset_img network-interfaces.jpg 開啟interfaces檔案設定網路 %}

若沒有指定特定IP位置，而且目前也可以正確的連線到Internet，也可以使用預設的DHCP自動取得的IP做使用
若想要安排在這個網段裡這台機器要使用哪個IP，就必需要自己設定了

#### Ubuntu 18.04 LTS

adskfj

alkdfjlasd

aldkfjlasdk