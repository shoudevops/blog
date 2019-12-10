---
title: 字典 Part III.
categories: Python
tags:
- python
- dictionary
- nesting
date: 2019-12-06 10:22:39
---

### 巢狀嵌套
有時候可能需要把一組字典存放在串列中，有時又需要把串列的項目當成值存在字典內，這些都叫作「巢狀嵌套（ nesting ）」。
可以把一組字典巢狀嵌套入串列內，也可以把一系列的串列項目巢狀嵌套入字典中，或是在字典中存入字典。

#### 字典串列

<!-- more -->

建立一個外星異形串列，其中每個項目都是一個外星異形的字典，該字典中又存放外星異形的各種資訊：
```python
alien_0 = {'color': 'green', 'points': 5}
alien_1 = {'color': 'yellow', 'points': 10}
alien_2 = {'color': 'red', 'points': 15}

aliens = [alien_0, alien_1, alien_2]

for alien in aliens:
    print(alien)
```
先建立三個字典，每個字典代表一個外星異形，再將這三個外星異形字典存放入 aliens 串列中，最後再以迴圈遍訪這個串列：
```text
{'color': 'green', 'points': 5}
{'color': 'yellow', 'points': 10}
{'color': 'red', 'points': 15}
```
以現實情況來看，外星異形不止三個，有可能是使用程式動生成的，下面使用 range()生成30個外星異形：
```python
# Make an empty list for aliens.
aliens = []

for alien_number in range(30):
    new_alien = {'color': 'green', 'points': 5, 'speed': 'slow'}
    aliens.append(new_alien)

# Show the first 5 aliens.
for alien in aliens[:5]:
    print(alien)
print("...")

# Show how many aliens have been created.
print("Total number of aliens: " + str(len(aliens)))
```
先建立一個空串列 aliens，用來存放自動生成的外星異形。
用range() 返回一系列的數字告訴 `Python` 要迭代重複迴圈幾次。
每次執行這個迴圈時都會生成一個外星異形字典，並將它新增到 aliens 串列的尾端。
使用切片切出串列前5個外星異形，並將其輸出顯示。
最後輸出串列的總長度，證實生成了30個外星異形字典：
```text
{'color': 'green', 'points': 5, 'speed': 'slow'}
{'color': 'green', 'points': 5, 'speed': 'slow'}
{'color': 'green', 'points': 5, 'speed': 'slow'}
{'color': 'green', 'points': 5, 'speed': 'slow'}
{'color': 'green', 'points': 5, 'speed': 'slow'}
...
Total number of aliens: 30
```
在遊戲程式的進行中，我們會希望外星異形會以不同顏色和不同移動速度程現在畫面上，
當需要變更顏色時，我們會用 for 迴圈和 if 陳述句來修改某些外星異形字典中的 'color'：
```python
# Make an empty list for aliens.
aliens = []

for alien_number in range(0, 30):
    new_alien = {'color': 'green', 'points': 5, 'speed': 'slow'}
    aliens.append(new_alien)

for alien in aliens[0:3]:
    if alien['color'] == 'green':
        alien['color'] = 'yellow'
        alien['points'] = 10
        alien['speed'] = 'medium'

# Show the first 5 aliens.
for alien in aliens[:5]:
    print(alien)
print("...")
```
修改前三個外星異形，可用串列的切片來配合迴圈遍訪。
if 陳述句確保只改顏色是 'green' 的外星異形，將 'color' 是 'green'的外星異形修改成其它樣式的外星異形：
```text
{'color': 'yellow', 'points': 10, 'speed': 'medium'}
{'color': 'yellow', 'points': 10, 'speed': 'medium'}
{'color': 'yellow', 'points': 10, 'speed': 'medium'}
{'color': 'green', 'points': 5, 'speed': 'slow'}
{'color': 'green', 'points': 5, 'speed': 'slow'}
...
```
還可以再擴充這個迴圈，在其中加入 elif 程式區塊，把 'yellow' 黃色的外星異形改為 'red' 紅色、
'speed' 速度是 'fast'、而得分 'points' 是15。
```text
for alien in aliens[0:3]:
    if alien['color'] == 'green':
        alien['color'] = 'yellow'
        alien['points'] = 10
        alien['speed'] = 'medium'
    elif alien['color'] == 'yellow':
        alien['color'] = 'red'
        alien['points'] = 15
        alien['speed'] = 'fast'
```
在串列中存放大量的字典，而每個字典又含有特定物件的多項資訊，這種情況在編寫程式的歷程中很常遇到。

