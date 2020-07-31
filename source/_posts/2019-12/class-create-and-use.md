---
title: 類別 － 建立類別和實例的運用
categories: Python
tags:
  - python
  - class
date: 2019-12-15 11:08:54
---

物件導向程式設計（ Object-oriented programming ）是編寫應用軟體最有效率的方法之一。
在物件導向程式設計中，我們設計編寫出類別（ class ），用來代表現實世界的各種事物和情景，並以這些類別為基礎來建立物件。
從類別建立物件的過程稱之為例示或實例化（ instantiation ），這樣就能運用類別的實例（ instance ）。

### 建立和使用類別
使用類別（ class ）可以對幾乎任何事物進行塑模（ model ）。

<!-- more -->

接下來會編寫一個代表小狗的簡單 Dog 類別，此類別代表的是任意一隻小狗，並不是只針對某一特定的小狗。
思考一下大多數的寵物狗具有什麼特性？有名字和年齡（資訊），還會蹲下和翻滾（行為），
在 Dog 類別中都放入這些資訊和行為。此類別會讓 `Python` 知道如何建立代表小狗的物件。
這個類別後，將會使用它建立代表特定小狗的實例。

#### 建立 Dog 類別
以 Dog 類別所建立的每個實例都會存放有名字（ name ）和年齡（ age ），
也讓每隻小狗有蹲下（ sit() ）和翻滾（ roll_over() ）的行為能力：
```python
class Dog():
    """A simple attempt to model a dog."""

    def __init__(self, name, age):
        """Initialize name and age attributes."""
        self.name = name
        self.age = age

    def sit(self):
        """Simulate a dog sitting in response to a command."""
        print(self.name.title() + " is now sitting")

    def roll_over(self):
        """Simulate rolling over in response to a command."""
        print(self.name.title() + " rolled over!")
```
先定義一個 Dog 的類別，在 `Python` 中，第一個字母為大寫是類別的命名慣例。
這個類別定義的括號中是空的，因為我們要從零開始來建立這個類別。

##### `__init__` 方法
屬於類別的函式稱為方法（method），之前學習函式的一切都適用於這裡所提到的「方法」，唯一最不同的就是呼叫方法的方式。
`__init__`方法是一種特殊的方法，每次當我們以 Dog 類別為基礎建立新的實例時， `Python` 都會自動執行這個方法。
這個方法的名字在開頭跟結尾都有兩個底線，這樣的命名慣例可防止 `Python` 的預設方法名稱與您建立的方法名稱發生衝突。

定義`__init__`方法有三個參數：self、name 和 age 。在此方法的定義中， self 是必要的，必須放在其它參數的前面。
`self` 必須放在定義中，因為當 `Python` 隨後呼叫這個`__init__`方法時，方法的呼叫會自動傳入 self 引數。
當建立 Dog 實例時， `Python` 會呼叫 Dog 類別的 `__init__` 方法。
我們會把 name 和 age 當成引數傳入 Dog() ，而 self 則會自動傳入，因此不需要由我們傳入。
每當以 Dog 類別為基礎建立實例時，只需要提供 name 和 age 兩個引數值就可以了。

在`__init__`方法下內縮的程式區塊內，兩個變數都名字前面都有個 self 開頭，
以 self 為前導的變數都能提供類別中所有方法使用，還可透過任何由類別所建立的實例來存取這些變數。
self.name = name 會取得 name 參數中的值，並存放到 name 變數中，該變數會連接目前所建立的實例。
self.age = age 這行的處理過程跟 self.name = name 相同。
可由實例來存取的數就稱為屬性（ attribute ）。

Dog 類別中有定義兩個方法：sit() 和 roll_over()。
因為這兩個方法不需要額外的資訊，所以只定義一個 self 參數即可。之後建立的實例將可存取這兩個方法。

#### 從類別建立實例
可以將類別想像成一組指令，指示如何建立實例的指令。
Dog 類別就是一系列的指令，讓 `Python` 知道如何建立代表某隻小狗的個別實例：
```python
class Dog():
    """A simple attempt to model a dog."""

    def __init__(self, name, age):
        """Initialize name and age attributes."""
        self.name = name
        self.age = age

    def sit(self):
        """Simulate a dog sitting in response to a command."""
        print(self.name.title() + " is now sitting")

    def roll_over(self):
        """Simulate rolling over in response to a command."""
        print(self.name.title() + " rolled over!")

my_dog = Dog('willie', 6)

print("My dog's name is " + my_dog.name.title() + ".")
print("My dog is " + str(my_dog.age) + " years old.")
```
在這裡建立一個名為 'willie'、年齡為 6 歲的小狗，
`Python`讀到這行時，會使用 'willie' 和 6 當成引數呼叫 Dog 類別中的 `__init__()`方法。
`__init__()`方法建立一個表特定小狗的實例，並使用我們所提供的值來設定 name 和 age 屬性。
`__init__()`方法並沒有很明顯地放入 return 陳述句，但 `Python` 會自動返回一個代表小狗的實例。

