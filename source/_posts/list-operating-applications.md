---
title: 串列的操作與運用
categories: Python
tags: 'python, list'
date: 2019-11-28 01:17:58
---

本篇將學習如何以迴圈來遍訪整個串列，
不管串列有多長，只需要幾行程式碼就搞定。

### 迴圈遍訪整個串列
在程式設計時常需要遍訪整個串列的所有項目，並對每個項目進行相同的操作處理。

<!-- more -->

可使用`Python` 的 for 迴圈來完成：
```python
magicians = ['alice', 'david', 'carolina']
for magician in magicians:
    print(magician)
```
在第二行定義`for`迴圈，告知`Python`從magicians 串列中取出名字，並將它存放到magician變數內。
在第三行告訴`Python`把存放在 magician變數內的名字輸出。
之後`Python`會對串列中的每個名稱重覆執行第二行和第三行。
```text
alice
david
carolina
```
在編寫 for 迴圈時，可以取任一個合法的名字用於存放串列中每一個值的臨時變數。
不過還是建議取個具有描述性又有意義的名字是比較好的：
```text
for magician in magicians:
for car in cars:
for item in list_of items:
```
這種取名的慣例有助於讓大家明白 for 迴圈中對每個項目要進行操作處理。
利用英文單字的單數和複數來命名，能協助判斷這段程式是處理單個項目還是整個串列。

#### 在 for 迴圈中進行更多操作
在 for 迴圈中可對每個項目執行任何的操作：
```python
magicians = ['alice', 'david', 'carolina']
for magician in magicians:
    print(magician.title() + ", that was a great trick!")
```
輸出的內容是對串列中每位魔術師都印出一條屬於他個人的訊息：
```text
Alice, that was a great trick!
David, that was a great trick!
Carolina, that was a great trick!
```
之後想在 for 迴圈中放多少行程式碼都可以，在 for magician in magicians 這行程式之後，
每行縮排的程式碼都算在迴圈之內，且都會對串列中每個項目執行一次。
接著可以新增第二行程式碼輸出另一條訊息：
```python
magicians = ['alice', 'david', 'carolina']
for magician in magicians:
    print(magician.title() + ", that was a great trick!")
    print("I can't wait to see your next trick, " + magician.title() + ".\n")
```

#### for 迴圈結束後的處理
在 for 迴圈之後沒有縮排的程式碼都只執行一次，不會重覆：
```python
magicians = ['alice', 'david', 'carolina']
for magician in magicians:
    print(magician.title() + ", that was a great trick!")
    print("I can't wait to see your next trick, " + magician.title() + ".\n")

print("Thank you, everyone. That was a great magic show!")
```
最後一行的 print陳述句沒有縮排，它不屬於 for 迴圈，不會重覆執行，只在迴圈結束後再執行一次：
```text
Alice, that was a great trick!
I can't wait to see your next trick, Alice.

David, that was a great trick!
I can't wait to see your next trick, David.

Carolina, that was a great trick!
I can't wait to see your next trick, Carolina.

Thank you, everyone. That was a great magic show!
```
使用 for 迴圈來處理資料，會發覺這是彙總整個資料集執行操作的好方法。

---

### 避免縮排的誤用
`Python`會依據這行程式的縮排(indentation)來判斷與前一行程式的連結，並利用縮排讓程式變得更易讀，
基本上它就是要我們使用空白縮排來讓程式碼整齊而結構分明。
開始運用適當的縮排來編寫程式時，需要注意一些常見的縮排錯誤。

#### 忘了縮排
在 for 陳述句後面屬於迴圈的程式行都要縮排，如果忘了縮排，`Python` 會顯示錯誤訊息提醒：
```python
magicians = ['alice', 'david', 'carolina']
for magician in magicians:
print(magician)
```
在 for 迴圈內的print 陳述句應該要縮排卻沒有縮排，當`Python` 找不到縮排的程式區堆時，
會讓您知道哪一行程式碼可能有問題：
```text
  File "text.py", line 3
    print(magician)
        ^
IndentationError: expected an indented block
```
只要把 for 陳述句後面的程式行或程式區塊縮排，就能修正這樣的錯誤。

#### 忘了縮排其它程式行
有時迴圈能執行且不會報錯，但輸出的結果不是想要的內容；
在迴圈中進行多項工作卻忘了縮排某行程式，這種情況就會發生：
```python
magicians = ['alice', 'david', 'carolina']
for magician in magicians:
    print(magician.title() + ", that was a great trick!")
print("I can't wait to see your next trick, " + magician.title() + ".\n")
```
第二條print陳述句原本要縮排，但因為已滿足`Python` 要 for 陳述句後至少要有一行縮排的程式行，因此執行後不會有錯誤訊息。
```text
Alice, that was a great trick!
David, that was a great trick!
Carolina, that was a great trick!
I can't wait to see your next trick, Carolina.
```
由於magician 變數最後迴圈存放的值為`carolina`，因此就只印出「I can’t wait to see your next trick, Carolina.」。
這算是個邏輯錯誤（logical error）。從語法上來看都是合法的，但有邏輯上的錯誤，導致執行結果不是我們想要的。

#### 不需要的縮排
如果程式中不小心縮排了不需要縮排的程式行，`Python` 會顯示意外縮排的錯誤訊息：
```text
  File "text.py", line 2
    print(message)
    ^
IndentationError: unexpected indent
```
為了避免意外縮排的錯誤，在縮排程式行時要小心。

#### 迴圈之後不需要的縮排
如果不小心把應在迴圈結束後才執行的程式行縮排了，該程式行就會跟著迴圈對每個串列中的項目重覆執行。
有些時候`Python` 會回報錯誤訊息，但大多數都是邏輯錯誤，不會顯示錯誤訊息：
```python
magicians = ['alice', 'david', 'carolina']
for magician in magicians:
    print(magician.title() + ", that was a great trick!")
    print("I can't wait to see your next trick, " + magician.title() + ".\n")

    print("Thank you, everyone. That was a great magic show!")
```
這是個邏輯錯誤，與前面「忘了縮排其它程式行」的錯誤相似，
如果原本設計的只應該執行顯示一次卻執行了多次，請確定是否對程式行做了不需要的縮排。
```text
Alice, that was a great trick!
I can't wait to see your next trick, Alice.

Thank you, everyone. That was a great magic show!
David, that was a great trick!
I can't wait to see your next trick, David.

Thank you, everyone. That was a great magic show!
Carolina, that was a great trick!
I can't wait to see your next trick, Carolina.

Thank you, everyone. That was a great magic show!
```

#### 忘記加冒號
在 for 陳述句尾端的冒號是用來告訴Python下一行是迴圈的開始：
```python
magicians = ['alice', 'david', 'carolina']
for magician in magicians:
    print(magician)
```
如果忘了加冒號，就會導致語法錯誤，因為Python不知道您想要做什麼。
雖然這個簡單的錯誤很容易修正，但卻不容易發現。

---

其它更多關於串列的操作與運用，請看 `Part II.`。
