---
title: Linux 檔案權限介紹
categories: Linux
tags: linux
date: 2020-04-17 17:25:37
---

各個元件或裝置在Linux底下都是「一個檔案」，每個檔案都有相當多的屬性與權限，
其中最重要的就是檔案的擁有者與群組的概念了。

### Linux 檔案屬性

先介紹查看檔案的指令：
```
ls -al
```
顯示當前目錄路徑下有什麼檔案與屬性

<!-- more -->

{% asset_img list-file.jpg 查看檔案 %}
> ls是「list」的意思，「-al」選擇表示列出所的的檔案詳細權限與屬性
> 檔名開頭是「.」的表示隱藏檔案

```
-rw-r--r-- 1 chenhsiang chenhsiang 655 Apr 16 14:35 .profile
```

#### 檔案類型與權限
```
-rw-r--r--
```
最重要也最需要注意的就是這裡！這一欄共有十個字元
+ 第一個字元代表這個檔案是`目錄、檔案或連結檔等等`：
    - [d]是目錄，例如上圖的`.cache`那一行
    - [-]是檔案，例如上圖的`.profile`那一行
    - [l]表示為連結檔（link file)
    - [b]表示為裝置檔案內可供儲存的週邊設備(可隨機存取裝置)
    - [c]表示為裝置檔案內的序列埠設備，例如鍵盤、滑鼠（一次性讀取裝置）

+ 接下來的九個字元中，以三個為一組，且均為「rwx」的三個參數組合。「r」代表可讀（read）、「w」代表可寫（write）、「x」代表可執行（execute）。這三個權限的位置不會改變，如果沒有權限，裝會出現「-」。
    - 第一組為「檔案擁有者可具備的權限」，以上圖的「.profile」檔案為例，它的擁有者可以讀寫但不可執行
    - 第二組為「加入此群組帳號的權限」
    - 第三組為「非本人且沒有加入本群組的其它帳號的權限」

#### 檔案權限的重要性
Linux 檔案系統的每個檔案都加了很多屬性，最大的用途是在「資料安全性」

##### 系統保護的功能
例如帳號管理的檔案`/etc/shadow`，紀錄系統中所有帳號資料，因此只有root能讀取，該檔案的權限就會是「----------」，看起來像是所有人都不能使用，但root不受系統的權限限制，所以不管什麼檔案權限，root都可以存取。

##### 團隊開發軟體或資料共用的功能
如果希望每個在團隊的人都可以使用某個目錄下的檔案，而非團隊的人則不能存取，
就可以先檔案權限設定為「-rwxrws---」提供給同一個Group使用。
> 上面的`s`屬性是Set GID(SGID)的意思，只對目錄有效
> 1. 目錄被設置後，任何用戶在此目錄下建立的文件，所屬群組皆與該目錄所屬的群組相同
> 2. 可使用在特定多人團隊的專案開發上

##### 未將權限設定妥當的危害
如果目錄權限沒有設定好，可能造成其它人都可以在你的系統上隨意操作，
因此修改Linux檔案與目錄的屬性前，一定要先搞清楚，什麼資料是可變的，什麼是不可變的！

### 改變檔案屬性與權限
先介紹幾個常用於群組、擁有者、各種身份的權限之修改的指令：
> chgrp ：改變檔案所屬群組
> chown ：改變檔案擁有者
> chmod ：改變檔案的權限, SUID, SGID, SBIT等等的特性

#### 改變所屬群組：chgrp
就是`change group`的縮寫，要被改變的群組名稱必須要在`/etc/group`檔案內存在才行。否則會報錯。
完整的指令：
```
chgrp [-R] [GROUP] FILE
```
+ -R：進行遞迴(recursive)的持續變更，亦即連同次目錄下的所有檔案、目錄都更新成為這個群組之意。
常常用在變更某一目錄內所有的檔案之情況。
+ GROUP：群組名稱，要變更`$filename`到`$GROUP`群組

