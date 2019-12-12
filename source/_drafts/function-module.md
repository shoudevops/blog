---
title: 函式 Part IV.
categories: Python
tags:
- Python
- function
---
### 把函式儲存在模組中
* 函式有個優點是它們和主程式部份可以分開放置，為函式取一個具有描述性的名字，這樣在主程式中使用時能讓程式更易讀好懂。
* 可以更進一步將函式儲存在一個獨立的檔案中，這個檔案稱為模組（ module ），需要使用函式時匯入這個模組到主程式中。
* Import 陳述句告知 `Python` 在目前執行的程式檔中可取用模組內的程式碼。

<!-- more -->

#### 匯入整個模組
要讓函式變成可以匯入，首先就要建立模組，模組的副檔名為 `.py`，其中放了要匯入程式中的程式碼。
首先建立一個存放了 make_pizza() 函式的模組，檔案名稱為 pizza.py：
```python
def make_pizza(size, *toppings):
    """Summarize the pizza we are about to make."""
    print("\nMaking a " + str(size) + "-inch pizza with the following toppings:")
    for topping in toppings:
        print("- " + topping)
```
接著在 pizza.py 所在的資料夾中建立另一個檔案名稱為 making_pizzas.py 的檔案，
這個檔案會匯入上面建立的模組，再呼叫 make_pizza() 函式兩次：
```python
import pizza

pizza.make_pizza(16, 'pepperoni')
pizza.make_pizza(12, 'mushrooms', 'green peppers', 'extra cheese')
```
`import pizza` 這行指令會讓 `Python` 開啟 pizza.py 檔案，並將其中所有的函式都複雜到這個檔案內。
若想要呼叫匯入模組內的函式，可指定匯入的模組名稱（ pizza ）和函式名稱（ make_pizza() ），並以句點（ . ）分隔連接。
輸出的內容與沒有用匯入模組的原始版本程式是相同的：
```text
Making a 16-inch pizza with the following toppings:
- pepperoni

Making a 12-inch pizza with the following toppings:
- mushrooms
- green peppers
- extra cheese
```
上面為第一種匯入的方式，使用 import 陳述句並指定模組名稱。
使用這個 import 語法匯入 module_name.py 的整個模組，就能以下最這樣的語法來取用其中的任何一個函式：
```text
module_name.function_name()
```

#### 匯入特定的函式
還可以匯入模組中某個特定的函式，其匯入的語法如下：
```text
from module_name import function_name
```
若要從模組中匯入多個函式時，可用逗號分隔：
```text
from module_name import function_0, function_1, function_2
```
以上面的 making_pizzas.py 為例，如果只想匯入想要用使用的函式，指令語法如下：
```python
from pizza import make_pizza

make_pizza(16, 'pepperoni')
make_pizza(12, 'mushrooms', 'green peppers', 'extra cheese')
```
使用這種語法，呼叫函式時就不需要加模組名稱和句號，
在 import 陳述句已經明顯匯入了 make_pizza() 函式，因此呼叫時只需直接指定這個函式名稱即可。

#### 使用 as 為函式指定別名
如果要匯入的函式名稱可能會與您程式中現有的函式名稱產生衝突，或是函式的名稱太長等因素下，
我們可以為匯入的函式取一個獨一無二的別名（ alias ），在匯入函式時就能為它指定別名：
```python
from pizza import make_pizza as mp

mp(16, 'pepperoni')
mp(12, 'mushrooms', 'green peppers', 'extra cheese')
```
範例中的 import 陳述句為 make_pizza() 函式取了別名為 mp()，後讀要呼叫 make_pizza() 時，可縐寫成 mp()，
`Python` 會找到匯入的 make_pizza() 來執行，使用別名也能避開程式中若也有寫了 make_pizza() 函式的混淆。

指定別名的匯入語法如下：
```text
from module_name import function_name as fn
```

