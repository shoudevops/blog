---
title: Linux 目錄
categories:
tags:
---
為了讓使用者可以瞭解到已安裝較體通常放置於哪個目錄下，因此有了`Filesystem Hierarchy Standard(FHS)`標準的出現。
希望每個獨立的軟體開發商、作業系統製作者，以及想要維護系統的使用者，都能遵循FHS的標準。

### 目錄配置的依據 - FHS
FHS依據檔案系統使用的頻繁與否與是否允許使用者隨意更動，而將目錄定義為四種交互作用的形態：
+ 可分享的：可以分享給其它系統掛載使用的目錄
+ 不可分享的：自己機器上面運作的裝置檔案或是與程序有關的socket檔案等
+ 不變的：有些資料是跟隨著Linux Distribution而不變動的，例如函式庫、文件說明檔、系統管理員所管理的主機服務設定檔等
+ 可變動的：經常改變的資料，例如登錄檔、一般用戶可自已收受的新聞群組等

<!--more -->
以表格來呈現：

||可分享的(shareable)|不可分享的(unshareable)|
|---|---|---|
|不變的(static)|/usr(軟體放置處)<br />/opt(第三方協力軟體)|/etc(設定檔)<br />/boot(開機與核心檔)|
|可變動的(variable)|/var/mail(使用者郵件信箱)<br />/var/spool/news(新聞群組)|/var/run(程序相關)<br />/var/lock(程序相關)|

事實上，FHS針對目錄樹架構僅定義出三層目錄底下應該放置什麼資料，分別是：
+ /(root，根目錄)：與開機系統有關
+ /usr(unix software resource)：與軟體安裝/ 執行有關
+ /var(variable)：與系統運作過程有關

---

### 根目錄的意義與內容

所有的目錄都是由根目錄衍生出來的，同時根目錄也與開機/還原/系統修復等動作有關
所以FHS希望根目錄不要放在非常的的分割槽內，因為越大的分割槽就會放入越多資料，根目錄所在的分割槽就可能會有較多發生錯誤的機會。

FHS也定義出根目錄(/)底下應該要有哪些次目錄的存在才好，即使沒有實體目錄，FHS也希望有連結檔存在：

