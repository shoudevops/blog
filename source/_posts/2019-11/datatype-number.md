---
title: 數值
categories: Python
tags:
- python
- datatype
- number
date: 2019-11-22 09:05:29
---
在程式設計中很常使用「數值」來記錄遊戲的分數、呈現視覺化的資料、儲存Web 應用程式的資訊等。

### 整數
在`Python`中可以對整數進行+（加）、-（減）、*（乘）、/（除）的運算。
```python
>>> 2 + 3
5
>>> 3 - 2
1
>>> 2 * 3
6
>>> 3 / 2
1.5
```

<!-- more -->

`Python`使用 **（兩個乘號）來表示次方的運算
```python
>>> 3 ** 2
9
>>> 3 ** 3
27
>>> 10 ** 6
1000000
```
`Python`也支援運算順序，因此可以在一個表示式中使用多個運算子，
也可以使用括號來改變運算的順序，讓`Python`依照指定的順序運算
```python
>>> 2 + 3 * 4
14
>>> (2 + 3) * 4
20
```

---

### 浮點數
`Python`將帶有小數點的數值都稱為浮點數（float），
使用浮點數只需輸入想要使用的數值，`Python`都會以我們所期待的方式來遲算和處理：
```python
>>> 0.1 + 0.1
0.2
>>> 0.2 + 0.2
0.4
>>> 2 * 0.1
0.2
>>> 2 * 0.2
0.4
```
但請注意得到的運算結果，小數位有可能不是那麼精確：
```python
>>> 0.2 + 0.1
0.30000000000000004
>>> 3 * 0.1
0.30000000000000004
```
所有程式語言都有這樣的問題，不用擔心，
`Python`會盡可能找出最精確的方式來表示結果，但受限於電腦內部表示數值的方式，
所以有時會很難十分精確。

---

### 使用 str() 函式避開型別錯誤
我們常會在顯示訊息中用到變數的值：
```python
age = 23
message = "Happy " + age + "rd Birthday!"

print(message)
```
看似簡單沒有錯誤的祝福句：Happy 23rd Birthday!，
但執行後卻出現錯誤：
```text
Traceback (most recent call last):
  File "syntax_error.py", line 2, in <module>
    message = "Happy " + age + "rd Birthday!"
TypeError: can only concatenate str (not "int") to str
```
這是型別錯誤(TypeError)，意思是`Python`不能辨識我們所用的資訊類型。

`Python`發現程式使用了一個含有整數值的變數，但不知道如何直譯這個值。
`Python`知道這個變數可以表示為數值23，也可以表示字元2和字元3。
且字串連接了含有整數值的變數，因此產生了類型不一致，需要指定`Python`把數值當成字串。
```python
age = 23
message = "Happy " + str(age) + "rd Birthday!"

print(message)
```
`Python`現在知道把數值23轉換成字串，就會得到我們希望且沒有錯誤的訊息：
```text
Happy 23rd Birthday!
```
