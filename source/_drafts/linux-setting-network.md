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

- `lo` 是Loopback，能用來作為測試作業系統內部迴圈所用的一個網域
- `ens33` 是虛擬機建立時提供給它的網路卡一，整個區塊都是這張網路卡的資訊
- `inet addr: 192.168.246.128` 是目前`ens33`這張網路卡所取得的私有IP
- `Bcast: 192.168.246.255` 是目前172.16.122.xxx這個網段下的廣播IP
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

以下是要修改的interfaces檔案內容：
```
auto ens33    ->  ens33 是機器的網路卡名稱，請自行修改。
iface ens33 inet static

# 下面的IP要修改為機器網段的IP
address 192.168.246.168
netmask 255.255.255.0
gateway 192.168.246.2

# 設定DNS Server
dns-nameservers 168.95.1.1
dns-nameservers 8.8.8.8
```

設定完成後存檔離開，再來就要刷新網路卡設定跟重新啟動網路卡
```
# 刷新設定
sudo ip addr flush ens33    ->  網路卡名稱要記得修改哦

# 重啟網路卡（不是root權限會要求輸入密碼）
/etc/init.d/networking restart
```

下查詢指令後會看到 IP已經更新
{% asset_img networking-flush.jpg 刷新網路卡設定再重啟網路卡 %}

#### Ubuntu 18.04 LTS

到Ubuntu 18.04的機器後，先查詢網路資訊
{% asset_img networking-18-ifconfig.jpg Ubuntu 18.04 LTS ifconfig %}

如果我們跟 Ubuntu 16.04 一樣開啟 /etc/network/interfaces 的檔案，會看到：
{% asset_img networking-18-interfaces.jpg 查看interfaces檔案 %}

> ifupdown has been replaced by netplan(5) on this system. See /etc/netplan for current configuration.

安裝系統時如果有使用到網路，在 `/etc/netplan/`目錄下就應該會有基本的設定檔，
若完全沒有設定檔，可以使用以下指令自動產生預設的設定檔：
```
sudo netplan generate
```

開啟 /etc/netplan/50-cloud-init.yaml 設定檔（或其它設定檔），將相關資訊填入
```
network:
    ethernets:
        ens33:
            addresses: [192.168.246.188/24]  ->  IP 位址與網路遮罩
            gateway4: 192.168.246.2
            nameservers:
                addresses: [168.95.1.1, 8.8.8.8]
            dhcp4: no
    version: 2
```
修改並存檔後輸入以下指令：
```
sudo netplan try
```
執行後會檢查設定檔格式，如果正確的話就會套用，並在120秒以後自動還原設定（如果設錯了在兩分鐘後會還原）！
在120秒按`ENTER`之後就會使用新的設定檔內容了！
也能在120秒以後輸入以下指令套用
```
sudo netplan apply
```
再來查看設定是否生效：
{% asset_img networking-netplan-apply.jpg 查看網路介面設定 %}

---

### 檢查網路是否可以連線

網路介面都設定完成後，要如何驗證是否可以正確的連線到Internet呢？
最簡單的方式就是`ping`一個不在同網段內的位址測試有沒有回應：
```
ping 8.8.8.8
```
ping看看Google的DNS Server會不會有回應
{% asset_img networking-ping.jpg Ping Google DNS Server %}

可以看到Google DNS Server有回應，這樣就可以正常的連線到Internet囉！