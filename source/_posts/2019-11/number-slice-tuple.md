---
title: 串列的操作與運用 Part II.
categories: Python
tags: 'python, number, slice, tuple'
date: 2019-11-29 11:00:53
---

### 建立數字串列
串列很適合用來存放數值集合，而`Python`也提供了許多工具可協助我們有效地處理數字串列。

#### 使用 range()函式
`Python` 的 range()函式能很輕鬆地產生一系列的數字：

<!-- more -->

```python
for value in range(1,5):
    print(value)
```
雖然這段程式看起來像要輸出1到5的數字，但實際上5是不會輸出的：
```text
1
2
3
4
```
range()只輸出1到4的數字，這是我們常在程式語言中所看到的差 1（ off-by-one ）因素所造成的結果。
range()函式會讓`Python`從指定的第一個值開始算起，到指定的第二個值就停止，因此輸出並不含第二個值。
想要出1到5這幾個數字，要使用 range(1,6)
```python
for value in range(1,6):
    print(value)
```
在使用range()函式時，若輸出結果不符合預期，請試著對指定的值加1或減1。

#### 使用 range()製作數字串列
如果要製作數字串列，可使用 list()函式把 range()的結果直接轉成串列。
將 range()當成參數包在 list()中來呼叫執行，輸出的結果就會是個數字串列：
```python
numbers = list(range(1,6))
print(numbers)
```
結果如下：
```text
[1, 2, 3, 4, 5]
```
使用 range()時可以指定讓`Python`遞增的數值：
```python
even_numbers = list(range(2,11,2))
print(even_numbers)
```
range()函式是從2開始起算，以2來，直到或超過第二個數值11才停止：
```text
[2, 4, 6, 8, 10]
```
使用 range()函式幾乎可以製作任何數字集，
製作存放一個1到10的平方值的串列，在`Python`中用兩個星號（ ** ）來表示乘方的運算：
```python
squares = []
for value in range(1,11):
    square = value ** 2
    squares.append(square)

print(squares)
``` 
首先建立空串列，接著使用 range()函式讓`Python` 以迴圈遍訪1到10的整數值，
將在迴圈內的運算結果存入 square變數內，並使用 append()方法把每個平方值新增到 squares串列尾端，
最後在迴圈結束後輸出 squares串列：
```text
[1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
```
也可以用更簡潔的方式得到相同的運算結果：
```python
squares = []
for value in range(1,11):
    squares.append(value ** 2)

print(squares)
```

#### 數字串列的簡單統計運算
`Python`中有幾個函式可專門用來高數字串列的運算：
```text
>>> digits = [1, 2, 3, 4, 5, 6, 7, 8, 9, 0]
>>> min(digits)
0
>>> max(digits)
9
>>> sum(digits)
45
```

#### 串列推導解析
前面描述的製作 squares 串列的方式用了三到四行程式碼，
而串列推導解析（ list comprehension ）則讓我們只用一行程式製作相同的串列。
串列推導解析把 for 迴圈和建立新元素的程式碼合併成一行，並自動地新增每個新的元素：
```python
squares = [ value ** 2 for value in range(1,11)]
print(squares)
```
請留意這裡的 for 陳述句尾端並沒有冒號哦！

---

### 處理串列中某部份的內容
我們還可只處理串列中某部份的內容，在`Python` 中稱之為「切片（ slice ）」
 
#### 切片
切片需要指定使用的第一個元素和最後一個元素的索引足標。
與 range()函式相同，`Python` 在算到指定的第二個索引足標前的元素就會停止，
所以處理範圍不含第二個索引足標的元素：
```python
players = ['charles', 'martina', 'michael', 'florence', 'eli']
print(players[0:3])
```
此切片有三名隊員，輸出的結果也是個串列：
```text
['charles', 'martina', 'michael']
```
若想擷取串列中第2到第4個元素，就把切片的起始索引足標設為1，結尾索引足標設為4：
```python
players = ['charles', 'martina', 'michael', 'florence', 'eli']
print(players[1:4])
```
結果如下：
```text
['martina', 'michael', 'florence']
```
如果沒有指定第一個索引足標，`Python` 會自動以串列的開頭為切片的起始：
```python
players = ['charles', 'martina', 'michael', 'florence', 'eli']
print(players[:4])
```
結果如下：
```text
['charles', 'martina', 'michael', 'florence']
```
也有類似的作法讓切片可擷取到串列結尾：
```python
players = ['charles', 'martina', 'michael', 'florence', 'eli']
print(players[2:])
```
`Python` 會返回串列從第三個到結尾的所有項目元素：
```text
['michael', 'florence', 'eli']
```
此外也可以使用負數來當索引足標，負數是從尾端往回推的距離，因此可取出串列任意尾段的切片：
```python
players = ['charles', 'martina', 'michael', 'florence', 'eli']
print(players[-3:])
```
這段程式會輸出串列到數後三名的元素項目，就算串列長度有變化也不影響。

