---
title: 串列的操作與運用
categories: Python
tags: python, list
---
本篇將學習如何以迴圈來遍訪整個串列，
不管串列有多長，只需要幾行程式碼就搞定。

### 迴圈遍訪整個串列
在程式設計時常需要遍訪整個串列的所有項目，並對每個項目進行相同的操作處理。

<!-- more -->

可使用`Python` 的 for 迴圖來完成：
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


#### for 迴圖結束後的處理

### 避免縮排的誤用
#### 忘了縮排
#### 忘了縮排其它程式行
#### 不需要的縮排
#### 迴圈之後不需要的縮排
#### 忘記加冒號

### 建立數字串列
#### 使用 range()函式
#### 使用 range()製作數字串列
#### 數字串列的簡單統計運算
#### 串列推導解析

### 處理串列中某部份的內容
#### 切片
#### 迴圈遍訪切片
#### 複製串列