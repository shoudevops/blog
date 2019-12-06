---
title: if 陳述句 － 條件檢測
categories: Python
tags: 'python, conditional test, if'
date: 2019-12-02 10:06:57
---

程式設計的工作中常會碰到要檢查一組條件，並依據條件來進行對應的處理。
`Python` 的 if 陳述句能檢查程式目前的狀況，並依據該狀況來進行適當的回應。

### 從簡單的範例開始

<!-- more -->

例如有個串列裡存放了汽車廠牌，對大多數廠片來說，首字要以大寫字母呈現，但 BMW 要全部都大寫，
以下示範怎麼用 if陳述句正確地回應處理特別的情況：
```python
cars = ['audi', 'bmw', 'subaru', 'toyota']

for car in cars:
    if car == 'bmw':
        print(car.upper())
    else:
        print(car.title())
```
for 迴圈中會先檢查目前的廠牌名稱是否為 'bmw'，
如果是，則以全部大寫來輸出，不然就是首字大寫來輸出：
```text
Audi
BMW
Subaru
Toyota
```

---

### 條件檢測
每一條 if 陳述句的核心就是表示式，它會運算求值為`True`或`False`的結果，這個表示式就稱為條件檢測（ conditional test ）。
`Python`會依據條件檢測的結果來決定是否要執行 if 陳述句內的程式碼。

#### 檢查是否相等
大部份的條件檢測中都是對變數內目前的值與特定的值進行比較，最簡單的就是檢查變數的值是否與特定值相等：
```text
>>> car = 'bmw'
>>> car == 'bmw'
True
```
先把 'bmw' 指定到變數內，接著用兩個等號檢查變數中的值是否等於 'bmw'。
當變數中的值不是 'bmw' 時，就會返回`False`：
```text
>>> car = 'audi'
>>> car == 'bmw'
False
```

#### 檢查是否相等時忽略大小寫
`Python` 中檢查是否相等時是有區分大小寫的：
```text
>>> car = 'Audi'
>>> car == 'audi'
False
```
若不想區分大小寫，可以先把變數的值轉換成小寫再來比較：
```text
>>> car = 'Audi'
>>> car.lower() == 'audi'
True
```
且lower() 函式不會變更存放在變數的值：
```text
>>> car = 'Audi'
>>> car.lower() == 'audi'
True
>>> car
'Audi'
```

#### 檢查是否不相等
若想檢查兩個值是否不相等，可用驚嘆號和等號（ != ）所組合的運算子來處理：
```python
requested_topping = 'mushrooms'

if requested_topping != 'anchovies':
    print("Hold the anchovies!")
```
若變數與值不相等，`Python` 會返回`True` 並執行 if 陳述句後面的程式；
若這兩個值相等則返回`False` ，因此不會執行 if 陳述句後面的程式：
```text
Hold the anchovies!
```

#### 數值的比較
比較檢查數值是很直接的：
```text
>>> age = 18
>>> age ==18
True
```
還可以檢查兩個數值是否不相等，若不相等時輸出一條文字訊息：
```python
answer = 17

if answer != 42:
    print("That is not the correct answer. Please try again!")
```
answer（ 17 ）不等於42，條件滿足，因此會執行內縮的程式區塊：
```text
That is not the correct answer. Please try again!
```
在條件陳述句中可放入各種數學的比較：
```text
>>> age = 19
>>> age < 21
True
>>> age <= 21
True
>>> age > 21
False
>>> age >=21
False
```

#### 檢測多個條件
有可需會同時間需檢測多個條件，在這種狀況下，`and`和`or`關鍵字能幫得上忙

##### 使用 and 檢測多個條件
若要檢測兩個條件是否為`True`，可用 and 關鍵字把兩個條件連結起來，
如果兩個條件都是 True，則整個連結起來的表示式就為 True，
若只要有一個條件是 False，則整個表示式就為 False：
```text
>>> age_0 = 22
>>> age_1 = 18
>>> age_0 >= 21 and age_1 >= 21
False
>>> age_1 = 22
>>> age_0 >= 21 and age_1 >= 21
True
```
若要增加可讀性，可以將每個單獨的檢測條件用括弧括起來，但這並不是必要的處理：
```text
(age_0 >= 21) and (age_1 >= 21)
```

##### 使用 or 檢測多個條件
or 關鍵字也允許進行多個條件的檢測，只要有一個條件滿足，就能通過整個檢測。
若以 or 連接兩個條件，只有在兩個條件都沒通過時，整個 or 表示式才會是 False：
```text
>>> age_0 = 22
>>> age_1 = 18
>>> age_0 >= 21 or age_1 >= 21
True
>>> age_0 = 18
>>> age_0 >= 21 or age_1 >= 21
False
```

#### 檢測某個特定值是否在串列之中
在進行處理動作之前有件重要的事是，先檢測某個特定值是否有在串列之中，
若要判別某個特定值是否在串列之後，可以使用 `in` 關鍵字來配合：
```text
>>> requested_toppings = ['mushroom', 'onions', 'pineapple']
>>> requested_toppings = ['mushrooms', 'onions', 'pineapple']
>>> 'mushrooms' in requested_toppings
True
>>> 'pepperoni' in requested_toppings
False
```

#### 檢測某個特定值是否不在串列中
有些時候想要確定在串列中並沒有存放某個特定值，在這樣的情況下，可使用 `not in` 關鍵字來協助：
```python
banned_users = ['andrew', 'carolina', 'david']
user = 'marie'

if user not in banned_users:
    print(user.title() + ", you can post a response if you wish.")
```
如果 user的值沒有在 banned_users串列中，Python 會返回True，下到內縮的程式區塊會執行：
```text
Marie, you can post a response if you wish.
```

#### 布林表示式
當學習更多關於程式設計的課題，就會遇到「布林表示式（ Boolean  expression）」，
它只是條件檢測的另一個稱呼而已。與條件檢測的表示式一樣，布林表示式的求值結果一定是`True`或`False`：
```python
game_active = True
can_edit = False
```