---
title: PostgreSQL for Docker
categories: PostgreSQL
tags:
- postgresql
- database
date: 2020-07-30 17:17:35
---

使用Docker 建立PostgreSQL 環境
Installation PostgreSQL with Docker

### 安裝Docker
如果還沒有Docker 環境，可以到[Get Started with Docker](https://www.docker.com/get-started)取得

### Docker Volume
使用Docker Volume 為資料庫建立持久化
建立一個名稱為`postgresql-data`的docker volume：

<!-- more -->

```
docker volume create --name postgresql-data
```

### PostgreSQL Container
到Docker Hub找到由官方釋出的[PostgreSQL Image](https://hub.docker.com/_/postgres/)
本教程使用PostgreSQL 10.13做範例，建立 PostgreSQL Container，執行以下指令：
```
docker run -d --name postgres --restart always -p 5432:5432 -v postgresql-data:/var/lib/postgresql/data -e POSTGRES_PASSWORD=pgpassword postgres:10.13
```
+ -d：在背景執行容器
+ --name：容器的名稱
+ --restart：不論任何情況造成容器停止運行，Docker 會嘗試重新啟動容器
+ -p：容器的5432 Port 映射到Docker 本機的5432 Port(host_port:container_port)
+ -v：使用建立完成的Docker Volume：postgresql-data掛載到容器路徑`/var/lib/postgresql/data`
+ -e：PostgreSQL 容器使用的環境變數
+ postgres:10.13：指定使用的PostgreSQL 映像檔

#### 掛載主機目錄
若不使用Docker Volume，也可將資料庫持久化建立於本機目錄下，
可直接指定絕對路徑，或是移動到掛載的目錄下以`$PWD`當作路徑

##### 絕對路徑
```
docker run -d --name postgres --restart always -p 5432:5432 -v /Users/chenhsiang/Documents/Temp/Docker/PostgreSQL/postgresql-data:/var/lib/postgresql/data -e POSTGRES_PASSWORD=pgpassword postgres:10.13
```

##### 移動到掛載目錄
```
cd /Users/chenhsiang/Documents/Temp/Docker/PostgreSQL

docker run -d --name postgres --restart always -p 5432:5432 -v $PWD/postgresql-data:/var/lib/postgresql/data -e POSTGRES_PASSWORD=pgpassword postgres:10.13
```

### PostgreSQL 管理工具 - pgAdmin 4
從[官方Download 頁面](https://www.pgadmin.org/download/)可以看到目前有釋出的版本。
{% asset_img pgadmin4_download_page.jpg Download Page %}

開啟Docker Hub pgAdmin4的[連結](https://hub.docker.com/r/dpage/pgadmin4/)
依文件說明加入對應的參數執行，指令如下：
```
docker run -d --name pgadmin4 --restart always -e "PGADMIN_DEFAULT_EMAIL=example@mail.com" -e "PGADMIN_DEFAULT_PASSWORD=give_a_password" -p 8080:80 dpage/pgadmin4:4.24
```
+ -e：註冊一組pgAdmin4 的帳號密碼，注意是pgAdmin4，不是PostgreSQL 資料庫的帳號
+ -p：容器的80 Port 映射到Docker 本機的8080 Port（本機port 可以自訂開啟Browser所使用的port number）

完成後開啟[http://localhost:8080/](http://localhost:8080/)，就會看到pgAdmin4的登入頁面
{% asset_img pgadmin4_login_page.jpg Login Page %}
使用Docker 指令註冊的pgAdmin4帳號密碼進行登入

### 與PostgreSQL 資料庫建立連線
#### 點擊Add New Server 新增資料庫
{% asset_img pgadmin4_add_new_server.jpg Add New Server %}

#### Create - Server 畫面，General → Name 可以自行命名
{% asset_img pgadmin4_add_new_server_name.jpg Server Name %}

#### Create - Server 畫面，Connection → Hostname/address
這裡有兩個選擇：輸入本機的Internal IP 或Docker network 的IP
{% asset_img pgadmin4_add_new_server_hostname.jpg Server Hostname %}
本機的Internal IP查詢方式：
```
Windows: 
ipconfig

MacOS/ Linux: 
ifconfig
```
ipconfig：
{% asset_img pgadmin4_add_new_server_hostname_ipconfig.jpg Server Hostname ipconfig %}
ifconfig：
{% asset_img pgadmin4_add_new_server_hostname_ifconfig.jpg Server Hostname ifconfig %}

容器的IPAddress查詢方式：
```
docker inspect postgres | grep "IPAddress"
```
{% asset_img pgadmin4_add_new_server_hostname_container_ip.jpg Server Hostname Container IP %}

#### 填上Hostname, Username, Password
Hostname填入上一步查詢的結果（擇一）
Username預設是postgres
Password是建立PostgreSQL 容器時帶的環境變𣤋`POSTGRES_PASSWORD`的值
填入後點擊`Save`即完成與資料庫建立連線
{% asset_img pgadmin4_add_new_server_complete.jpg Complete and Save %}