##### 存取屬性
若要存取實例的屬性，可使用句點標示法，
我們編寫了下最程式碼來存取 my_dog 的 name 屬性的值：
```text
my_dog.name
```
句點標示法在 `Python` 中很常用到，這種語法展示了 `Python` 如何取得屬性的值。
`Python` 會先找到 my_dog 實例，再尋找與這個實例連接的 name 屬性，這個屬性與 Dog 類別中 self.name 指到的屬性相同。
my_dog.age 也用相同方式來取得 age 的值。

輸出結果為我們期望的 my_dog 資訊的匯整：
```text
My dog's name is Willie.
My dog is 6 years old.
```

##### 呼叫方法
以 Dog 類別為基礎建立實例後，就能使用句點標示法來呼叫 Dog 類別中所定義的任何方法：
```python
class Dog():
    """A simple attempt to model a dog."""

    def __init__(self, name, age):
        """Initialize name and age attributes."""
        self.name = name
        self.age = age

    def sit(self):
        """Simulate a dog sitting in response to a command."""
        print(self.name.title() + " is now sitting")

    def roll_over(self):
        """Simulate rolling over in response to a command."""
        print(self.name.title() + " rolled over!")

my_dog = Dog('willie', 6)
my_dog.sit()
my_dog.roll_over()
```
呼叫方法可寫入實例的名稱（ my_dog ）和要呼叫的方法，並以句點分隔。
執行到 my_dog.sit() 時， `Python` 會在 Dog 類別中找到 sit() 法方並執行其中的程式。
`Python` 也會以相同的方式解讀和處理 my_dog.roll_over()：
```text
Willie is now sitting
Willie rolled over!
```

##### 建立多個實例
可以從類別依照需要建立多個實例，再建立另一個名為 your_dog的實例：
```python
class Dog():
    """A simple attempt to model a dog."""

    def __init__(self, name, age):
        """Initialize name and age attributes."""
        self.name = name
        self.age = age

    def sit(self):
        """Simulate a dog sitting in response to a command."""
        print(self.name.title() + " is now sitting")

    def roll_over(self):
        """Simulate rolling over in response to a command."""
        print(self.name.title() + " rolled over!")

my_dog = Dog('willie', 6)
your_dog = Dog('lucy', 3)

print("My dog's name is " + my_dog.name.title() + ".")
print("My dog is " + str(my_dog.age) + " years old.")
my_dog.sit()

print("\nYour dog's name is " + your_dog.name.title() + ".")
print("Your dog is " + str(your_dog.age) + " years old.")
your_dog.sit()
```
每個小狗都是單獨的實例，有屬於自己的一組屬性，也能執行相同的方法：
```text
My dog's name is Willie.
My dog is 6 years old.
Willie is now sitting

Your dog's name is Lucy.
Your dog is 3 years old.
Lucy is now sitting
```
就算給第二隻小狗相同的名字和年齡，`Python` 還是會以 Dog 類別為基礎建立二個個別的實例。
可以依照需要以類別為基礎來建立所需數量的實例，條件是每個實例都要分別存放在不同的變數內，或放入串列或字典中不同的位置上。

---

### 類別和實例的運用
我們可以使用類別來對現實中的場景進行塑模，類別設計編寫好之後，多數的時間都會花在使用以這個類別所建立的實例上。
目前第一個要處理的工作是修改實例的屬性，可以直接修改實例的屬性，也可以編寫出方法，以特定的方式來進行更新修改。

