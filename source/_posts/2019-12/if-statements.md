---
title: if 陳述句
categories: Python
tags:
- python
- if
date: 2019-12-03 18:09:36
---

### if 陳述句
學會條件檢測後，就可以開始編寫 if 陳述句了。
if 陳述句有很多種，要用哪一種取決於條件檢測的數量。

#### 簡單的 if 陳述句

<!-- more -->

最簡單的 if 陳述句是只有一備條件檢測和一個處理動作：
```text
if conditional_test:
    do something
```
條件檢測為 True 時，則`Python`就會執行緊接在後的內縮程式，
若條件檢測結果為 False 時，`Python`會忽略後面的內縮程式。
舉一個簡單的列子，判斷此人是否有投票權：
```python
age = 21
if age >= 20:
    print("You are old enough to vote!")
```
`Python`會檢測變數存放的值是否大於等於20，因為age設為21，所以結果為True，就會執行內縮的print陳述句：
```text
You are old enough to vote!
```
在 if 陳述句後的程式區塊中，可依需求寫入任意行的程式碼：
```python
age = 21
if age >= 20:
    print("You are old enough to vote!")
    print("Have you registered to vote yet?")
```
當條件檢測通過了，這兩條內縮的print陳述句就會執行：
```text
You are old enough to vote!
Have you registered to vote yet?
```
如果 age 的值小於18的話，這支程式就不會有任何輸出。

#### if-else 陳述句
在條件檢測通過時執行某一動作，而不通過時執行另一種動作，這種情況下可使用`Python`提供的 `if-else` 陳述句達成：
```python
age = 19
if age >= 20:
    print("You are old enough to vote!")
    print("Have you registered to vote yet?")
else:
    print("Sorry, you are too young to vote.")
    print("Please register to vote as soon as you turn 20!")
```
若條件檢測通過，就會執行第一個內縮的 print 區塊，檢測條件沒過，就執行 else 第二個區塊的程式：
```text
Sorry, you are too young to vote.
Please register to vote as soon as you turn 20!
```

#### if-elif-else 路徑
在編寫設計程式時常會需要檢測超過兩種以上的條件狀況，此時`Python`提供的 `if-elif-else` 語法就能派上用場。
`Python` 只會執行 if-elif-else 路徑中的其中一個程式區塊，它會依序檢測每個條件，直到碰到符合條件的檢測。
在檢測通過後，`Python`才會執行在後面的縮排程式區塊，並跳過其它剩下的檢測：
```python
age = 12

if age < 4:
    print("Your admission cost is $0.")
elif age < 18:
    print("Your admission cost is $5.")
else:
    print("Your admission cost is $10.")
```
在這裡 age 小於18，因此`Python`只會執行elif的程式區塊，並輸出文字訊息後就結束程式：
```text
Your admission cost is $5.
```
不要在 if-elif-else 區塊中輸出文字訊息，而是改成設定對應的值到變數內，在 if-elif-else 都檢測執行完成後，
再以設定的變數來輸出訊息，這樣整個程式碼就會變得更簡潔：
```python
age = 12

if age < 4:
    price = 0
elif age < 18:
    price = 5
else:
    price = 10

print("Your admission cost is $" + str(price) + ".")
```
這樣的寫法除了效率高，在修改時也相對容易。

#### 使用多個 elif 程式區塊
在設計程式時可依照需要使用多個 `elif`程式區塊：
```python
age = 12

if age < 4:
    price = 0
elif age < 18:
    price = 5
elif age < 65:
    price = 10
else:
    price = 5

print("Your admission cost is $" + str(price) + ".")
```

#### 省略 else 程式區塊
`Python`對於在 `if-elif` 路徑結構後並不一定要放 `else` 程式區塊，
在某些情況下， `else` 程式區塊還是有其用途，但在某些情況下可直接用一條 elif 陳述句來處理，
會讓程式的邏輯更清楚：
```python
age = 12

if age < 4:
    price = 0
elif age < 18:
    price = 5
elif age < 65:
    price = 10
elif age >=65:
    price = 5

print("Your admission cost is $" + str(price) + ".")
```
經過這樣的修改後，每個區塊都只有在條件檢測通過後才會進去執行。

`else`是個較廣泛的陳述，只要不滿足指定的 `if` 或 `elif` 條件檢測，
`else` 中的程式就會執行，這樣有可能會引入不合法或惡意的資料。
如果知道最後要檢測的條件，應考慮再使用 `elif` 程式區塊來代替 else，
這樣才能確保只有在滿足該條件下，對應的程式碼才會執行。

