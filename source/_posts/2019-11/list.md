---
title: 串列簡介
categories: Python
tags: 'python, list'
date: 2019-11-25 15:21:42
---
### 什麼是串列？
串列(List)是個依特定順序排放的項目集合所組成。
任何東西都可以放入串列中，項目之間也不需要有什麼關聯。

在`Python`中是用中括號（[）標示串列，其中個別元素是以逗號（,）分隔。

<!-- more -->

```python
bicycles = ['trek', 'cannondale', 'redline', 'specialized']
print(bicycles)
```
若要求`Python`印出列表，`Python`會返回列表的表示形態，包括中括號：
```python
['trek', 'cannondale', 'redline', 'specialized']
```
但這不是要讓使用者看到的輸出形態，所以要學習如何存取串列中想要的個別項目。

---

### 存取串列中的元素
串列是有順序性的集合，因此要存取串列中的某個元素，就要告知`Python`元素的所在位置或索引足標（index）。
若想存取串列中的元素，寫出串列的名稱並在中括號中指出元素的索引足標：
```python
bicycles = ['trek', 'cannondale', 'redline', 'specialized']
print(bicycles[0])
```
上面的範例，`Python`返回的只有該元素的值，不會有引號和中括號，這才是我們要給使用者看到的結果：
```python
trek
```
還可以對任何元素使用字串方法：
```python
bicycles = ['trek', 'cannondale', 'redline', 'specialized']
print(bicycles[0].title())
```

---

### 索引足標是從0開始，不是1
`Python`中串列第一個元素的項目位置之索引足標是0，第二個項目元素的索引足標為2，
因此只要將其第幾個位置減1當成索引足標就可以了：
```python
bicycles = ['trek', 'cannondale', 'redline', 'specialized']
print(bicycles[1])
print(bicycles[3])
```
會返回第2和第3個項目元素：
```python
cannondale
specialized
```
`Python`有個特別的語法可存取串列的最後一個項目：
```python
bicycles = ['trek', 'cannondale', 'redline', 'specialized']
print(bicycles[-1])
```
此段程式會返回輸出 specialized，也適用其它負數上，例如 -2是串列的倒數第2個項目，
-3為倒數第3個項目，以此類推。

---

### 使用串列中的個別值
也可以像使用其它變數一樣的使用串列中的個別值：
```python
bicycles = ['trek', 'cannondale', 'redline', 'specialized']
message = "My first bicycle was a " + bicycles[0].title() + "."
print(message)
```
使用了 bicycle[0] 連接成一個句子，並把句子存到 message 變數內：
```text
My first bicycle was a Trek.
```

---

### 修改、新增和刪除串列中的元素
我們所建立的大多數串列都是動態的，在串列建立後都會隨著程式的運作執行而修改增刪其中的元素。

#### 修改串列中的元素
修改串列元素所用的語法和存取串列元素的語法類似，可以先指定串列名稱和要修改項目元素的索引足標位置，
再指定新的值進去即可：
```python
motorcycles = ['honda', 'yamaha', 'suzuki']
print(motorcycles)

motorcycles[0] = 'ducati'
print(motorcycles)
```
首先定義一個motorcycles串列，再將第一個項目元素的值指定為'ducati'，輸出結果：
```text
['honda', 'yamaha', 'suzuki']
['ducati', 'yamaha', 'suzuki']
```
修改其它項目元素的值也使用相同方法。

#### 新增元素到串列中
新增元素到串列中的理由有很多種，`Python`也提供了很多種可以在現有串列中加入新資料的方法。

##### 在串列尾端新增元素
想要在字串尾端新增元素，最簡單的方式是把項目元素以「附加（append）」的方式加到串列尾端：
```python
motorcycles = ['honda', 'yamaha', 'suzuki']
print(motorcycles)

motorcycles.append('ducati')
print(motorcycles)
```
append()方使會把'ducati'新增到串列尾端，不影響原有串列中的其它內容：
```text
['honda', 'yamaha', 'suzuki']
['honda', 'yamaha', 'suzuki', 'ducati']
```
append()方法使得動態建立串列變簡單了，可先建一空的串列，再列用append()陳述句新增項目：
```python
motorcycles = []

motorcycles.append('honda')
motorcycles.append('yamaha')
motorcycles.append('suzuki')

print(motorcycles)
```
執行結果與前面的串列完全相同：
```text
['honda', 'yamaha', 'suzuki']
```
這種方式很普遍，因為有時要等到執行程式後才知道程式中要儲存的資料有哪些。
為了配合使用者，可先建立一個空串列，然後把使用者所輸入的每個值附加到空串列內。

##### 在串列中插入元素
使用 insert()方法就可以在串列的位一位置加入新元素，指定新插入元素的索引足標位置和值即可：
```python
motorcycles = ['honda', 'yamaha', 'suzuki']

motorcycles.insert(0, 'ducati')
print(motorcycles)
```
範例的操作會讓原本串列中的項目值都向右移一位：
```text
['ducati', 'honda', 'yamaha', 'suzuki']
```

#### 從串列中刪除元素
我們常需要從串列中刪除一個或一組元素，`Python`也提供了幾個方法讓我們可以依據在串列中的位置或值來刪除項目。

##### 使用 del 陳述句刪除元素
如果知道要刪除的元素在串列中的哪個位置，就可用del陳述句刪除：
```python
motorcycles = ['honda', 'yamaha', 'suzuki']
print(motorcycles)

del motorcycles[0]
print(motorcycles)
```
用del刪除串列的第一個元素：
```text
['honda', 'yamaha', 'suzuki']
['yamaha', 'suzuki']
```
如果知道索引足標位置，使用 del 陳述句即可刪除串列中該索引足標位置的內容：
```python
motorcycles = ['honda', 'yamaha', 'suzuki']
print(motorcycles)

del motorcycles[1]
print(motorcycles)
```
刪除串列中第二個項目：
```text
['honda', 'yamaha', 'suzuki']
['honda', 'suzuki']
```
串列中的值使用del 陳述句刪除之後就不能存取了。

##### 使用 pop()方法刪除
在刪除串列中的某個項目值後，卻會需要使用這個值來進行其它處理。
pop()方法可刪除串列尾端的項目，並讓我們能使用這個被刪除的項目。
pop（彈出）這個術語源自於堆疊，把串列相像成堆疊，而堆疊的pop是把最頂端的項目彈出，
而在這個比喻中堆疊的頂端對應串列中的尾端。
```python
motorcycles = ['honda', 'yamaha', 'suzuki']
print(motorcycles)

popped_motorcycle = motorcycles.pop()
print(motorcycles)
print(popped_motorcycle)
```
定義motorcycles串列，接著從這個串列中彈出一個值，並指定存到 popped_motorcycle變數內，
隨即輸出 motorcycles串列，確定是否已刪除一個值，最後將單出的值輸出，證明還能繼續存取已刪除的值。
```text
['honda', 'yamaha', 'suzuki']
['honda', 'yamaha']
suzuki
```
實際應用：
```python
motorcycles = ['honda', 'yamaha', 'suzuki']

last_owned = motorcycles.pop()
print("The last motorcycle I owned was a " + last_owned.title() + ".")
```
即輸出一句簡單的句子，指出最近所擁有的機車是哪個廠牌：
```text
The last motorcycle I owned was a Suzuki.
```

##### 彈出串列中位一位置的項目
藉由在 pop()方法的括號中指定要刪除項目的索引足標位置，就能刪除串列中任一位值的項目。
```python
motorcycles = ['honda', 'yamaha', 'suzuki']

first_owned = motorcycles.pop(0)
print("The first motorcycle I owned was a " + first_owned.title() + ".")
```
從串列中彈出第一個項目的機車廠牌，再輸出簡單的句子：
```text
The first motorcycle I owned was a Honda.
```
請記住，每次使用 pop()之後，串列中被彈出的項目就會刪除掉了。

如果不確定要用del陳述句或是pop()方法，可以用以下方法判斷：
**刪除串列中某項目且不再使用時，用del陳述句。**
**刪除某項目後還會用到該項目時，就用pop()方法。**

##### 依據值來刪除項目
有時並不知道要刪除的值在串列的哪個位置，如果只知道要刪除項目的值，可使用remove()方法來處理。
```python
motorcycles = ['honda', 'yamaha', 'suzuki', 'ducati']
print(motorcycles)

motorcycles.remove('ducati')
print(motorcycles)
```
告知`Python` 要從串列中找出'ducati'的所在，並移除掉這個元素：
```text
['honda', 'yamaha', 'suzuki', 'ducati']
['honda', 'yamaha', 'suzuki']
```
也可以指定串列中要移除的值使用remove()方法來移除：
```python
motorcycles = ['honda', 'yamaha', 'suzuki', 'ducati']
print(motorcycles)

too_expensive = 'ducati'
motorcycles.remove(too_expensive)
print(motorcycles)
print("\nA " + too_expensive.title() + " is too expensive for me.")
```
把'ducati'值指定存放到 too_expensive 變數內，接著用這個變數來告知`Python`要從串列中刪除這個值。

---

### 組織串列
`Python` 提供幾個可以組織和調整串列的方式，可依不同情況來使用。

#### 使用 sort()方法對串列永久性改變排列順序
`Python` 的 sort()方法可對串列進行排序：
```python
cars = ['bmw', 'audi', 'toyota', 'subaru']
cars.sort()
print(cars)
```
執行後 cars串列會依字母順序排列，且不能回覆到原來的排列順序：
```text
['audi', 'bmw', 'subaru', 'toyota']
```
只要在 sort()方法中傳入`reverse=True`參數，也能依字母相反順序來排列串列中的項目：
```python
cars = ['bmw', 'audi', 'toyota', 'subaru']
cars.sort(reverse=True)
print(cars)
```
串列的項目已永久性變更了順序：
```text
['toyota', 'subaru', 'bmw', 'audi']
```

#### 使用 sorted()函式對串列暫時性改變排列順序
若要保留原本的排列順序，但在顯現時是以特定的排序呈現，可用 sorted()函式。
此函式能依照特定排序來顯示串列的項目內容，但不影響串列中原本來排列順序。
```python
cars = ['bmw', 'audi', 'toyota', 'subaru']

print("Here is the original list:")
print(cars)

print("\nHere is the sorted list:")
print(sorted(cars))

print("\nHere is the original list again:")
print(cars)
```
改變順序顯示後，串列的項目還是以原本順序排列：
```text
Here is the original list:
['bmw', 'audi', 'toyota', 'subaru']

Here is the sorted list:
['audi', 'bmw', 'subaru', 'toyota']

Here is the original list again:
['bmw', 'audi', 'toyota', 'subaru']
```
如果想要按字母反序顯示串列的項目，可在sorted()函式傳入 `reverse=True`參數。

#### 反序印出串列
若要反轉串列項目原本的順序，可使用reverse()方法：
```python
cars = ['bmw', 'audi', 'toyota', 'subaru']
print(cars)

cars.reverse()
print(cars)
```
請注意一點，reverse()並不是指按字母反序排列串列項目，只是簡單的反轉串列項目的排列順序。
```text
['bmw', 'audi', 'toyota', 'subaru']
['subaru', 'toyota', 'audi', 'bmw']
```
reverse()方法會永久性改變串列中項目的排列順序，但可以隨時再反轉回來，只要再對串列套用`reverse()`即可。

#### 找出串列的長度
藉由使用 len()函式能快速找出串列的長度：
```python
>>> cars = ['bmw', 'audi', 'toyota', 'subaru']
>>> len(cars)
4
```

---

### 使用串列時避免 IndexError
這是在剛開始使用串列時常會遇到的一種錯誤。
假設串列內含三個項目，但使用者卻要求了第四個項目：
```python
motorcycles = ['honda', 'yamaha', 'suzuki']
print(motorcycles[3])
```
執行結果會是索引錯誤：
```text
Traceback (most recent call last):
  File "syntax_error.py", line 2, in <module>
    print(motorcycles[3])
IndexError: list index out of range
```
大家常把串列第三個項目的索引足標想成是3，但`Python` 的串列第三個項目的索引足標為2，要從0開始算起才正確。

當需要存取串列最後一個項目時，可使用 `-1` 來當索引足標：
```python
motorcycles = ['honda', 'yamaha', 'suzuki']
print(motorcycles[-1])
```
只有在串列是空的時候，使用 `-1`來存取最後一個項目會產生錯誤：
```python
motorcycles = []
print(motorcycles[-1])
```
motorcycles 串列是空的，沒有任何項目在其中，因此`Python`會返回索引錯誤的訊息：
```text
Traceback (most recent call last):
  File "syntax_error.py", line 2, in <module>
    print(motorcycles[-1])
IndexError: list index out of range
```
