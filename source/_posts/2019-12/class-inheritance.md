---
title: 類別 － 繼承
categories: Python
tags:
  - python
  - class
  - inheritance
date: 2019-12-17 16:17:32
---

### 繼承
編寫類別時，不是一定都要從零開始，如果要編寫的類別已有另一個現成很相似的類別，可以用繼承（ inheritance ）的方式製作。
一個類別繼承自另一個類別時，它會自動取得另一個類別的所有屬性和方法，
原有的類別就稱為父類別（ parent class ），而新的類別稱為子類別（ child class ）。
子類別繼承了父類別的所有屬性和方法，同時還可以定義自己專屬的屬性和方法。

<!-- more -->

#### 子類別的 `__init__()` 方法
建立子類別的實例時，`Python` 第一個要進行的工作是把值分配給父類別中的所有屬性。
若要做到這一點，子類別的 `__init__()` 方法需要父類別給予支援。

以電動車的塑模來說明，電動車屬於一種特殊的車子，
因此我們可以`類別 － 建立類別和實例的運用`篇的 Car 類別為基礎來建立新的 `ElectricCar` 類別，
這樣只需對電動車特有的屬性和方法編寫新的程式碼：
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

class ElectricCar(Car):
    """Represent aspects of a car, specific to electric vehicles."""

    def __init__(self, make, model, year):
        """Initialize attributes of the parent class."""
        super().__init__(make, model, year)

my_tesla = ElectricCar('tesla', 'model s', 2016)
print(my_tesla.get_descriptive_name())
```
一開始是原本 Car 類別的程式碼。在建立子類別時，父類別必須要放在目前的程式檔案內，且放置的位置要在子類別的前面。
之後定義一個新的 ElectricCar 子類別，定義子類別時，必須要在括號內放入父類別的名稱。
`__init__()`方法接收建立 Car 實例所需要的資訊。
`super()` 是個特殊的函式，會協助 `Python` 把父類別和子類別連接起來；
`Python` 會呼叫 ElectricCar 父類別的 `__init__()`方法，讓 ElectricCar 實例含有父類別的所有屬性。
super 的名字來自於對父類別稱呼的慣例，父類別有另一個英文名稱 superclass，而子類別另一個英文名稱是 subclass。

接著建立一個電動車實例來測試繼承是否有正確地發揮作用，在此提供 `tesla`、`model s`和2016等引數：
```text
2016 Tesla Model S
```
這個階段還沒加入電動車特有的屬性和方法，只先確定電動車具備有一般車子的屬性和方法。

#### 為子類別定義屬性和方法
當有了一個從父類別繼承來的子類別時，可對子類別新增其專有的屬性和方法，這樣都與父類別的不相同。
我們要對電動車新增一個特有的屬性（例如電池），以及一個描述該屬性的方法，
這個屬性用來存放電池容量，並寫一個輸出描述電池的方法：
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

class ElectricCar(Car):
    """Represent aspects of a car, specific to electric vehicles."""

    def __init__(self, make, model, year):
        """
        Initialize attributes of the parent class.
        Then initialize attributes specific to an electric car.
        """
        super().__init__(make, model, year)
        self.battery_size = 70

    def describe_battery(self):
        """Print a statement describing the battery size."""
        print("This car has a " + str(self.battery_size) + "-kWh battery.")

my_tesla = ElectricCar('tesla', 'model s', 2016)
print(my_tesla.get_descriptive_name())
my_tesla.describe_battery()
```
以 ElectricCar 類別建立的所有實例都會含有 self.battery_size 這個新屬性，但 Car 類別所建立的就沒有。
還有新增一個 describe_battery() 方法，功用是輸出關於電池的描述資訊。
呼叫這個方法時會看到一條描述電動車特有的說明文句：
```text
2016 Tesla Model S
This car has a 70-kWh battery.
```
對 ElectricCar 類別進行個別特殊化的處理上並沒有限制，可以根據需要新增任意數量的屬性和方法，便於能更準確對電動車進行塑模。
如果有個屬性或方法是任何一台車都有，不是電動車特有的，那就應該把這個屬性或方法加到 Car 類別而不是 ElectricCar 類別中。
這樣使用 Car 類別都能取得其一般車子的功能，使用 ElectricCar 類別的就有專屬於電動車特殊的屬性（資訊）和方法（行為）。

