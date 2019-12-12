---
title: 字典 － 介紹與使用
categories: Python
tags:
- python
- dictionary
date: 2019-12-04 19:04:25
---

本文章將會學習如果在字典中存取資訊，與如何修改這些資訊，
字典可儲存幾乎是無限的資訊內容，因此在下篇文章會解說如何以迴圈遍訪取用字典中的資料。
此外會學習把字典存入串列中、把串列存入字典內，以及把字典存入字典中。

<!-- more -->

---

### 單純的字典
以遊戲程式為例，遊戲中有一些顏色和得分都不相同的外星異形，下列用一個單純的字典存放關於特定外星異形的資訊：
```python
alien_0 = {'color': 'green', 'points': 5}

print(alien_0['color'])
print(alien_0['points'])
```
用print陳述句輸出從字得存得的資訊：
```text
green
5
```

---

### 使用字典
+ `Python` 中字典是一系列的鍵 － 值對（ key-value pairs ）。
+ 每個鍵（ key ）都有一個值（ value ）相關聯，可以畢鍵來存取與它關聯的值。
+ 與鍵相關聯的值可以是數值、字串、串列、另一個字典也可以。
+ 任何由 `Python` 所建立的物件（ object ）都可以當作字典的值。
+ 在`Python` 中字典是用大括號 {} 括住一系列的鍵 － 值對來呈現。
+ 鍵和值之間是用冒號：來分隔，而鍵 － 值對之間則用逗號分開。
+ 想要在字典中存入多少個鍵 － 值對都可以。

#### 存取字典中的值
若想取得與鍵相關聯的值，可給定字典的名稱，然後以中括號括住指定的鍵：
```python
alien_0 = {'color': 'green'}
print(alien_0['color'])
```
會返回alien_0中與'color'鍵相關的值：
```text
green
```
字典中可以放入任意數量的鍵 － 值對：
```python
alien_0 = {'color': 'green', 'points': 5}
```
現在可以存取 alien_0 字典的顏色和分數了：
```python
alien_0 = {'color': 'green', 'points': 5}

new_points = alien_0['points']
print("You just earned " + str(new_points) + " points!")
```
取得'points'鍵相關聯的值，並將值指定存到 new_points變數內。
接著將整數轉換成字串，連接訊息文字輸出：
```text
You just earned 5 points!
```

#### 新增鍵 － 值對
字典是動態結構，可隨時新增鍵 － 值對進去，先編寫字典名稱，再用中括號括住「鍵」，再指定相關聯的「值」進去：
```python
alien_0 = {'color': 'green', 'points': 5}
print(alien_0)

alien_0['x_position'] = 0
alien_0['y_position'] = 25
print(alien_0)
```
執行程式輸出修改新增的字典，就會看到剛新增的兩個鍵 － 值對在字典中：
```text
{'color': 'green', 'points': 5}
{'color': 'green', 'points': 5, 'x_position': 0, 'y_position': 25}
```
鍵 － 值對的排列順序與新都因順序不太一樣，因為`Python`不管字典中鍵 － 值對的排列順序，重點是在鍵和值之間的關聯。

#### 從建立空字典開始
先用一對大括號 {} 來定義空的字典，再分行逐一新增各鍵 － 值對：
```python
alien_0 = {}

alien_0['color'] = 'green'
alien_0['points'] = 5

print(alien_0)
```
一般來說，定義一個空字典用來儲存使用者提供的資料，或在編寫能自動產生大量鍵 － 值對資料的程式時才會使用。

#### 修改字典中的某個鍵對應的值
若想修改字典中的值，給定字典名稱、使用中括弧括住「鍵」，再把相關聯的新「值」指定過去即可：
```python
alien_0 = {'color': 'green'}
print("The alien is " + alien_0['color'] + ".")

alien_0['color'] = 'yellow'
print("The alien is now " + alien_0['color'] + ".")
```
將 'color' 鍵所關聯的值改指定為 'yellow'，從輸出結果看，這個字典的顏色已改成 'yellow'：
```text
The alien is green.
The alien is now yellow.
```

#### 刪除鍵 － 值對
當不再需要字典中的某些資訊時，可用 `del`陳述句把對應的鍵 － 值對徹底刪除掉。
使用 `del`陳述句時必須給定字典名稱和要刪除的鍵：
```python
alien_0 = {'color': 'green', 'points': 5}
print(alien_0)

del alien_0['points']
print(alien_0)
```
`del` 陳述句會讓 `Python`把`alien_0`字典中的 'points' 鍵和其關聯的值一起移除掉：
```text
{'color': 'green', 'points': 5}
{'color': 'green'}
```
#### 同類物件的字典
字典所存放的是個物件的多種資訊，但也可使用字典來儲存多個物件的同一種資訊：
```python
favorite_languages = {
    'jen': 'python',
    'sarah': 'c',
    'edward': 'ruby',
    'phil': 'python',
    }
```
當想要以多行的方式來定義和呈現字典時，在左大括號輸入後即按下 `Enter`鍵換行，
接著內縮四格空格，指定第一個鍵 － 值對，再加上逗號。
在定義和輸入好字典的內容後，在最後一個鍵 － 值對的下一行內縮四格空格並加上右大括號，讓它對齊字典中的鍵。
還有一種不錯的作法是在最後一個鍵 － 值對後面加上逗號，為以後新增鍵 － 值對作好準備。

若想要使用字典，可給定被調查者的鍵，就能從字典中擷取出對應的值：
```python
favorite_languages = {
    'jen': 'python',
    'sarah': 'c',
    'edward': 'ruby',
    'phil': 'python',
    }

print("Sarah's favorite language is " +
    favorite_languages['sarah'].title() +
    ".")
```
使用print 陳述句輸出了 Sarah 最愛的程式語言：
```text
Sarah's favorite language is C.
```
