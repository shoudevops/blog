---
title: 儲存資料
categories: Python
tags:
  - python
  - data processing
date: 2019-12-27 18:21:30
---

本篇會學習 json 模組，這個模組能幫我們儲存使用者的資料，以免在程式停止執行後就消失掉。

### 儲存資料
許多程式都會要求使用者輸入某種資訊，不管程式的焦點在哪裡，
都是要把使用者所提供的資訊存放到串列和字典等資料結果內。
使用者關閉程式時，我們大都會希望把這些資訊都保存下來，

<!-- more -->

這裡提供的簡單方式就是用 json 模組來儲存資料。

json 模組能讓我們把簡單的 `Python` 資料結構轉成到檔內，並在程式再次執行時載入這份檔案內的資料。
我們還可以利用 json 模組，讓 `Python` 程式彼此可共享資料。
更重要的是，JSON 資料格式並不是 `Python` 專用的，這能讓我們把以 JSON 格式儲存的資料與使用其它程式語言的人可以共用分享。
這是種輕便、好用又容易學習的格式。

*JSON(JavaScript Object Notation) 格式最初是為 JavaScript 所開發的格式，*
*但之後就普遍成為一種常見的格式，也被 Python 等許多程式語言採用。*

#### 使用 json.dump() 和 json.load()
嘗試編寫一支簡短的程式來儲存一組數字，然後再編寫一支程式把這組數字讀取回記憶體中。
前面的程式要用 json.dump() 來儲存這組數字，後面的程式則用 json.load() 將這組數字載入。

json.dump() 函試接收兩個引數，第一個是儲存的資料，第二個是用來儲存資料的檔案物件。
下最範例示範如何使用 json.dump() 儲存數字串例：
```python
import json

numbers = [2, 3, 5, 7, 11, 13]

filename = 'numbers.json'
with open(filename, 'w') as f_obj:
    json.dump(numbers, f_obj)
```
先匯入 json 模組，再建立一個數字串列。
指定要把數字串列儲存進去的檔案名稱(.json)。
在 with 程式下使用 json.dump() 函式把數字串列儲存到 numbers.json 檔案內。

這支程式執行後並沒有輸出顯示，但我們可以開啟 numbers.json 檔，存放在這個檔案內的資料與在 `Python` 中是一樣的：
```text
[2, 3, 5, 7, 11, 13]
```
再編寫一支程式，使用 json.load() 把這個串列讀取到記憶體內：
```python
import json

filename = 'numbers.json'
with open(filename) as f_obj:
    numbers = json.load(f_obj)

print(numbers)
```
我們確定讀取的是前面寫入的檔案，這次以讀取模式來開啟這份檔案，因為 `Python` 只需讀取不用寫入。
在 with 程式區塊內用 json.load() 載入存放在 numbers.json 檔內的資訊，並將其指定到 numbers 變數中。
最後印出這個數字串列，看是否為 json.dump() 範例中所建立的數字串列：
```text
[2, 3, 5, 7, 11, 13]
```
這是一種在程式之間可共享資料的簡單處理方式。

#### 儲存和讀取使用者生成的資料
在處理使用者生成的資料時，使用 json 格式來儲存是很有助益的，
因為如果不以某種方式儲存，等程式結束後使用者的資訊就會被丟掉。
以下範例是使用者在第一次執行程式時會被提示輸入自己的名字，
等再次執行時程式能記得這個名字，從儲存使用者的名字開始：
```python
import json

username = input("What is your name? ")

filename = 'username.json'
with open(filename, 'w') as f_obj:
    json.dump(username, f_obj)
    print("We'll remember you when you come back, " + username + "!")
```
先提示輸入名字，並將輸入存放到變數中。
隨後呼叫 json.dump() , 以使用者名字和檔案物件當引數傳入，讓使用者名字儲存入檔案內。
最後輸出一條訊息，告知我們儲存了使用者所輸入的資訊：
```text
What is your name? Charles
We'll remember you when you come back, Charles!
```
再讓我們編寫一支程式，對已存的使用者發出問候文句：
```python
import json

filename = 'username.json'

with open(filename) as f_obj:
    username = json.load(f_obj)
    print("Welcome back, " + username + "!")
```
這邊使用了 json.load() 把儲存在 username.json 中的資訊讀取到 username 變數內，
載入回復使用者名字後，就可以發出歡迎回來的問候文句：
```text
Welcome back, Charles!
```
再來需要把這兩支程式合併成一支，等這支程式執行時，就會嘗試從 username.json 檔中取出使用者名字，
因此我們要先編寫一個試著回復使用者名字的 try 程式碼區塊，如果檔案不存在，
就在 except 程式碼區塊中執行提示使用者輸入名字的處理，並把輸入儲存到 username.json 中，
方便程式再次執行時能載入回復：
```python
import json

# Load the username, if it has been stored previously.
#  Otherwise, prompt for the username and store it.

filename = 'username.json'
try:
    with open(filename) as f_obj:
        username = json.load(f_obj)
except FileNotFoundError:
    username = input("What is your name? ")
    with open(filename, 'w') as f_obj:
        json.dump(username, f_obj)
        print("We'll remember you when you come back, " + username + "!")
else:
    print("Welcome back, " + username + "!")
```
先試著開啟 username.json 檔，如果檔案存在，就把檔案內的伬畢者名字載入到記憶體中，
再執行 else 程式碼區塊，輸出一條歡迎回來的訊息文字。
當第一次執行程式時， username.json 並不存在，此時會引發 FileNotFoundError 例外，
因此 `Python` 會執行 except 程式碼區塊，提供使用者輸入名字，再使用 json.dump() 儲存這個名字，
再輸出一句問候文句。  

無論執行的是 except 程式碼區塊還是 else 程式碼區塊，
都會顯示使用者名字和適當的問候文句，如果這支程式第一次執行，
其輸出如下所示：
```text
What is your name? Charles
We'll remember you when you come back, Charles!
```
如果已執行過，則輸出如下所示：
```text
Welcome back, Charles!
```
這是程式之前已至少執行過一次時會呈現的輸出結果。