#### 使用 as 為模組指定別名
也可以為匯入的模組取一個別名。給定模組一個較短的別名，例如 pizza 模組取一個別名叫 p，
這樣就能更輕鬆簡潔的呼叫模組中的函式。與寫入 pizza.make_pizza() 語句， p.make_pizza 會更簡短：
```python
import pizza as p

p.make_pizza(16, 'pepperoni')
p.make_pizza(12, 'mushrooms', 'green peppers', 'extra cheese')
```
上面範例中的 import 陳述句為 pizza 模組取了個叫作 p 的別名，但在該模組內的所有函式的名稱都沒變。
呼叫函式時，可寫入 p.make_pizza() ，這樣就使程式碼更簡潔，也能讓我們降低對模組名稱的注意，集中關注在函式名稱上。
這些函式名稱很明確指出它們的功用，從理解程式碼來看，它們比模組名稱更為重要。

為模組取一個別名的語法如下：
```text
import module_name as mn
```

#### 匯入模組中所有函式
使用星號（ * ）運算子可讓 `Python` 匯入模組中所有的函式：
```python
from pizza import *

make_pizza(16, 'pepperoni')
make_pizza(12, 'mushrooms', 'green peppers', 'extra cheese')
```
import 陳述句中的星號會讓 `Python` 把 pizza 模組中所有函式都複製一份到這個程式檔中。
因為每個函式都已匯入，所以可直接用函式名稱來呼叫，不需要再加上模組名稱和句點的表示法。
不過在使用不是自己編寫的大型模組時，最好不要用這種匯入方式，
如果模組中有的函式名稱剛好與您專案中所使用的名稱相同時，可能會產生不預期的結果，
 `Python` 可能在遇到多個名稱相同的函式或變量，因為名稱相同而直接覆蓋過去，不是以分開的方式來呼叫使用。

最好的做法是只匯入需要的函式，或是匯入模組並使用句點表示法。這樣能讓程式變得更清楚且易讀好懂。
匯入模組所有函式語法如下：
```text
from module_name import *
```

---

### 函式的風格
編寫函式時要記住幾個編排風格上的細節。
* 函式取名字時要指定具有描述性的名字，且只用小寫英文字母和底線。
* 具有描述性的名字能幫助您首別人知道這段程式碼的功能。
* 每個函式中應該放入簡介此函式功用的注釋，這個注釋應緊接在函式定義的後面，並使用 docstring 格式。
* 在文件編寫良好的函式中，能讓其它程式設計人員只需閱讀這段 docstring 的文字描述就知道其功能用使用方法。
* 只需要知道函式名稱和需傳入的引數，以及迴回值的型別，就能在自己的程式中取用它。

在定義函式時，在對參數指定預設值時，等號兩側不要放空格：
```text
def function_name(parameter_0, parameter_1='default value')
```

在呼叫函式時傳入關鍵字引數時也應遵守這項約定，等號兩側不要放空格：
```text
function_name(value_0, parameter_1='value')
```

PEP8 中建議程式碼一行的長度不要超過 79 個字元，這樣只要文字編輯器的視窗大小適中，就能完整呈現一整行程式。
如果參數很多，使得函式定義的長度超過 79 個字元，那麼可以在函式定義中所輸入的左號後面用 Enter 鍵換行，
並在下一行按兩次 Tab 鍵（ 8 格空白 ）內縮，讓所有參數和只內縮一層的函式本體有所區別。
大多數的文字編輯器在第一個參數設好後按下 Enter 鍵，都會有自動對齊後續參數的功能，其內縮會與第一個參數對齊：
```text
def function_name(
        parameter_0, parameter_1, parameter_2, 
        parameter_3, parameter_4, parameter_5):
    function body...
```

如果程式或模組中含有很多函式，可用兩行空行來把相鄰的函式分隔開來，
這樣能更容易判斷上個函式在什麼位置是結尾，而下個函式是從哪裡開始。

所有的 import 陳述句都要放程式檔案的最開頭的位置，除非程式檔案開頭已放了注釋說明程式功用的文字。