#### Car 類別
下列是設計編寫出一個代表車子的類別，其中存放了關於中子的資訊，還有一個匯整這些資訊的方法：
```python
class Car():
    """A simple attempt to represent a car."""

    def __init__(self, make, model, year):
        """Initialize attributes to describe a car."""
        self.make = make
        self.model = model
        self.year = year

    def get_descriptive_name(self):
        """Return a neatly formatted descriptive name."""
        long_name = str(self.year) + ' ' + self.make + ' ' + self.model
        return long_name.title()

my_new_car = Car('audi', 'a4', 2016)
print(my_new_car.get_descriptive_name())
```
先定義了`__init__()`方法，在方法中加入三個參數：make、model 和 year 。
建立新的 Car 實例時要傳入製造廠商、型號和生產年份等資訊。
再來定義名稱為 get_descriptive_name() 的方法，使用 year、name 和 model 等屬性建來一條描述車子的文句，
並且用了 self.name、self.model 和 self.year，用以存取屬性的值。
接著以 Car 類別為基礎建立一個實例，並將它指定給 my_new_car 變數來存放。
隨後呼叫 get_descriptive_name() 方法，輸出關於我們所擁有車子的描述文句：
```text
2016 Audi A4
```
接著會為它新增一個隨時間變化的屬性來讓這個類別更有趣，我們將新增一個儲存汽車里程整數的屬性。

#### 對屬性設定預設值
類別中每個屬性都要有初姓值，就算這個值是 0 或空字串 '' 都可以。在某些情況下，在`__init__()`方法中指定這初始值是允許的。
如果對某個屬性進行了這樣的設定，就無須放入對此屬性提供初始值的參數。
下列範例新增了一個 odometer_reading 的屬性，初始值為 0。另外還新增了 read_odometer() 方法，以讀取車子的里程數：
```python
class Car():
    """A simple attempt to represent a car."""

    def __init__(self, make, model, year):
        """Initialize attributes to describe a car."""
        self.make = make
        self.model = model
        self.year = year
        self.odometer_reading = 0

    def get_descriptive_name(self):
        """Return a neatly formatted descriptive name."""
        long_name = str(self.year) + ' ' + self.make + ' ' + self.model
        return long_name.title()

    def read_odometer(self):
        """Print a statement showing the car's mileage."""
        print("This car has " + str(self.odometer_reading) + " miles on it.")

my_new_car = Car('audi', 'a4', 2016)
print(my_new_car.get_descriptive_name())
my_new_car.read_odometer()
```
現在當 `Python` 呼叫 `__init__()` 方法來建立新的實例時，會像前一個範例一樣以屬性的方式存放資訊。
接著 `Python` 會建立一個 odometer_reading 屬性，並將它的初始值設為 0。
之後定義了一個 read_odometer() 方法，此方法能讓我們輕鬆地取得車子的里程數：
```text
2016 Audi A4
This car has 0 miles on it.
```
但在車子賣出時里程數為 0 的並不多，因此我們需要有一個能修改這個屬性值的方法。

#### 修改屬性的值
有三種不同的方式可修改屬性的值：
* 直接利用實例進行修改
* 利用方法進行設定
* 利用方法進行值的增加

##### 直接修改屬性的值
若要修改屬性的值，最簡單的方式就是透過實例直接存取，下列示範直接把里程數設為 23：
```python
class Car():
    """A simple attempt to represent a car."""

    def __init__(self, make, model, year):
        """Initialize attributes to describe a car."""
        self.make = make
        self.model = model
        self.year = year
        self.odometer_reading = 0

    def get_descriptive_name(self):
        """Return a neatly formatted descriptive name."""
        long_name = str(self.year) + ' ' + self.make + ' ' + self.model
        return long_name.title()

    def read_odometer(self):
        """Print a statement showing the car's mileage."""
        print("This car has " + str(self.odometer_reading) + " miles on it.")

my_new_car = Car('audi', 'a4', 2016)
print(my_new_car.get_descriptive_name())

my_new_car.odometer_reading = 23
my_new_car.read_odometer()
```
直接使用句點標示法來直接存取並設定車子的 odometer_reading屬性。
讓 `Python` 在 my_new_car 實例中找出 odometer_reading 屬性，並將 23 指定進去：
```text
2016 Audi A4
This car has 23 miles on it.
```
有時候我們想要像這以直接存取屬性的值，但有時候則需要編寫對屬性進行更新的方法。