這裡先用`ls -al`指令查看目前檔案所屬群組
{% asset_img check-file-permission.jpg 查看所屬群組 %}
可以看到擁用者與所屬群組都是`chenhsiang`，接著用`chgrp`指令變更所屬群組
{% asset_img error-change-group.jpg 變更錯誤 %}
咦？這裡系統報錯了，原因是沒有`charles`這個群組
（前面有提到要在`/etc/group`這個檔案裡存在的群組才能變更）
{% asset_img change-group.jpg 變更群組並查看 %}
上圖我們就能看到已經改變檔案所屬的群組。

#### 改變檔案擁有者：chown
跟`chgrp`一樣，`chown`就是`change owner`的縮寫，使用者必須是已經存在系統中的帳號，
在`etc/passwd`這個檔案中有紀錄的使用者名稱才能改變。
`chown`還可以直接修改群組的名稱，**要將目錄下的所有目錄或檔案更改檔案擁有者，直接加上 -R 的選項即可**。
```
chown [-R] [OWNER] FILE
chown [-R] [OWNER]:[GROUP] FILE
```
試著變更檔案的擁有者給`bin`：
```
chown bin blog.txt
```
{% asset_img change-owner.jpg 變更擁有者 %}
再將擁有者與群組都變更為`root`：
```
chown root:root blog.txt
```
{% asset_img change-owner-root.jpg 變更擁有者與群組 %}
這樣就會同時修改檔案擁有者與所屬群組囉

#### 改變權限：chmod
權限設定的方法可以使用數字或是符號來進行變更

##### 數字類型改變檔案權限
檔案的基本權限有九個，分別是`owner/group/others`三種身份各有自己的`read/write/execute`權限，
各權限的分數對照如下：

+ r: 4
+ w: 2
+ x: 1

每種身份(owner/group/others)各自的三個權限(r/w/x)分數是需要累加的，
例如檔案權限是：[-rwxrwx---]，分數是：
+ owner = rwx = 4+2+1 = 7
+ group = rwx = 4+2+1 = 7
+ others = --- = 0+0+0 = 0

所以變更權限時的數字就是770
```
chmod [-R] MODE FILE
```
如果要將`blog.txt`這個檔案所有權限都設定啟用，那指令就是：
```
chmod 777 blog.txt
```
{% asset_img change-mode.jpg 變更檔案權限 %}
通當新增一個文字檔批次檔後，它的權限是 [-rw-rw-r--]也就是664，
如果要將該檔案變成可執行檔，並且不要讓其它人修改檔案的話，就需要[-rwxr-xr-x]，
這時候就要使用指令：
```
chmod 755 test.sh
```

如果有些檔案不想被其它人看到，那麼應該將檔案的權限設定為：[-rwxr-----]，
就要下`chmod 740 filename` 

##### 符號類型改變檔案權限
基本上九個權限分別是`owner(user)/group/others`三種身份，
可以由`u, g, o`來代表三種身份的權限，另外，`a`是代表`all`，也就是全部的身份，
讀寫的權限一樣是寫成`r, w, x`：

|chmod|u<br />g<br />o<br />a|+(加入)<br />-(除去)<br />=(設定)|r<br />w<br />x|檔案或目錄|
|---|:-:|---|---|---|

假如我們要將一個檔案的權限設定成[-rwxr-xr-x]時，基本上就是：
+ user(u)：具有可讀、可寫、可執行的權限；
+ group 與 others(g/o)：具有可讀與執行的權限。

所以就是：
```
chmod u=rwx,go=rx blog.txt
```
{% asset_img change-mode-symbo.jpg 用符號變更檔案權限 %}

如果不知道原先檔案屬性，而只想要增加 blog.txt 這個檔案的每個人均可寫人的權限，
那就可以使用指令：
```
chmod a+w blog.txt
```
{% asset_img change-mode-symbo-2.jpg 用符號變更檔案權限 %}

`+`與`-`的狀態下，只要是沒有指定到的項目，該權限**`不會被變動`**
假如想讓一個程式擁有可執行的權限，但又不知道該檔案原本的權限為何，此時利用：
```
chmod a+x filename
```
就可以讓該程式擁有執行的權限了。