#### 字典中的串列
除了在把字典存放在串列內，有時候也會有需要用到把串列存放到字典內的情況。
以描述顧客點的披薩來說，如果使用串列，就只能存放加點披薩的配料，
但如果使用字典來儲存，就不僅能存放配料的資訊，還可存放其它關於披薩的描述。
```python
# Store information about a pizza being ordered.
pizza = {
    'crust': 'thick',
    'toppings': ['mushrooms', 'extra cheese'],
    }

# Summarize the order.
print("You ordered a " + pizza['crust'] + "-crust pizza " + "with the following toppings:")

for topping in pizza['toppings']:
    print("\t" + topping)
```
建立一個字典存放關於顧客所點披薩的資訊，其中第二個鍵是 'toppings'，關聯的值是個字串存放顧客所點的配料。
披薩製作前輸出了客人要點的披薩描述，然後用 for 迴圈把所點的配料輸出。
若想存取配料串列，這裡用了 'toppings' 當成「鍵」，讓 `Python` 從字典中擷取配料串列：
```text
You ordered a thick-crust pizza with the following toppings:
	mushrooms
	extra cheese
```
當您想要在字典中以一個鍵關聯到多個值時，可以在字典中巢狀嵌套串列進去。
以先前提到的最愛程式語言的範例，如果把每個人的喜好存放在在一個串列內，就可以選擇多種喜歡的程式語言。
字典以這種情況存放串列，當迴圈遍訪字典時，關聯每個人員的都是一個程式語言的串列，而不是單個程式語言項：
```python
favorite_languages = {
    'jen': ['python', 'ruby'],
    'sarah': ['c'],
    'edward': ['ruby', 'go'],
    'phil': ['python', 'haskell'],
    }

for name, languages in favorite_languages.items():
    print("\n" + name.title() + "'s favorite languages are:")
    for language in languages:
        print("\t" + language.title())
```
以迴圈遍訪字典時，使用了 languages 變數來存放從字典中取出的每個值，因為我們知道這些值是串列。
在字典主迴圈的遍訪內，又加了一個 for 迴圈來遍訪每個人喜歡的程式語言，現在要列出多少種喜歡的程式語言都可以：
```text
Jen's favorite languages are:
	Python
	Ruby

Sarah's favorite languages are:
	C

Edward's favorite languages are:
	Ruby
	Go

Phil's favorite languages are:
	Python
	Haskell
```

#### 字典中的字典
可以在字典中再巢狀嵌套另一個字典，但這樣程式碼很快就變得更複雜了：
```python
users = {
    'aeinstein': {
        'first': 'albert',
        'last': 'einstein',
        'location': 'princeton',
        },

    'mcurie': {
        'first': 'marie',
        'last': 'curie',
        'location': 'paris',
        },

    }

for username, user_info in users.items():
    print("\nUsername: " + username)
    full_name = user_info['first'] + " " + user_info['last']
    location = user_info['location']

    print("\tFull name: " + full_name.title())
    print("\tLocation: " + location.title())
```
定義一個 users 字典，其中有兩個鍵：使用者帳號'aeinstein'和'mcurie'，而與這兩個鍵關聯的值都是個字典。
用迴圈遍訪 users 字典，讓`Python`將每個鍵存到 username 變數中，並依序將與鍵關聯的字典存放到 user_info 變數內。
先輸出顯示使用者帳號，再來存取字典內部資訊，並存放到各自的變數名稱後輸出顯示：
```text
Username: aeinstein
	Full name: Albert Einstein
	Location: Princeton

Username: mcurie
	Full name: Marie Curie
	Location: Paris
```
每位使用者帳號所關聯的字典內部結構是相同的，雖然 `Python` 沒有要求一定要相同，
但為了在處理巢狀嵌套字典時較簡單容易，這樣作才是正確的。
假日每位使用者帳號所關聯的字典內部都用不同的「鍵」，那麼 for 迴圈內部要存取每位使用者的資訊時就會變得十分複雜。
