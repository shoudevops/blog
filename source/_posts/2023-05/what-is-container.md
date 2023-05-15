---
title: 什麼是Container？
categories: Docker
tags: docker
keywords: 'docker, container, containerized'
date: 2023-05-15 23:03:38
---

`Container` 是一種作業系統虛擬化的形式，一個`Container` 內包含所有必要的執行檔、二進制檔、Library和Configuration，但相轉於傳統的虛擬化，Container 不包含作業系統內核，造就了它更輕巧，也更容易攜帶與部署。

<!--More-->

## Container 優點

`Container` 的環境獨立性，讓它能方便的在多環境中建置、測試、部署，不需要另外安裝或設定應用程式的依賴程序，也代表它能在任何的設備上輕鬆執行。

`Container` 的優點包括：

* 運行成本更低
* 攜帶性更高
* 確保環境一致性與隔離性
* 部署效率更高
* 更好的應用程式生命週期

## Container 與Docker 的關聯

由於運行`Container` 是依賴於`container runtime`，而`Docker Engine` 就是一種`container runtime`，只要任何有安裝`Docker Engine` 的實體機器或虛擬化機器，都可以輕松的執行`Container`。

## 容器和虛擬機的比較

### Container

{% asset_img containerized_applications.png Containerized Applications %}

`Container` 是應用層的抽象，將程式碼和依賴項目打包成映像檔，可與其它多個容器同時執行在同一台機器，並共用操作系統內核，但`Container` 間不會相互影響。

`Container` 比虛擬機佔用更少的空間，可以處理更多的應用程式並使用更少的虛擬機和操作系統。

### Virtual Machines

{% asset_img virtual_machine_applications.png Virtual Machine Applications %}

虛擬機（Virtual Machine）是將一台實體機器變成多台虛擬機器的物理硬件的抽象。

每個虛擬機都包含操作系統、應用程式、必要的二進制檔和Library，通常容量佔用幾十 GB，啟動速度與相比容器來得慢。

---

以上粗略的說明什麼是`Container（容器）`與`Container Runtime`，以及`Container` 與`Virtual Machine` 的比較，
接下來會圍繞著`Docker` 做一系列的說明與介紹。
