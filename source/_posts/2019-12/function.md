---
title: 函式 Part I.
categories: Python
tags:
- python
- function
date: 2019-12-10 15:30:53
---

本章將學習編寫函式，是個取了名字的程式區塊，
當要執行定義在函式中的特定工作時，可以呼叫這個函式的名稱來執行該項工作。
若在程式中需要執行同一項工作很多次時，不需要為這項工作重複寫入多次相同的程式碼，
只要把完成該項工作的程式定義成函式，再呼叫此函式讓 `Python` 執行其中的程中即可。
活用函式之後，在程式的編寫、閱讀、測試和修改都變得更容易。

<!-- more -->

### 定義函式
下列為一個簡單函式，能輸出問候文句：
```python
def greet_user():
    """Display a simple greeting."""
    print("Hello!")

greet_user()
```
使用 `def` 關鍵字來告知 `Python` 需要定義一個函式，這就是「函式定義（ function definition ）」，
告知 `Python` 函式的名稱和函式要完成工作所需的資訊，若有需要可在括號中放入這樣資訊，最後是以冒號（ : ）當結尾。
接著在 `def` 之後的所有內縮程式行組成函式的本體。
內縮的第一行的文字稱為「**文件字串（ docstring ）**」的注釋，用來描述函式的功用。

要使用這個函式就要呼叫它。**函式呼叫（ function call ）**是告知 `Python` 去執行函式內的程式碼。
若要呼叫某個函式，可輸入函式名稱和括號，如有需要才在括號內放入必需的資訊：
```text
Hello!
```

#### 把資訊傳入函式內
對上述程式做一點修改，就可讓函式輸出更多內容，在括號內放入 username，
藉由輸入的 username 就能讓函式接收在呼叫時所傳入的任意值。
現在這個函式會要求在每次呼叫時要提供一個值給 username：
```python
def greet_user(username):
    """Display a simple greeting."""
    print("Hello, " + username.title() + "!")

greet_user('jesse')
```
以輸入 greet_user('jesse') 來呼叫函式，會對函式內的 print 陳述句提供輸出時所需的資訊內容：
```text
hello, Jesse!
```
可以依據需要隨意呼叫 `greet_user()` 函式，呼叫時無論傳入什麼字串，都會輸出對應的輸出文句。

#### 引數與參數
在 `greet_user()` 函式中，username 變數是個「**參數（ parameter ）**」，是函式要完成工作時所需的一項資訊。
在 `greet_user('jesse')` 程式碼內， 'jesse'值是個引數。引數是呼叫函式時傳入到函式的資訊。
當呼叫函式時，會把函式要用到的值放在括號內傳入，上面範例中，將 `'jesse'` 引數傳入 `greet_user()`函式，
而這個值會存放在 `username` 參數中。

---

### 傳入引數
函式定義可以有多個參數，所以呼叫函式也可能需要多個引數。
要把引數傳入函式的方函有好幾個，可以使用**位置引數（ positional arguments ）**，是個要求編寫的順序要和參數的順序相同。
也可使用**關鍵字引數（ keyword arguments ）**，其中引數是由變數名稱和值、串列或字典所組成。

#### 位置引數
當呼叫函式時， `Python` 函式呼叫的每個引數必須對應符合函式定義中的參數。
最簡單的方式是按照引數的順序來傳入，這種對應符合的值就稱為**位置引數**。

下列範例函式會顯示某隻寵物屬於哪一種動物，以及其名字：
```python
def describe_pet(animal_type, pet_name):
    """Display information about a pet."""
    print("\nI have a " + animal_type + ".")
    print("My " + animal_type + "'s name is " + pet_name.title() + ".")

describe_pet('hamster', 'harry')
```
從函式的定義可得知它需要動物類型和名字兩個引數，呼叫 `describe_pet()` 時，需要按照順序提供一個動物類型和一個名字。
'hamster' 引數對應存放在 `animal_type` 參數中，而 'harry' 對應引數則存放在 `pet_name` 參數內：
```text
I have a hamster.
My hamster's name is Harry.
```

##### 函式的多次呼叫
可依據需要多次呼叫函式來用。若還想要描述某支寵物的文句，只要再呼叫 `describe_pet()`：
```python
def describe_pet(animal_type, pet_name):
    """Display information about a pet."""
    print("\nI have a " + animal_type + ".")
    print("My " + animal_type + "'s name is " + pet_name.title() + ".")

describe_pet('hamster', 'harry')
describe_pet('dog', 'willie')
```
第二個呼叫 `describe_pet()` 函式中，傳入了 'dog' 和 'willie' 引數，與前一個呼叫時處理引數的方式一樣，
`Python` 會把 `'dog'` 引數對應到 `animal_type` 參數，將 `'willie'` 引數對應到 `pet_name` 參數內：
```text
I have a hamster.
My hamster's name is Harry.

I have a dog.
My dog's name is Willie.
```
多次呼叫函式是一種很有效率的工作方式。只在函式中編寫一次用來描述寵物的文句，
之後每次想要描述新的寵物時，都能直接呼叫函式並傳入必要的資訊，這樣就能輸出對應的文句。
就算描述寵物的函式內程式擴增 10 行，依然只需一行呼叫函式的程式碼就能描述新的寵物。

