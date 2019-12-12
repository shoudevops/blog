---
title: 字典 － 迴圈的應用
categories: Python
tags:
- python
- dictionary
- loop
date: 2019-12-05 17:11:46
---

### 以迴圈遍訪字典
因為字典能放入大量的資料，所以`Python`允許我們使用迴圈來遍訪字典的所有內容。
字典允許用很多種方式來儲存資料，因此迴圈遍訪的方式也有幾種不同的作法，
可以迴圈遍訪字典的所有鍵 － 值對、或只遍訪所有的鍵、或只遍訪所有的值。

<!-- more -->

#### 遍訪字典中所有的鍵 － 值對
下列字典中存放了使用者的帳戶名稱、姓和名等：
```python
user_0 = {
    'username': 'efermi',
    'first': 'enrico',
    'last': 'fermi',
    }
```
若要取得此字典中的所有資訊時，做法是使用一個 for 迴圈來遍訪這個字典：
```python
user_0 = {
    'username': 'efermi',
    'first': 'enrico',
    'last': 'fermi',
    }

for key, value in user_0.items():
    print("\nKey: " + key)
    print("Value: " + value)
```
在 for 迴圈中，可宣告兩變數來存放鍵 － 值對中的鍵和值，這兩個變數可取任何名字。
for 陳述句的第二個部份包括字典名稱和跟在後面的 item() 方法，此方法會返回鍵 － 值對串列：
```text
Key: username
Value: efermi

Key: first
Value: enrico

Key: last
Value: fermi
```
若在遍訪字典時鍵 － 值對的返回順序可能和存放順序不同，
`Python`不管鍵 － 值對在字典中的存放順序，只關心鍵和值之間的相互關聯。

在 `Part I.`介紹的範例中也可以使用迴圈遍訪，而在迴圖中可用 name 和 language 來當存放的變數，
不再用 key 和 value 這樣的名稱，能讓人更容易了解其程式迴圈的作用和目的：
```python
favorite_languages = {
    'jen': 'python',
    'sarah': 'c',
    'edward': 'ruby',
    'phil': 'python',
    }

for name, language in favorite_languages.items():
    print(name.title() + "'s favorite language is " + language.title() + ".")
```
以這幾行程式碼，就能把所有人的喜好程式語言完全輸出：
```text
Jen's favorite language is Python.
Sarah's favorite language is C.
Edward's favorite language is Ruby.
Phil's favorite language is Python.
```
就算字典中儲存了數千，數百萬個人的資料，這樣的迴圈也一樣能順利運作。

#### 遍訪字典中的所有鍵
當不需要運用字典中的「值」，只需處理「鍵」的時候，`key()`方法就很有用：
```python
favorite_languages = {
    'jen': 'python',
    'sarah': 'c',
    'edward': 'ruby',
    'phil': 'python',
    }

for name in favorite_languages.keys():
    print(name.title())
```
告訴`Python`擷取 favorite_languages 字典中所有的「鍵」並逐一存入到 name變數內：
```text
Jen
Sarah
Edward
Phil
```
迴圈遍訪字典時，預設的處理動作就是遍訪所有的「鍵」，因此for迴圈可以更換為：
```text
for name in favorite_languages:
```
如果將 key()方法明顯地寫在程式中會更易讓人理解，或著也可省略不加。

以前面的迴圈遍訪字典中的名字（鍵），但當遍訪到指定好友的名字時，就輸出一條訊息告知其最喜歡的程式語言：
```python
favorite_languages = {
    'jen': 'python',
    'sarah': 'c',
    'edward': 'ruby',
    'phil': 'python',
    }

friends = ['phil', 'sarah']
for name in favorite_languages.keys():
    print(name.title())

    if name in friends:
        print("  Hi " + name.title() +
            ", I see your favorite language is " +
            favorite_languages[name].title() + "!")
```
字典中的每個名字都會輸出，但輸出到好友時會多出一條特別的訊息：
```text
Jen
Sarah
  Hi Sarah, I see your favorite language is C!
Edward
Phil
  Hi Phil, I see your favorite language is Python!
```
也可以使用 key() 方法來確定某個特定的人名字是否有出現在字典內：
```python
favorite_languages = {
    'jen': 'python',
    'sarah': 'c',
    'edward': 'ruby',
    'phil': 'python',
    }

if 'erin' not in favorite_languages.keys():
    print("Erin, please take our poll!")
```
key() 方法並不只用在迴圈遍訪，它會返回一個串列，存放著字典中的所有「鍵」，
由於 'erin' 不在此串列內，因此輸出一條訊息來請她接受訪查：
```text
Erin, please take our poll!
```

#### 以特定順序遍訪字典的鍵
前面曾經提到，「`Python`不管鍵 － 值對在字典中的存放順序，只關心鍵和值之間的相互關聯。」
若想要以特定的順序返回字典中的項目，就要在 for 迴圈中對返回的「鍵」，
使用 `sorted()` 函式以複製的方式來取得依照特定順序排列的「鍵」串列：
```python
favorite_languages = {
    'jen': 'python',
    'sarah': 'c',
    'edward': 'ruby',
    'phil': 'python',
    }

for name in sorted(favorite_languages.keys()):
    print(name.title() + ", thank you for taking the poll.")
```
for 陳述句用 sorted() 函式對 dictionary.keys() 進行處理，讓 `Python` 在列出字典中所有「鍵」之後，
並在遍訪之前對這些「鍵」進行了排序：
```text
Edward, thank you for taking the poll.
Jen, thank you for taking the poll.
Phil, thank you for taking the poll.
Sarah, thank you for taking the poll.
```

#### 以迴圈遍訪字典中所有的值
如果感興趣的是字典中所存放的「值」，則可使用 `values()` 方法來處理，
此方法會返回字典中所有「值」的串列，而不包含「鍵」：
```python
favorite_languages = {
    'jen': 'python',
    'sarah': 'c',
    'edward': 'ruby',
    'phil': 'python',
    }

print("The following languages have been mentioned:")
for language in favorite_languages.values():
    print(language.title())
```
for 陳述句會擷取字典中所有的「值」，並將它們依序存放到 language 變數內：
```text
The following languages have been mentioned:
Python
C
Ruby
Python
```
若要刪除重複的值，可使用「集合（ set ）」來達成。
集合的概念與串列很相似，但存放其中的每個項目都必須是唯一的：
```python
favorite_languages = {
    'jen': 'python',
    'sarah': 'c',
    'edward': 'ruby',
    'phil': 'python',
    }

print("The following languages have been mentioned:")
for language in set(favorite_languages.values()):
    print(language.title())
```
使用 set()來處理從字典取回的「值」串列，就會讓 `Python` 取出唯一不重複的「值」項目，
並以這樣「值」建立成一個集合：
```text
The following languages have been mentioned:
Python
C
Ruby
```
隨著持續學習 `Python` ，通常就會發現一些好用的內建功能，這些功能大都能依需要來處理資料。