##### 透過方法修改屬性的值
擁有更新屬性的方法對我們很有幫助，這樣就不需要直接存取屬性，而可將值傳入到方法，由它在內部進行更新修改：
```python
class Car():
    """A simple attempt to represent a car."""

    def __init__(self, make, model, year):
        """Initialize attributes to describe a car."""
        self.make = make
        self.model = model
        self.year = year
        self.odometer_reading = 0

    def get_descriptive_name(self):
        """Return a neatly formatted descriptive name."""
        long_name = str(self.year) + ' ' + self.make + ' ' + self.model
        return long_name.title()

    def read_odometer(self):
        """Print a statement showing the car's mileage."""
        print("This car has " + str(self.odometer_reading) + " miles on it.")

    def update_odometer(self, mileage):
        """Set the odometer reading to the given value."""
        self.odometer_reading = mileage

my_new_car = Car('audi', 'a4', 2016)
print(my_new_car.get_descriptive_name())

my_new_car.update_odometer(23)
my_new_car.read_odometer()
```
在 Car 類別新增了 update_odometer() 方法，此方法接收一個里程數值，並將它存放到 self.odometer_reading 內。
之後再呼叫 update_odometer() 方法並傳入 23 當引數（此引數對應於方法定義中的 mileage 參數）。
此方法執行後會將里程數改成 23，而 read_odometer() 會輸出此數值：
```text
2016 Audi A4
This car has 23 miles on it.
```
還可以對 update_odometer() 方法進行擴充，讓它在修改里程數時做些其它的工作。
下面範例新增一些邏輯處理，禁止其它人將里程數往回調小：
```python
class Car():
    """A simple attempt to represent a car."""

    def __init__(self, make, model, year):
        """Initialize attributes to describe a car."""
        self.make = make
        self.model = model
        self.year = year
        self.odometer_reading = 0

    def get_descriptive_name(self):
        """Return a neatly formatted descriptive name."""
        long_name = str(self.year) + ' ' + self.make + ' ' + self.model
        return long_name.title()

    def read_odometer(self):
        """Print a statement showing the car's mileage."""
        print("This car has " + str(self.odometer_reading) + " miles on it.")

    def update_odometer(self, mileage):
        """
        Set the odometer reading to the given value.
        Reject the change if it attempts to roll the odometer back.
        """
        if mileage >= self.odometer_reading:
            self.odometer_reading = mileage
        else:
            print("You can't roll back an odometer!")
```
現在的 update_odometer() 方法要在修改屬性前檢查指定的里程值是否合理，
如果新的指定里程數（ mileage ）大於或等於原本的里程式，那就將新的里程數指定進原本的里程數屬性中，
若不是則輸出一條警告訊息，告知不能對里程數回調。

##### 利用方法進行值的增加
有時候我們希望讓屬性的值以特定的數值增加，而不是指定新的值進去。
假設有一台二手車，從購買到登記期間增加了 100 英里的里程數，下最的方法能傳入這個新增里程數，並加進原本里程數內：
```python
class Car():
    """A simple attempt to represent a car."""

    def __init__(self, make, model, year):
        """Initialize attributes to describe a car."""
        self.make = make
        self.model = model
        self.year = year
        self.odometer_reading = 0

    def get_descriptive_name(self):
        """Return a neatly formatted descriptive name."""
        long_name = str(self.year) + ' ' + self.make + ' ' + self.model
        return long_name.title()

    def read_odometer(self):
        """Print a statement showing the car's mileage."""
        print("This car has " + str(self.odometer_reading) + " miles on it.")

    def update_odometer(self, mileage):
        """
        Set the odometer reading to the given value.
        Reject the change if it attempts to roll the odometer back.
        """
        if mileage >= self.odometer_reading:
            self.odometer_reading = mileage
        else:
            print("You can't roll back an odometer!")

    def increment_odometer(self, miles):
        """Add the given amount to the odometer reading."""
        self.odometer_reading += miles

my_used_car = Car('subaru', 'outback', 2013)
print(my_used_car.get_descriptive_name())

my_used_car.update_odometer(23500)
my_used_car.read_odometer()

my_used_car.increment_odometer(100)
my_used_car.read_odometer()
```
首先新增一個 increment_odometer() 方法，接收一個單位為英里的數值，並會將此數值加到 self.odometer_reading 中。
接著建立一台二手車實例，並呼叫 update_odometer() 方法傳入 23500，把這台二手車的里程數設為 23500。
之後呼叫 increment_odometer() 方法並傳入 100，把從購買到登記時新行駛的 100 英里增加到原本的里程數中：
```text
2013 Subaru Outback
This car has 23500 miles on it.
This car has 23600 miles on it.
```
之後也可以很容易的修改這個方法，加入禁止增量為負數的處理，防止有人用這個來回調車子的里程數。