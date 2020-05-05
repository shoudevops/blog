---
title: Linux 目錄
date: 2020-05-05 14:40:45
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
        <td>/lib&lt;qual&gt;</td>
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
這個目錄有點類似 Windows系統的「`C:\Windows\(其中的一部份)` + `C:\Program files\`」這兩個目錄的綜合體
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
        <td>Ubuntu：放置一些非必要性的指令，主要是一些第三方協力軟體的執行程式<br />CentOS 7~：全部的使用者指令都放置於此目錄，並使用連結檔的方式將 /bin 連結到此目錄</td>
    </tr>
    <tr>
        <td>/usr/lib</td>
        <td>Ubuntu：用來放置 /usr/bin 的程式會用到的函式庫<br />CentOS 7~：基本上與 /lib 功能相同，所以 /lib 就是連結到此目錄中的</td>
    </tr>
    <tr>
        <td>/usr/local</td>
        <td>系統管理員在本機自行安裝自已下載的軟體（非Distribution預設提供者），建議安裝到此目錄比較便於管理</td>
    </tr>
    <tr>
        <td>/usr/sbin</td>
        <td>Ubuntu：放置一些使用者安裝的系統管理的必要程式，例如：dhcpd, httpd等<br />CentOS 7~：非系統正常運作所需要的系統指令，基本功能與/sbin差不多，</td>
    </tr>
    <tr>
        <td>/usr/share</td>
        <td>主要放置唯讀架構的資料檔案，幾乎是不分硬體架構均可讀取的資料，因為幾乎都是文字檔案<br />此目錄下常見的還有這些次目錄：
        <ul>
            <li>/usr/share/man：線上說明文件</li>
            <li>/usr/share/doc：軟體雜項的文件說明</li>
            <li>/usr/share/zoneinfo：與時區有關的時區檔案</li>
        </ul></td>
    </tr>
    <tr><td colspan="2">第二部份：FHS 建議可以存在的目錄</td></tr>
    <tr>
        <td>/usr/games/</td>
        <td>與遊戲比較相關的資料放置處</td>
    </tr>
    <tr>
        <td>/usr/include/</td>
        <td>C/ C++等程式語言的檔頭(header)與包含檔(include)放置處<br /></td>
    </tr>
    <tr>
        <td>/usr/libexec/</td>
        <td>放置某些不被一般使用者慣用的執行檔或腳本(script)等，例如大部份的 X視窗底下的操作指令</td>
    </tr>
    <tr>
        <td>/usr/lib&lt;qual&gt;</td>
        <td>與 /lib&lt;qual&gt; 功能相同，/lib&lt;qual&gt; 就是連結到此目錄中</td>
    </tr>
    <tr>
        <td>/usr/src</td>
        <td>一般原始碼放置的位置，src有source的意思。核心原始碼建議放置到 /usr/src/linux/ 目錄下</td>
    </tr>
</table>

---

### /var 的意義與內容
/usr 是安裝時會佔用較大硬碟容量的目錄，/var 是系統運作後會漸漸佔用硬碟容量的目錄
因為 /var目錄主要針對常性變動的檔案，包括快取(cache)、登錄檔(log file)及某些軟體運作所產生的檔案
包括程序檔案(lock file, run file)，或者例如MySQL資料庫的檔案等
當見的次目錄有：
<table>
    <tr>
        <th>目錄</th>
        <th>應放置檔案內容</th>
    </tr>
    <tr><td colspan="2">第一部份：FHS 要求必須要存在的目錄</td></tr>
    <tr>
        <td>/var/cache/</td>
        <td>應用程式本身運作過程中會產生的一些暫存檔</td>
    </tr>
    <tr>
        <td>/var/lib/</td>
        <td>程式本身執行的過程中，需要使用到的資料檔案放置的目錄。在此目錄下各自的軟體應該要有各自的目錄<br />例如 MySQL的資料庫放置到 /var/lib/mysql，而 rpm的資料庫則放到 /var/lib/rpm</td>
    </tr>
    <tr>
        <td>/var/lock/</td>
        <td>某些裝置或檔案資源，一次只能被一個應用程式使用，如果同時有兩個程式使用該裝置時就會產生錯誤，因此就要將該裝置上鎖(lock)，確保該裝置只會給單一軟體使用。<br />目前此目錄也已經移到 /run/lock中</td>
    </tr>
    <tr>
        <td>/var/log</td>
        <td>登錄檔放置的目錄，比較重要的檔案如 /var/log/messages, /var/log/wtmp(紀錄登入者的資訊)等</td>
    </tr>
    <tr>
        <td>/var/mail</td>
        <td>放置個人電子郵件的目錄，此目錄也被放置到 /var/spool/mail 目錄中，通常這兩個目錄是互為連結檔</td>
    </tr>
    <tr>
        <td>/var/run</td>
        <td>某些服務或程式啟動後，會將它們的 PID放置在這個目錄下。<br />與 /run 相同，這個目錄連結到 /run </td>
    </tr>
    <tr>
        <td>/var/spool</td>
        <td>通常放置一些佇列資料（「佇列」就是排隊等待其它程式使用的資料），這些資料被使用後通常都會被刪除<br />如果是工作排程資料(crontab)，就會被放置到 /var/spool/cron/ 目錄中</td>
    </tr>
</table>

---

### 針對 FHS，各家Distributions的差異
由於 FHS僅是定義出最上層(/)與次層(/usr, /var)的目錄內容應該要放置的檔案或目錄資料
因此，在其它次目錄層級內，就可以隨開發者自行配置，但記住大致的 FHS標準，差異性其實有限