<table>
    <tr>
        <th>目錄</th>
        <th>應放置檔案內容</th>
    </tr>
    <tr>
        <td colspan="2">第一部份：FHS要求必須存在的目錄</td>
    </tr>
    <tr>
        <td>/bin</td>
        <td>放置單人維護模式下還能夠被操作的指令</td>
    </tr>
    <tr>
        <td>/boot</td>
        <td>放置開機會使用到的檔案，包括Linux核心檔案與開機選單以及開機所需設定檔<br />
        Linux kernel常用的檔名為：vmlinuz，如果使用的是grub2開機管理程式，就還會存在/boot/grub2/的目錄</td>
    </tr>
    <tr>
        <td>/dev</td>
        <td>任何裝置與周邊設備都是以檔案的型態存在於這個目錄<br />
        比較重要的檔案有：<strong>/dev/null, /dev/zero, /dev/tty, /dev/loop*, /dev/sd*</strong> 等</td>
    </tr>
    <tr>
        <td>/bin</td>
        <td>系統主要的設定檔幾乎都放置在這個目錄內，例如人員的帳號密碼檔、各種服務的啟始檔<br />
        這個目錄下的各檔案屬性是可讓一般使用者查閱的，但是只有root有權力修改<br />
        FHS建議不要放置可執行檔(binary)在這裡<br />
        比較重要的檔案有：<strong>/etc/modprobe.d/, /etc/passwd, /etc/fstab/, /etc/issue</strong> 等<br />
        FHS還規範幾個重要的目錄最好要存在/etc/目錄下：<br />
            <ul>
                <li>/etc/opt(必要)：放置第三方協助軟體 <strong>/opt</strong>的相關設定檔</li>
                <li>/etc/X11(建議)：與 <strong>X Window</strong> 有關的各種設定檔，尤其是 <strong>xorg.conf</strong> 這個 X Server 的設定檔</li>
                <li>/etc/sgml(建議)：與 SGML格式有關的個項設定檔</li>
                <li>/etc/xml(建議)：與 XML格式有關的各項設定檔</li>
            </ul>
        </td>
    </tr>
    <tr>
        <td>/lib</td>
        <td>放置開機時會用到的函式庫，以及在/bin或/sbin底下的指令會呼叫的函式庫<br /><ul><li>/lib/modules/：主要放置可抽換式的核心相關模組(驅動程式)</li></ul></td>
    </tr>
    <tr>
        <td>/media</td>
        <td>放置可移除的裝置</td>
    </tr>
    <tr>
        <td>/mnt</td>
        <td>暫時掛載某些額外的裝置，建議可以放到這個目錄</td>
    </tr>
    <tr>
        <td>/opt</td>
        <td>給第三方協力軟體放置的目錄</td>
    </tr>
    <tr>
        <td>/run</td>
        <td>放置系統開機後所產生的各項資訊</td>
    </tr>
    <tr>
        <td>/sbin</td>
        <td>放置開機過程中所需要的，包括開機、修復、還原系統所需要的指令<br />常見的指令有：fdisk, fsck, ifconfig, mkfs</td>
    </tr>
    <tr>
        <td>/srv</td>
        <td>service的縮寫，一些網路服務啟動後，所需要取用的資料目錄</td>
    </tr>
    <tr>
        <td>/tmp</td>
        <td>讓使用者或是正在執行的程序暫時存放的目錄，重新開機時會清空目錄底下的全部資料</td>
    </tr>
    <tr>
        <td>/usr</td>
        <td>第二層FHS設定，下面會說明</td>
    </tr>
    <tr>
        <td>/var</td>
        <td>第二層FHS設定，主要放置變動性的資料，下面會說明</td>
    </tr>
    <tr>
        <td colspan="2">第二部份：FHS建議可以存在的目錄</td>
    </tr>
    <tr>
        <td>/home</td>
        <td>系統預設的使用者家目錄(home directory)，新增一個一般使用者帳號時，預設的使用者家目錄都會規範到這裡<br />
        <strong>家目錄有兩種代號</strong>：<br />
        <ul>
            <li>~ ：代表目前這個使用者的家目錄</li>
            <li>~chenhsiang ：代表 chenhsiang 的家目錄</li>
        </ul>
        </td>
    </tr>
    <tr>
        <td>/lib<qual></td>
        <td>存放與 /lib 不同格式的二進位函式庫</td>
    </tr>
    <tr>
        <td>/root</td>
        <td>系統管理員(root)的家目錄</td>
    </tr>
</table>

FHS針對根目錄定義的標準就是上面表格的內容，不過Linux底下還有許多目錄也需要瞭解：

|目錄|應放置檔案內容|
|---|---|
|/lost+found|使用標準的`ext2`/`ext3`/`ext4`檔案系統格式才會產生的目錄，當檔案系統發生錯誤時，將一些遺失的片段放到這個目錄下<br />如果是使用xfs檔案系檔，就不會存在這個目錄|
|/proc|本身是一個「虛擬檔案系統(virtual filesystem)」，放置的資料都是在記憶體中，本身不佔任何硬碟空間<br />例如系統核心、行程資訊(process)、周邊裝置的狀態及網路狀態等<br />比較重要的檔案：`/proc/cpuinfo`, `/proc/dma`, `/proc/interrupts`, `/proc/ioports`, `/proc/net/*`等|
|/sys|跟`/proc`類似，也是一個虛擬檔案系統，也是不佔用硬碟空間，主要是紀錄核心與系統硬體資訊相關的資訊<br />包含目前已載入的核心模組與核心偵測到的硬體裝置資訊等|

---

### /usr 的意義與內容
/usr 裡面放置的資料屬於可分享的與不可變動的
**usr是`Unix Software Resource`的縮寫**，是「Unix 作業系統軟體資源」所放置的目錄
FHS 建議所有的軟體開發者，應該將資料合理的分別放置到這個目錄下的次目錄，而不要自行建立該軟體獨立的目錄
這個目錄有點類似 Windows系統的「C:\Windows\(其中的一部份) + C:\Program files\」這兩個目錄的綜合體
系統剛安裝好時，這個目錄會佔用最多的硬碟容量
一般來說，/usr的次目錄建議有底下這些：

<table>
    <tr>
        <th>目錄</th>
        <th>應放置檔案內容</th>
    </tr>
    <tr><td colspan="2">第一部份：FHS 要求必須要存在的目錄</td></tr>
    <tr>
        <td>/usr/bin</td>
        <td>放置一般用戶能使用的指令</td>
    </tr>
</table>