#### 覆寫父類別方法
如果父類別的方法不符合子類別想塑模事物的行為，都可以進行覆寫。
作法是在子類別中定義一個與父類別方法有相同名稱的方法，這樣 `Python` 就不會用父類別同名的方法，只會關注子類別中所定義的方法。

假設 Car 類別中有個名為 fill_gas_tank() 方法。但此方法對電動車沒有作用，因此想要覆寫這個方法，示範如下：
```python
class ElectricCar(Car):
    """Represent aspects of a car, specific to electric vehicles."""

    def __init__(self, make, model, year):
        """
        Initialize attributes of the parent class.
        Then initialize attributes specific to an electric car.
        """
        super().__init__(make, model, year)
        self.battery_size = 70

    def describe_battery(self):
        """Print a statement describing the battery size."""
        print("This car has a " + str(self.battery_size) + "-kWh battery.")

    def fill_gas_tank(self):
        """Electric cars don't have gas tanks."""
        print("This car doesn't need a gas tank!")
```
現在如果呼叫電動車的 fill_gas_tank() 方法， `Python` 會忽略 Car 類別中的 fill_gas_tank() 方法，而執行這裡的程式。
使用繼承這項功能，既可以讓子類別保留父類別中想要的東西，也能覆寫刪除不符合需要的內容。

#### 把實例當成屬性
當類別中有愈來愈多的屬性和方法時，程式檔案也變得愈來愈長。這樣的情況下可能要把類別的某一部份再獨立成一個類別。
我們可以把大型的類別拆分成多個一起運作的小類別。

假如持續對 ElectricCar 類別新增更多細節，就會發現其中含有很多屬於汽車電池相關的屬性和方法，
當遇到這種情況時，就不要再新增了，而是把電池相關的屬性和方法移動到另一個單獨的 Battery 類別中：
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

class Battery():
    """A simple attempt to model a battery for an electric car."""

    def __init__(self, battery_size=70):
        """Initialize the battery's attributes."""
        self.battery_size = battery_size

    def describe_battery(self):
        """Print a statement describing the battery size."""
        print("This car has a " + str(self.battery_size) + "-kWh battery.")


class ElectricCar(Car):
    """Represent aspects of a car, specific to electric vehicles."""

    def __init__(self, make, model, year):
        """
        Initialize attributes of the parent class.
        Then initialize attributes specific to an electric car.
        """
        super().__init__(make, model, year)
        self.battery = Battery()

my_tesla = ElectricCar('tesla', 'model s', 2016)

print(my_tesla.get_descriptive_name())
my_tesla.battery.describe_battery()
```
定義一個 Battery() 類別，沒有繼承任何類別。
定義`__init__()`方法除了 self 之外，還有另一個 battery_size 參數，此參數是可選擇性放入的，如果沒有提供值，就會使用預設值 70。
describe_battery() 方法也從 ElectricCar 類別移到 Battery 類別中。

在 ElectricCar 類別中新增一個 self.battery 屬性，會讓 `Python` 建立一個新的 Battery 實例，並存放在 self.battery 屬性中。
每次 `__init__()` 方法被呼叫時都會執行這項處理，任何建立的 ElectricCar 實例現都會自動建立一個 Battery 實例當成其中一個屬性。

隨後建立一台電動車實例，並將它儲存到 my_tesla 變數內。
若想要描述其電池屬性時，需要使用到電動車的 battery 屬性 `my_tesla.battery.describe_battery()`，
這樣會讓 `Python` 在 my_tesla 實例中找出 battery 屬性，並存放在 Battery 實例中的屬性呼叫 describe_battery() 方法：
```text
2016 Tesla Model S
This car has a 70-kWh battery.
```
這種類別的分拆能讓我們加入更新電池的細節，而且也不會讓 ElectricCar 類別變得很長很亂。
下面的範例再為 Battery 類別新增一個方法，可依據電池容量回報車子可行駛的續航里程：
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

my_tesla = ElectricCar('tesla', 'model s', 2016)
print(my_tesla.get_descriptive_name())
my_tesla.battery.describe_battery()
my_tesla.battery.get_range()
```
新增了 get_range() 方法，此方法做個簡單的分析，若電池容量為 70 kWh，可行駛的續航里程設為 240 英里，
若容量為 85 kWh，則可行駛的續航里程數設為 270 英里，隨後回報這個值。
最後在透過車子實例的 battery 屬性來呼叫這個方法：
```text
2016 Tesla Model S
This car has a 70-kWh battery.
This car can go approximately 240 miles on a full charge.
```