在函式中可依照需要使用任意個位置引數， `Python` 會依照順序把函式呼叫的引數對應到函式定義的參數上。
##### 在位置引數中順序很重要
使用位置引數來呼叫函式時，如果引數放置的順序不對，可能會出現跟想像中不同的結果：
```python
def describe_pet(animal_type, pet_name):
    """Display information about a pet."""
    print("\nI have a " + animal_type + ".")
    print("My " + animal_type + "'s name is " + pet_name.title() + ".")

describe_pet('harry', 'hamster')
```
這次的函式呼叫，先放置名字，再放置動物類型，順序相反，結果變成：
```text
I have a harry.
My harry's name is Hamster.
```
如果出現上面這樣的怪文句，請確定函式呼叫時引數的順序是否與函式定義時的參數順序是一致的。

#### 關鍵字引數
**關鍵字引數（ keyword argument ）**是傳入函式的**名 － 值對（ name-value pair  ）**。
直接在引數中就把名字和值關聯起來，因此在對函式傳入引數時不會產生混淆。
關鍵字引數會讓我們不需考慮在函式呼叫時放置引數的順序，還能清楚地標示出值在函式中的用述：
```python
def describe_pet(animal_type, pet_name):
    """Display information about a pet."""
    print("\nI have a " + animal_type + ".")
    print("My " + animal_type + "'s name is " + pet_name.title() + ".")

describe_pet(animal_type='hamster', pet_name='harry')
```
函式的內容沒變，但在呼叫函式時對 `Python` 明確指出各引數所對應的參數。
關鍵字引數的順序可隨便排放，因為 `Python` 知道各個值要存到哪一個參數內。
下列兩個函式呼叫是一樣的：
```text
describe_pet(animal_type='hamster', pet_name='harry')
describe_pet(pet_name='harry', animal_type='hamster')
```

#### 預設值
在編寫函式時可以給定每個參數一個預設值，在呼叫函式時若對參數指定引數，
`Python` 就會使用指定的甲數值，不然參數就其預設值進行處理。
因此，在為參數設定預設值之後，可在函式呼叫時省略其對應的引數。
用了預設值之後可簡化函式的呼叫，展示出函式呼叫的典型用法：
```python
def describe_pet(pet_name, animal_type='dog'):
    """Display information about a pet."""
    print("\nI have a " + animal_type + ".")
    print("My " + animal_type + "'s name is " + pet_name.title() + ".")

describe_pet(pet_name='willie')
```
上述只對 'animal_type' 參數指定了預設值，在呼叫函式時，如果沒有提供 `animal_type` 指定值，
`Python` 就會以預設值 'dog' 來處理：
```text
I have a dog.
My dog's name is Willie.
```
可以注意在這個函式的定義中，修改了參數的排放順序，由於對 `animal_type` 參數指定了預設值，
不需要透過引數傳入動物類型也可以處理，因此在函式呼叫中只算有一個引數 `pet_name` ，
但 `Python` 仍將這個引數視為位置引數，所以當函式呼叫中只放寵物名字當引數，此引數會對應到函式的第一個參數 `pet_name` 中。
這就是為什麼在定義函式時需要把 `pet_name` 放在前面的原因。

現在使用此函式最簡單的方式只只在呼叫函式時放入名字即可：
```text
describe_pet('willie')
```
因為只提供一個引數 'willie'，此引數會對應到函式定義的第一個參數 pet_name，因此輸出結果與前面是一樣的。

假如要描述的寵物不是小狗時，可用下列方式來呼叫函式：
```text
describe_pet(pet_name='harry', animal_type='hamster')
```

#### 等效的函式呼叫
在定義函式時可以混合使用位置引數、關鍵字引數與預設值的指定，所以一般都會有多種等效的函式呼叫方式。
下列函式的定義，其中有對一個參數指定了預設值：
```text
describe_pet(pet_name, animal_type='dog'):
```
這樣的定義在任何情況下呼叫函式時都要提供 `pet_name` 對應的引數值，
所以在提供這個引數時可依位置引數方式，也可使用關鍵字引數。

如果要描述的寵物不是小狗，就要在呼叫函式時提供 `animal_type` 對應的引數值。
同樣指定此引數時可用位置引數方式或使用關鍵字引數來處理。

下列這幾種呼叫函式的方式都是合乎規定的：
```text
# A dog named Willie.
describe_pet('willie')
describe_pet(pet_name='willie')

# A hamster named Harry.
describe_pet('harry', 'hamster')
describe_pet(pet_name='harry', animal_type='hamster')
describe_pet(animal_type='hamster', pet_name='harry')
```

#### 避免引數錯誤
開始使用函式時，也會遇到引數對應錯誤的問題，我們提供的引數不能對應函式定義要完成工作所需的資訊，
提供的引數不論多於或少於需要，都會出現錯誤訊息：
```python
def describe_pet(animal_type, pet_name):
    """Display information about a pet."""
    print("\nI have a " + animal_type + ".")
    print("My " + animal_type + "'s name is " + pet_name.title() + ".")

describe_pet()
```
`Python` 發覺函式呼叫少了必要的資訊，所以就會顯示 Traceback 錯誤，指出問題所在：
```text
Traceback (most recent call last):
  File "test.py", line 6, in <module>
    describe_pet()
TypeError: describe_pet() missing 2 required positional arguments: 'animal_type' and 'pet_name'
```
Traceback 說明該函式呼叫少用了兩個引數，並列出對應的參數名稱。

`Python` 讀取函式的程式碼，並指出需要的是引數及其對應的參數，這提供了很大的幫助，
也是盪什麼在設計程式時，要對變數和函式取名字要有描述性名稱的原因。