#### 迴圈遍訪切片
若想以迴圈遍訪串列某部份的項目元素，可在 for 迴圈中使用切片來達成：
```python
players = ['charles', 'martina', 'michael', 'florence', 'eli']

print("Here are the first three players on my team:")
for player in players[:3]:
    print(player.title())
```
for 迴圈並沒有遍訪整個 players 串列，`Python` 只遍訪串列的前三項：
```text
Here are the first three players on my team:
Charles
Martina
Michael
```

#### 複製串列
在編寫程式時，很常需要以現在的串列為基礎來建立全新的串列。
若想要複製串列，可以先建立一個含有原本整個串列的切片，其做法就是都不放起始和結尾索引足標，
只留一個冒號在中括號內（ [:] ），這樣就能複製整個串列了：
```python
my_foods = ['pizza,', 'falafel', 'carrot cake']
friend_foods = my_foods[:]

print("My favorite foods are:")
print(my_foods)

print("\nMy friend's favorite foods are:")
print(friend_foods)
```
不指定索引足標的方法從 my_foods 串列擷取整個串列當切片，等於複製了這個串列並指定到 friend_foods 變數內：
```text
My favorite foods are:
['pizza', 'falafel', 'carrot cake']

My friend's favorite foods are:
['pizza', 'falafel', 'carrot cake']
```
可以分別新增不同食物到各自的串列內，確定這兩個串列都存放了自己和朋友最喜歡的食物：
```python
my_foods = ['pizza,', 'falafel', 'carrot cake']
friend_foods = my_foods[:]

my_foods.append('cannoli')
friend_foods.append('ice cream')

print("My favorite foods are:")
print(my_foods)

print("\nMy friend's favorite foods are:")
print(friend_foods)
```
將 my_foods 與 複製出來的 friend_foods 兩個串列分別新增新的項目進去，最後輸出兩個串列：
```text
My favorite foods are:
['pizza', 'falafel', 'carrot cake', 'cannoli']

My friend's favorite foods are:
['pizza', 'falafel', 'carrot cake', 'ice cream']
```
假如只是單純地把 my_foods 指定給 friend_foods （ friend_foods = my_foods ），
這樣並不會真的建立兩個串列：
```python
my_foods = ['pizza,', 'falafel', 'carrot cake']

# This doesn't work:
friend_foods = my_foods

my_foods.append('cannoli')
friend_foods.append('ice cream')

print("My favorite foods are:")
print(my_foods)

print("\nMy friend's favorite foods are:")
print(friend_foods)
```
這樣並不是把 my_foods 的複製品指定存入 friend_foods。
這種指定語法在 `Python` 中是讓新的 friend_foods 變數連接到 my_foods 已存放的串列上，
兩個變數都指向同一個串列:
```text
My favorite foods are:
['pizza', 'falafel', 'carrot cake', 'cannoli', 'ice cream']

My friend's favorite foods are:
['pizza', 'falafel', 'carrot cake', 'cannoli', 'ice cream']
```
這樣的輸出結果並不是我們所要的。

---

### 多元組
有時候相要建立一個不能被修改的資料集合，這時「多元組（ tuples，或元組 ）」能滿足這項要求。
`Python` 把不能修改的值稱為不可變的（ immutable ），而這個不可變的串列就稱為多元組。

#### 定義多元組
多元組看起來很像串列，但用的是小括號（ () ）而不是中括號（ [] ）來定義標示。
在定義完多元組之後就可以用項目的索引足標來提取其中的元素，作法和串列相同：
```python
dimensions = (200, 50)
print(dimensions[0])
print(dimensions[1])
```
使用小括號定義多元組後，再將每個項目分別輸出，使用的語法和存取串列中的元素是一樣的：
```text
200
50
```
試著修改多元組中的任一元素會有什麼結果：
```python
dimensions = (200, 50)
dimensions[0] = 250
```
試著修改多元組中的第一個項目的值，結果如下：
```text
Traceback (most recent call last):
  File "test.py", line 2, in <module>
    dimensions[0] = 250
TypeError: 'tuple' object does not support item assignment
```
因為修改多元組是不允許的，所以`Python`會告知不能對多元組中的項目指定新值。

#### 遍訪多元組中所有的值
就像在處理串列一樣，可以使用 for 迴圈遍訪多元組中所有的值：
```python
dimensions = (200, 50)
for dimension in dimensions:
    print(dimension)
```
結果與串列一樣，`Python`會返回多元組中所有的元素
```text
200
50
```

#### 重寫多元組
雖然不能修改多元組，但卻可以把新的值指定給存放多元組的變數內：
```python
dimensions = (200, 50)
print("Original dimensions:")
for dimension in dimensions:
    print(dimension)

dimensions = (400, 100)
print("\nModified dimensions:")
for dimension in dimensions:
    print(dimension)
```
執行後`Python` 沒有回報錯誤訊息，因為重寫多元組並指定到變數是合法的：
```text
Original dimensions:
200
50

Modified dimensions:
400
100
```
與串列相比，多元組算是簡單的資料結構。
如果在程式的整個生命週期中想要存放一組都不會改變的值，就很適合用多元組來定義。
