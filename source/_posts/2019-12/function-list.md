---
title: 函式 － 串列應用與任意數量的引數
categories: Python
tags:
  - python
  - function
  - list
date: 2019-12-12 09:15:11
---

### 傳入串列
函式傳入串列是很好用的功能，把串列傳入函式後，函式就能直接存取其內容。

假設有個使用者串列，我們要對串列中每位使用者輸出問候文字：
```python
def greet_users(names):
    """Print a simple greeting to each user in the list."""
    for name in names:
        msg = "Hello, " + name.title() + "!"
        print(msg)

usernames = ['hannah', 'ty', 'margot']
greet_users(usernames)
```

<!-- more -->

定義 greet_users() 能接收名字串列，並將其存放在 names 引數內。
函式以迴圈遍訪接收的串列，並對其中每位使用者輸出一條問候文句。
隨後定義一個 usernames 串列，然後呼叫 greet_users() 函式並把串列傳入：
```text
Hello, Hannah!
Hello, Ty!
Hello, Margot!
```
當要處理一組使用者並輸出問候文句時，可呼叫這個函式來處理。

#### 在函式中修改串列
串列傳入函式後，函式就可對串列進行修改。
函式中對中列所做的任何修改都是永久性的，能讓我們有效率地處理大量的資料。

假設有一家 3D 列印模型的公司，能提供畢者提交設計來印出模型。
要印出模型的設計提案都儲存在一個串列內，印出後會移到另一個串列中。
下列是不使用函式的情況：
```python
# Star with some designs that need to be printed.
unprinted_designs = ['iphone case', 'robot pendant', 'dodecahedron']
completed_models = []

# Simulate printing each design, until none are left.
# Move each design to completed_models after printing.
while unprinted_designs:
    current_design = unprinted_designs.pop()

    # Simulate creating a 3D print from the design.
    print("Printing model: " + current_design)
    completed_models.append(current_design)

# Display all completed models.
print("\nThe following models have been printed:")
for completed_model in completed_models:
    print(completed_model)
```
建立一個要印出的模型設計提案串列 unprinted_designs，還有建立一個空串列 completed_model 來存放列印完成的模型。
只要 unprinted_design 串列中還有設計項目，while 迴圈就會處理印出設計的過程：
從串列尾端提取一個設計項目並刪除它，並存放到 current_design 變數中，顯示一條正在印出目前項目的訊息，
隨後將設計項目新增到 completed_models 串列中。迴圈結束後，顯示已印出的所有設計項目：
```text
Printing model: dodecahedron
Printing model: robot pendant
Printing model: iphone case

The following models have been printed:
dodecahedron
robot pendant
iphone case
```
確定範例中的程式沒有問題後，可以編寫兩個函式來重構這些程式碼，每個函式負責一件特定的工作。
第一個函式負責處理印出設計項目的工作，第二個函式則匯整印了哪些設計項目：
```python
def print_models(unprinted_designs, completed_models):
    """
    Simulate printing each design, util none are left.
    Move each design to completed_models after printing.
    """
    while unprinted_designs:
        current_design = unprinted_designs.pop()

        # Simulate creating a 3D print from the design.
        print("Printing model: " + current_design)
        completed_models.append(current_design)

def show_completed_models(completed_models):
    """Show all the models that were printed."""
    print("\nThe following models have been printed:")
    for completed_model in completed_models:
        print(completed_model)

unprinted_designs = ['iphone case', 'robot pendant', 'dodecahedron']
completed_models = []

print_models(unprinted_designs, completed_models)
show_completed_models(completed_models)
```
定義了兩個函式之後，一併將兩個參數的內容定義完成，隨後只要呼叫並傳入正確的引數即可。
此程式的輸出與前面沒有用函式的版本相同，但程式的內容組織整理得更好，也更易於日後擴充和維護。
完成大部份工作的程式都移到這兩個函式內了，因為讓程式的主體更易讀好懂。
使用具有描述性的函式名稱，讓人在閱讀程式時很容易理解其功用，就算沒有任何注釋也沒關係。

上面的程式示範了「每個函式都應只負責一件特定工作」的理念。
當您在設計和編寫函式時，若發現它處理的工作太多時，請試著將工作進行劃分，看能否分成兩個函式來處理。
請記住在函式中也可以呼叫另一個函式，這個觀念有助於把複雜的工作分割成一系列的處理步驟。

#### 防止函式修改串列內容
有時候我們希望程式要禁止函式修改串列的內容。
以上面的範例來看，就算印出了所有設計項目後，也要保留原本還沒印出模型的設計串列，用此串列當作紀錄備案。
但因為已將所有設計項目從 unprinted_designs 串列提取出來，這個串列變成空的了。
若想要解決這個問題，可以對函式傳入串列的複製品，而不是傳入原本的串列，這樣函式所進行的相關處理只會影響到複製品，
原本的串列則不受影響，呼叫函式傳入串列的複製品，作法如下：
```text
function_name(list_name[:])
```
`[:]` 是切片表示法，可建立串列的複製品。
所以在上面範例中，若不想提取清空原本的 unprinted_design 串列，可以用下列的方式呼叫 print_models() 函式：
```text
print_models(unprinted_designs[:], completed_models)
```
這樣 print_models() 函式用的就是 unprinted_designs 串列的複製品，不是原本的串列。
如之前的處理，completed_models 串列會蒐集已印出模型的設計項目名稱，
但函式所做的處理並不會影響原本的 unprinted_designs 串列。

