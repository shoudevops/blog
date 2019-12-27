---
title: 儲存資料
categories: Python
tags:
- python
- data processing
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

```

#### 重構