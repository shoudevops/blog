---
title: 類別 － 匯入類別
categories: Python
tags:
  - python
  - class
date: 2019-12-18 10:15:39
---

### 匯入類別
隨著不斷為類別新增功能，程式檔會變得愈來愈長，就算已使用繼承功能也是如此。
為遵循 `Python` 的設計理念，檔案要盡量維持簡潔乾淨。
因此 `Python` 允許我們把類別儲存在模組中，在需要使用時由主程式匯入使用。

<!-- more -->

#### 匯入單個類別
先建立一個只放入 Car 類別的模組（ car.py ），並從現在開始使用這個模組的程式都要以更具體的名字來命名，如：my_car.py。
下列是 car.py 模組的內容，只放入 Car 類別的程式碼：
```python
"""A class that can be used to represent a car."""


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
```
在第一行放入模組層級的文件字串（ docstring ），描述此模組的內容及其功用，在建立模組時都應該要放入這樣的文件字串。

再來建立另一份 my_car.py 檔案，在其中匯入 Car 類別來建立實例：
```python
from car import Car

my_new_car = Car('audi', 'a4', 2016)
print(my_new_car.get_descriptive_name())

my_new_car.odometer_reading = 23
my_new_car.read_odometer()
```
第一行的 import 陳述句會讓 `Python` 開啟 car 模組，並匯入 Car 類別。
如此就可以直接取用 Car 類別，執行的輸出結果如下所示：
```text
2016 Audi A4
This car has 23 miles on it.
```
匯入類別是很有效率的程式設計方式。若在這支程式中直接寫入整個 Car 類別，那檔案內容就會變很長。
將這個類別移到一個單獨的模組檔案中，再匯入模組，一樣可以使用所有的功能，但主程式的檔案就變得簡潔乾淨而易讀好懂。
這樣的處理方式能把大部份的程式邏輯存放在獨立的檔案中，確定好這個類別有遵照我們所期望的方式運作，就可以不再管這個檔案了，
轉而把程式設計的施點放在主程式更高層的邏輯思維上。

#### 在模組中存放多個類別
在一個模組中可存放任意數量的類別，但放在其中的類別彼此之間還是要有某種相關性比較好。
Battery 類別和 ElectricCar 類別都是車子相關功用的塑模，所以把它們都放入 car.py 模組內：
```python
"""A set of classes used to represent gas and electric cars."""


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


class Battery():
    """A simple attempt to model a battery for an electric car."""

    def __init__(self, battery_size=70):
        """Initialize the battery's attributes."""
        self.battery_size = battery_size

    def describe_battery(self):
        """Print a statement describing the battery size."""
        print("This car has a " + str(self.battery_size) + "-kWh battery.")

    def get_range(self):
        """Print a statement about the range this battery provdies."""
        if self.battery_size == 70:
            range = 240
        elif self.battery_size == 85:
            range = 270
        
        message = "This car can go approximately " + str(range)
        message += " miles on a full charge."
        print(message)      


class ElectricCar(Car):
    """Represent aspects of a car, specific to electric vehicles."""

    def __init__(self, make, model, year):
        """
        Initialize attributes of the parent class.
        Then initialize attributes specific to an electric car.
        """
        super().__init__(make, model, year)
        self.battery = Battery()
```
現在可以建立一個 my_electric_car.py 的檔案，匯入 ElectricCar 類別，再建立一台電動車實例：
```python
from car import ElectricCar

my_tesla = ElectricCar('tesla', 'model s', 2016)

print(my_tesla.get_descriptive_name())
my_tesla.battery.describe_battery()
my_tesla.battery.get_range()
```
輸出的結果與之前所看到的相同，但這支程式把大部份的處理邏輯都隱藏到模組中：
```text
2016 Tesla Model S
This car has a 70-kWh battery.
This car can go approximately 240 miles on a full charge.
```

#### 從模組中匯入多個類別
也可以依據需要在主程式檔案中匯入多個類別。
假設要在同一支程式中建立一般車和電動車的實例，這衡就需要把 Car 和 ElectricCar 類別都匯入：
```python
from car import Car, ElectricCar

my_beetle = Car('volkswagen', 'beetle', 2016)
print(my_beetle.get_descriptive_name())

my_tesla = ElectricCar('tesla', 'model s', 2016)
print(my_tesla.get_descriptive_name())
```
第一行是指從一個模組中匯入多個類別，其中多個類別是以逗號分隔開。匯入必要的類別後就可依據需要建立類別各自的實例。
這個範例建立了一台 Volkswagen Beetle 的一般車實例與 Tesla Roadster 的電動車實例：
```text
2016 Volkswagen Beetle
2016 Tesla Roadster
```