#### 檢測多個條件
`if-elif-else` 語法功能很強大，但只適用在僅有一種條件滿足時才執行的狀況，
然而有時候會希望檢測所有條件，在這樣的情況下就要使用一系列不含 `elif` 和 `else` 區塊的單純 `if` 陳述語法：
```python
requested_toppings = ['mushrooms', 'extra cheese']

if 'mushrooms' in requested_toppings:
    print('Adding mushrooms.')
if 'pepperoni' in requested_toppings:
    print('Adding pepperoni.')
if 'extra cheese' in requested_toppings:
    print('Adding extra cheese.')

print("\nFinished making your pizza!")
```
在上面的程式中所有檢測都會執行，因為 requested_toppings 串列中存放了 `'mushrooms'` 和 `'extra cheese'`，
所以會輸出披薩加了對應的配料：
```text
Adding mushrooms.
Adding extra cheese.

Finished making your pizza!
```
如果使用 `if-elif-else` 區塊，程式不會正確執行，因為在第一個條件檢測通過後就會跳過剩下的檢測。

總而言之，只想要執行一個程式區塊，就使用 `if-elif-else` 路徑結構，
如果想要執行多個程式區塊，就使用一系列單獨的 `if` 陳述句。

---

### 使用 if 陳述句來處理串列
如果把 `if` 陳述句和串列合起來使用，就能進行一些有趣的處理，另外能有效率地處理不斷更新變化的情況，
也能證明程式在所有可能的情況下都會依照您所期望的條件執行。

#### 檢測特定項目
繼續前面使用過的披薩店為例。先建立一個串列，其中存放顧客所點的配料，再使用迴圈以很高的效率來逐一把加到披薩的配料輸出：
```python
requested_toppings = ['mushrooms', 'green peppers', 'extra cheese']

for requested_topping in requested_toppings:
    print("Adding " + requested_topping + ".")

print("\nFinished making your pizza!")
```
for 迴圈之後的輸出很直接：
```text
dding mushrooms.
Adding green peppers.
Adding extra cheese.

Finished making your pizza!
```
假如其中一項材料用完了要怎麼處理呢？可以在 for 迴圈內加入一條 if陳述句來處理：
```python
requested_toppings = ['mushrooms', 'green peppers', 'extra cheese']

for requested_topping in requested_toppings:
    if requested_topping == 'green peppers':
        print("Sorry, we are out of green peppers right now.")
    else:
        print("Adding " + requested_topping + ".")

print("\nFinished making your pizza!")
```
這次在加上配料之前都先檢測，並輸出顯示已把顧客所點的配料作了適當的處置：
```text
Adding mushrooms.
Sorry, we are out of green peppers right now.
Adding extra cheese.

Finished making your pizza!
```

#### 檢測串列不是空的
到目前為止都對每個檢測做了假設串列中至少都含有一個項目。
隨後要讓使用者輸入資訊來存放到串列內，因此在執行 for 迴圈前先檢測串列是不是空的就十分重要：
```python
requested_toppings = []

if requested_toppings:
    for requested_topping in requested_toppings:
        print("Adding " + requested_topping + ".")
    print("\nFinished making your pizza!")
else:
    print("Are you sure you want a plain pizza?")
```
先建立一個空串列，接著進行快速檢測，如果串列內至少有一個項目，那 `Python` 會返回 True，如果是空的就返回 False，
如果 `Python` 返回 False，則會跳到else執行：
```text
Are you sure you want a plain pizza?
```

#### 使用多個串列
顧客的要求很多，假如顧客要在披薩中加上炸薯條當配料時該如何處理呢？
可以使用串列和 if陳述句來確定要點的配料有正常提供：
```python
available_toppings = ['mushrooms', 'olives', 'green peppers', 
                      'pepperoni', 'pineapple', 'extra cheese']
requested_toppings = ['mushrooms', 'french fries', 'extra cheese']

for requested_topping in requested_toppings:
    if requested_topping in available_toppings:
        print("Adding " + requested_topping + ".")
    else:
        print("Sorry, we don't have " + requested_topping + ".")

print("\nFinished making your pizza!")
```
先建立兩個串列分別提供正常的配料與顧客點的配料，其中顧客點的配料中有個不尋常項目 'french fries'。
接著用迴圈遍訪顧客所點配料串列的每個項目，再對每個項目檢測看它是否有在披薩店提供的正常配料串列中，
如果有則將它加到披薩中，若沒有則跳到else程式區塊執行：
```text
Adding mushrooms.
Sorry, we don't have french fries.
Adding extra cheese.

Finished making your pizza!
```
