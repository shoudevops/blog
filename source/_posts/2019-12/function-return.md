---
title: 函式 － 返回值
categories: Python
tags:
  - python
  - function
  - return
date: 2019-12-11 09:23:35
---

### 返回值
函式也可以高一些資訊並返回一個或一組值。函式返回的值稱之為「**返回值（ return value ）**」。
在函式中可以用 return 陳述句把值返回到呼叫函式的那行程式碼中。
返回值讓我們能夠將程式的大多數繁雜工作移到函式內部去完成，如此就能簡化程式的結構。

<!-- more -->

#### 返回簡單值
來看一個函式範例，此函式能接收名和姓，並返回經過格式化的完整姓名文句：
```python
def get_formatted_name(first_name, last_name):
    """Return a full name, neatly formatted."""
    full_name = first_name + ' ' + last_name
    return full_name.title()

musician = get_formatted_name('jimi', 'hendrix')
print(musician)
```
此函式的定義中是把 first_name 和 last_name 當成參數，並把兩者連接在一起，
中間會放一個空格，再將結果存放在 full_name 變數內。
最後把 full_name 的值轉換成首字大寫再將結果返回到函式呼叫的那一行：
```text
Jimi Hendrix
```
如果需要處理分別存放大量姓和名的大型程式中，像 get_formatted_name() 這樣的函式就很有用了，
每當有需要輸出完整姓名的時候，就呼叫這個函式來協助就行了。

#### 讓引數變成可選擇性的
在使用函式時只有在必要時才提供額外的資訊，不提供時則以預設值來處理。
所以在家義函式時只要把某個參數指定預設值，那在呼叫時這個對應的引數就變可選性的，
在有需要時才提供新的資訊進去：
```python
def get_formatted_name(first_name, middle_name, last_name):
    """Return a full name, neatly formatted."""
    full_name = first_name + ' ' + middle_name + ' ' + last_name
    return full_name.title()

musician = get_formatted_name('john', 'lee', 'hooker')
print(musician)
```
上述範例擴展 get_formatted_name() 函式的功能，讓它可以處理中間名字：
```text
John Lee Hooker
```
不過並非每個人都有中間名，但甘在呼叫此函式時只提供名和姓就不能運作了。
為此我們將中間名變成可選擇性的，有才加上，沒有就略過：
```python
def get_formatted_name(first_name, last_name, middle_name=''):
    """Return a full name, neatly formatted."""
    if middle_name:
        full_name = first_name + ' ' + middle_name + ' ' + last_name
    else:
        full_name = first_name + ' ' + last_name
    return full_name.title()

musician = get_formatted_name('jimi', 'hendrix')
print(musician)

musician = get_formatted_name('john', 'hooker', 'lee')
print(musician)
```
為了讓函式在提供中間名時依然可以執行，在程式定義函式時，對 middle_name 參數指定一個預設值 － 空字串（''），
並將它從參數清單的中間移到最後：
```text
Jimi Hendrix
John Lee Hooker
```
如果只想指定名和姓，呼叫的方式就較為簡單，直接放入即可。
但當有中間名時，歐要把中間名放在最後一個引數，這樣 `Python` 才能正確地把位置引數的值對應到函式的參數中。

「值」可選擇性放進函式來呼叫，能夠讓函式在處理各種不同情形的需求時可確保函式呼叫盡可能變得較為簡單。

#### 返回字典
函式能返回各種型別的值，包括串列、字典等比較複雜的資料結構：
```python
def build_person(first_name, last_name):
    """Return a dictionary of information about a person."""
    person = {'first': first_name, 'last': last_name}
    return person

musician = build_person('jimi', 'hendrix')
print(musician)
```
函式接受 first_name 和 last_name ，並將這兩個值裝進字典內。
在儲存 first_name 值時，「鍵（key）」是用 'first'；儲存 last_name 時，「鍵（key）」是用 'last'。
最後會返回這個「 person 」字典，輸出後得到以下結果：
```text
{'first': 'jimi', 'last': 'hendrix'}
```
這個函式接收了簡單的文字資訊，再將它們存放到更有意義的資料結構內，讓我們不止能輸出，也能以其它方式處理運用這些資訊。
還可以擴充這個函式的功能，讓它可以接收可選擇性的值：
```python
def build_person(first_name, last_name, age=''):
    """Return a dictionary of information about a person."""
    person = {'first': first_name, 'last': last_name}
    if age:
        person['age'] = age
    return person

musician = build_person('jimi', 'hendrix', age=27)
print(musician)
```
這個函式的定義中新增了一個可選擇性的參數 age，並指定預設值為空字串。
如果函式在呼叫時有傳入這個參數值，這個值也會一起儲存到字典內。

#### 在 while 迴圈使用函式
可以將前面所學過的程式結構中一起運用函式，
把 while 迴圈和 get_formatted_name() 函式結合一起運用：
```python
def get_formatted_name(first_name, last_name):
    """Return a full name, neatly formatted."""
    full_name = first_name + ' ' + last_name
    return full_name.title()

# This is an infinite loop!
while True:
    print("\nPlease tell me your name:")
    f_name = input("First name: ")
    l_name = input("Last name: ")

    formatted_name = get_formatted_name(f_name, l_name)
    print("\nHello, " + formatted_name + "!")
```
while 迴圈能讓使用者輸入名和姓，執行時會提示畢者輸入 First name 和 Last name。
但以上範例沒有定義結束退出迴圈的條件，因此在每次提示使用者輸入時，都要提供結束退出的路徑。
每次提示使用者輸入時，都有條件可執行 break 陳述句來結束退出迴圈：
```python
def get_formatted_name(first_name, last_name):
    """Return a full name, neatly formatted."""
    full_name = first_name + ' ' + last_name
    return full_name.title()

# This is an infinite loop!
while True:
    print("\nPlease tell me your name:")
    print("('enter 'q' at any to to quit.)")
    f_name = input("First name: ")
    if f_name == 'q':
        break

    l_name = input("Last name: ")
    if l_name == 'q':
        break

    formatted_name = get_formatted_name(f_name, l_name)
    print("\nHello, " + formatted_name + "!")
```
只要在使用者輸入名或姓的時候，輸入 'q' 就停止結束：
```text
Please tell me your name:
('enter 'q' at any to to quit.)
First name: eric
Last name: matthes

Hello, Eric Matthes!

Please tell me your name:
('enter 'q' at any to to quit.)
First name: q
```