雖然對函式傳入串列的複製品可保留原本串 列的內容，但除非有充分的理由，
不然還是以原本的串列來進行傳入和處理是比較好的做法。
因為函式直接用原本的串列會比較有效率，可避免花費時間和記憶體空間來複製串列，當處理的串列很大時更是如此。

---

### 傳入任意數量的引數到函式內
有時候我們預先不知道函式需要接收多少個引數，還好 `Python` 允許函式呼叫陳述句中可蒐集任意數量的引數。

例如，有個製作披薩的函式要接收多種配料來製作，但無法預知顧客會選多少種配料。
下列的函式定義中只有一個參數 `*toppings`，這樣的定義後不管呼叫函式時提供了多少個引數，此參數都會把它們蒐集起來：
```python
def make_pizza(*toppings):
    """Print the list of toppings that have been requested."""
    print(toppings)

make_pizza('pepperoni')
make_pizza('mushrooms', 'green peppers', 'extra cheese')
```
`*toppings` 參數中的星號會讓 `Python` 建立一個名稱是 toppings 的空多元組，並將接收到的所有值都裝入這個多元組內。
函式本體內的 print 陳述句會輸出顯示來證實 `Python` 能處理用一個引數和三個引數呼叫函式的情形。
函式會以類似的方式處理不同的呼叫，請留意！ `Python` 都會把引數裝進一個多元組內 就算只有一個引數值也一樣：
```text
('pepperoni',)
('mushrooms', 'green peppers', 'extra cheese')
```
現在可以把 print 陳述句換成迴圈，對配料串列以迴圈遍訪，並將所點的披薩的配料進行描述：
```python
def make_pizza(*toppings):
    """Summarize the pizza we are about to make."""
    print("\nMaking a pizza with the following toppings:")
    for topping in toppings:
        print("- " + topping)

make_pizza('pepperoni')
make_pizza('mushrooms', 'green peppers', 'extra cheese')
```
不論在呼叫函式時用一個引數或三個引數，這個函式都能好好處理：
```text
Making a pizza with the following toppings:
- pepperoni

Making a pizza with the following toppings:
- mushrooms
- green peppers
- extra cheese
```

#### 一起使用位置引數和任意數量引數
如果要讓函式接收不同型別的引數，就必須要在函式定義中把接收任意數量引數的參數設定放在最尾端。
`Python` 會先比對位置引數和關鍵字引數，然後才把剩下的引數都蒐集到一個參數內。

例如上面的程式內，函式還需要加一個代表披薩大小的引數，那就必須要把這個參數放在 `*toppings` 參數的前面：
```python
def make_pizza(size, *toppings):
    """Summarize the pizza we are about to make."""
    print("\nMaking a " + str(size) + 
        "-inch pizza with the following toppings:")
    for topping in toppings:
        print("- " + topping)

make_pizza(16, 'pepperoni')
make_pizza(12, 'mushrooms', 'green peppers', 'extra cheese')
```
`Python` 會把接收到第一個值存放到 size 參數內，並將其它所有值都存放到多元組 toppings。
函式呼叫中，先給定代表披薩大小的引數值，然後依照顧客給定任意數量的配料：
```text
Making a 16-inch pizza with the following toppings:
- pepperoni

Making a 12-inch pizza with the following toppings:
- mushrooms
- green peppers
- extra cheese
```

#### 使用任意數量的關鍵字引數
有時候我們會希望函式接收任意數量的引數，但預先卻不知道要傳入函式的是什麼樣的資訊。
這種情況下，可以讓函式變成能接收任意數量的鍵 － 值對，在呼叫函式時提供多少的鍵 － 對就接收多少對。
以下範列要從使用者接收資訊，但不確定收到什麼樣的資訊內容：
```python
def build_profile(first, last, **user_info):
    """Build a dictionary containing everything we know about a user."""
    profile = {}
    profile['first_name'] = first
    profile['last_name'] = last
    for key, value in user_info.items():
        profile[key] = value
    return profile

user_profile = build_profile('albert', 'einstein', location='princeton', field='physics')
print(user_profile)
```
函式的定義中要求提供名（first）和姓（last），同時允許使用者依據需要提供任意數量的名字 － 值對。
**user_info 參數的兩個星號會讓 `Python` 建立 user_info 的空字典，並將接收到的所有名字 － 值對都裝入這個字典內。
再來以迴圈遍訪 user_info 中的鍵 － 值對項目，並把每個鍵 － 值對都新增到 profile 字典中。
最後把 profile 字典返回到呼叫函式的那一行指令：
```text
{'first_name': 'albert', 'last_name': 'einstein', 'location': 'princeton', 'field': 'physics'}
```
返回字典中含有名和姓，以及求學地點與科系。
呼叫這個函式時不論額外提供多少的鍵 － 值對，這個函式都能正確處理。

在設計編寫函式時，我們可以用各種方式混合使用位置引數、關鍵字引數和任意數量引數這三個應用。
目前就先使用最簡單的方式來完成程式工作就好了。
繼續往下學習，就能掌握在各種不同情況下要使用哪一種方法是最有效率的。