#### 匯入整個模組
還可以匯入整個模組，再用句點標示法存取所需的類別。這樣匯入方法簡單，程式也易讀好懂。
由於建立類別實例的程式碼都含有模組名稱和句點，因此不會與目前檔案中使用的相同名稱產生衝突。
下列範例匯入整個 car 模組，並建立一台一般車和一台電動車：
```python
import car

my_beetle = car.Car('volkswagen', 'beetle', 2016)
print(my_beetle.get_descriptive_name())

my_tesla = car.ElectricCar('tesla', 'roadster', 2016)
print(my_tesla.get_descriptive_name())
```
第一行即匯入整個 car 模組，接著用 module_name.class_name 語法存取需要的類別。
建立一台 Volkswagen Beetle 車子實例與 Tesla Roadster 車子實例。

#### 匯入模組中的所有類別
我們可以匯入模組中的每一個類別，語法如下：
```text
from module_name import *
```
不推薦使用這種方式匯入，假如可以在程式檔開端處所看到的 import 陳述句中看到匯入哪些類別，對於程式的理解是很有幫助的。
上面範例以一個星號匯入所有類別是很難看出到底匯了什麼類別，也可能引起名稱衝突之類的問題，
如果不小心匯入一個與主程式檔案內取名稱同的類別，就會引發判讀上的錯誤。

當需要從一個模組中要匯入很多類別時，最好還是以匯入整個模組的方式匯入，
然後用 module_name.class_name 語法來存取需要的類別。
這樣雖然程式檔案的開頭並沒有列出用到的模組，但因為存取匯入類別需要加上模組名稱和句點，
就能清楚知道程式中哪些地方用了這樣的匯入模組，進而避免類別同名的衝突。

#### 在模組中匯入另一個模組
有時候需要把類別分到多個模組內，避免某個模組過於龐大，或避免在同一個模組中儲存太多不相干的類別。
把類別存放到多個模組中時，可能會發現某個模組中的類別是依賴著另一個模組中的類別，
在這種情況下，就會在模組中匯入所依賴的模組。

例如 Car 類別存放在一個模組中，而 ElectricCar 和 Battery 類別則存放在另一個模組。
把第二個模組取名為 electric_car.py ，並將 ElectricCar 和 Bettery 類別移到這個模組中：
```python
"""A set of classes that can be used to represent electric cars."""

from car import Car


class Battery():
    """A simple attempt to model a battery for an electric car."""

    def __init__(self, battery_size=70):
        """Initialize the battery's attributes."""
        self.battery_size = battery_size

    def describe_battery(self):
        """Print a statement describing the battery size."""
        print("This car has a " + str(self.battery_size) + "-kWh battery.")

    def get_range(self):
        """Print a statement about the range this battery provdies."""
        if self.battery_size == 70:
            range = 240
        elif self.battery_size == 85:
            range = 270

        message = "This car can go approximately " + str(range)
        message += " miles on a full charge."
        print(message)


class ElectricCar(Car):
    """Represent aspects of a car, specific to electric vehicles."""

    def __init__(self, make, model, year):
        """
        Initialize attributes of the parent class.
        Then initialize attributes specific to an electric car.
        """
        super().__init__(make, model, year)
        self.battery = Battery()
```
ElectricCar 類別需要用到 Car 這個父類別，因此直接把 Car 類別匯入這個模組內。

現在就可以從每個模組中匯入需要的類別，並根據需要建立各種類型的車子實例：
```python
from car import Car
from electric_car import ElectricCar

my_beetle = Car('volkswagen', 'beetle', 2016)
print(my_beetle.get_descriptive_name())

my_tesla = ElectricCar('tesla', 'roadster', 2016)
print(my_tesla.get_descriptive_name())
```
分別匯入 car 模組中的 Car 類別與 electric_car 模組中的 ElectricCar 類別。
從輸出結果來看這兩台車子實例都有正確建立：
```text
2016 Volkswagen Beetle
2016 Tesla Roadster
```
