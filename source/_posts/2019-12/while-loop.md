---
title: while 迴圈
categories: Python
tags:
- python
- while
date: 2019-12-09 17:35:05
---

### 簡介 while 迴圈
for 迴圈收集項目的集合，並對集合中的每個項目執行一次程式區塊。
相較之下，while 迴圈在條件為真時會一直不斷地執行。

#### while 迴圈實作

<!-- more -->

用 while 迴圈透過一系列的數字來計數：
```python
current_number = 1
while current_number <= 5:
    print(current_number)
    current_number += 1
```
只要 current_number 小於等於5，就執行此迴圈中的程式區塊。
接著輸出 current_number 的值，再使用 `+=` 將變數的值加 1。
（運算子 += 是 current_number = current_number + 1 的縮寫）
```text
1
2
3
4
5
```

#### 讓使用者決定什麼時候結束
放入一個 while 迴圈讓程式在使用者的意願下一直執行。
定義一個結束值（ quit value ），只要使用者沒有輸入這個值，程式就會一直執行：
```python
prompt = "\nTell me something, and I will repeat it back to you: "
prompt += "\nEnter 'quit' to end the program. "

message = ""
while message != "quit":
    message = input(prompt)
    print(message)
```
先定義提示的訊息文字，告知使用者有兩種輸入的選項。再來設定一個 message 變數，用來存放使用者輸入的值，
先將 message 變數設定空字串，讓 `Python` 在第一次到達 while 迴圈時會將 message 與 'quit' 進行檢測比較。
若輸入的內容不是 'quit' 時，這個迴圈會一直執行。迴圈內的第一行會顯示文字，等待使用者輸入，
不論使用者輸入什麼內容，都會存放到 message 變數中並輸出顯示。
當使用者最終輸入 'quit' ，`Python` 就會停止 while 迴圈，而整支程式也就結束離開：
```text
Tell me something, and I will repeat it back to you: 
Enter 'quit' to end the program. Hello everyone!
Hello everyone!

Tell me something, and I will repeat it back to you: 
Enter 'quit' to end the program. Hello again.
Hello again.

Tell me something, and I will repeat it back to you: 
Enter 'quit' to end the program. quit
quit
```
執行之後發現最後輸入的 'quit' 也輸出了，因此可以再做簡單的修改：
```python
prompt = "\nTell me something, and I will repeat it back to you: "
prompt += "\nEnter 'quit' to end the program. "

message = ""
while message != "quit":
    message = input(prompt)
    if message != 'quit':
        print(message)
```
現在程式在輸出訊息前會進行檢測，如果不是 'quit' 時才會輸出：
```text
Tell me something, and I will repeat it back to you: 
Enter 'quit' to end the program. Hello everyone!
Hello everyone!

Tell me something, and I will repeat it back to you: 
Enter 'quit' to end the program. Hello again.
Hello again.

Tell me something, and I will repeat it back to you: 
Enter 'quit' to end the program. quit
```

#### 使用旗標
若有支程式要在多個條件都為 True 的情況下才執行，則可以定義一個變數用來判別整支程式是否在作用中，
這樣的變數稱為「旗標（ flag ）」，用來當作程式執行的交通號誌。
當此旗標為 True 時讓程式可以繼續執行，若有任何事件讓旗標變成 False 時讓程式停止。
如此一來，while 陳述句中就只需檢測旗標是否為 True 即可，而所有的檢測可放在程式的其它地方來設定：
```python
prompt = "\nTell me something, and I will repeat it back to you:"
prompt += "\nEnter 'quit' to end the program. "

active = True
while active:
    message = input(prompt)

    if message == 'quit':
        active = False
    else:
        print(message)
```
在迴圈開始前將 active 變數設為 True，讓程式開始的狀態為啟用。
這樣簡化了 while 迴圈的語法，條件式不用在其中作比較運算，相關的處理邏輯放在程式其它部份。
在 while 迴圈中，加入一條 if 陳述句檢測 message 變數內的值，
如果是 'quit'，就把 active 變數設為 False，while 迴圈就會停止。
如果輸入的不是 'quit' ，就把 message 的內容輸出 

#### 使用 break 離開迴圈
不管條件檢測結果為何，使用 break 可以馬上離開 while 迴圈不再執行迴圈剩下的程式：
```python
prompt = "\nPlease enter the name of a city you have visited:"
prompt += "\n(Enter 'quit' when you are finished.) "

while True:
    city = input(prompt)

    if city == 'quit':
        break
    else:
        print("I'd love to go to " + city.title() + "!")
```
迴圈是以 while True 開始，它會不斷執行直到執行 break 陳述句時才離開：
```text
Please enter the name of a city you have visited:
(Enter 'quit' when you are finished.) New York
I'd love to go to New York!

Please enter the name of a city you have visited:
(Enter 'quit' when you are finished.) San Francisco
I'd love to go to San Francisco!

Please enter the name of a city you have visited:
(Enter 'quit' when you are finished.) quit
```

#### 在迴圈中使用 continue
與 break 不同，continue 陳述句會返回迴圈的開頭，並檢測條件再判別是否繼續執行迴圈：
```python
current_number = 0
while current_number < 10:
    current_number += 1
    if current_number % 2 == 0:
        continue

    print(current_number)
```
迴圈內的 if 陳述句會檢查 current_number 與 2 的模敗運算結果，如果為 0，就執行 if 下的 continue 陳述句，
讓 `Python` 忽略剩下的程式並跳回到 while 迴圈的開頭，如果 current_number 不能被 2 整除，就執行迴圈內剩下的程式，
`Python` 輸出這個數字：
```text
1
3
5
7
9
```

#### 避免發生無窮迴圈
每個 while 迴圈都需要有停止執行的方式，如此才不會永遠都在執行：
```python
x = 1
while x <= 5:
    print(x)
    x += 1
```
如果不小心漏了 x += 1 ，那這個迴圈就會永遠都在執行了…
每位程式設計師都有可能不小心寫出無窮迴圈，尤其是在迴圈的結束條件比較微妙時更會如此。
如果程式陷入無窮迴圈時，可按 Ctrl + C 鍵或是關閉顯示程式輸出的終端視窗。

要避刷寫出無窮迴圈的程式，一定要對每個 while 迴圈進行測試，確定是會依照您所期望的方式結束迴圈。
請確定程式中至少要有個地方會讓迴圈的條件式變成 False，或是有條 break 陳述句可執行。

---

### 使用 while 迴圈來處理串列和字典
for 迴圈對串列來說是很有效率的工具，但卻不能在 for 迴圈中修改串列，不然 `Python` 很難追蹤處理其中的項目。
想要在遍訪串列的同時又進行修改，可使用 while 迴圈來處理。
把 while 迴圈和串列與字典整合起來運用，就能蒐集、儲存並組織管理大量的輸入，隨後再進行檢視和輸出都很容易。

#### 從某個串列搬移項目到另一個串列
假設有一個串列存放網站新登錄但尚未驗證的使用者帳號，
在驗證之後要如何把它們搬移到另一個已驗證的使用者串列內呢：
```python
# Start with users that need to be verified.
# and an empty list to hold confirmed users.
unconfirmed_users = ['alice', 'brian', 'candace']
confirmed_users = []

# Verify each user until there are no more unconfirmed users.
# Move each verified user into the list of confirmed users.
while unconfirmed_users:
    current_user = unconfirmed_users.pop()

    print("Verifying user: " + current_user.title())
    confirmed_users.append(current_user)

# Display all confirmed users.
print("\nThe following users have been confirmed:")
for confirmed_user in confirmed_users:
    print(confirmed_user.title())
```
利用 while 迴圈在驗證使用者帳號時把帳號從未驗證的使用者串列中提取出來，
然後再把該帳號新增到另一個已驗證的使用者帳號串列中。

未驗證帳號的串列會隨著回圈迭代的 `pop()` 提取而愈來愈短，
而已驗證帳號的串列則會隨著迴圈迭代的 `append()` 新增而愈來愈長。

unconfirmed_users 串列中的項目都提取完後就會變成空串列，此時為 False 而結束迴圈的執行，
然後再輸出已驗證帳號的 confirmed_users 串列內容：
```text
Verifying user: Candace
Verifying user: Brian
Verifying user: Alice

The following users have been confirmed:
Candace
Brian
Alice
```

#### 刪除串列中含有某特定值的所有項目
之前介紹的使用 remove() 函式來刪除串列某特定值的項目，
然後 remove() 能順利運作是因為要刪除的串列中含有該值的項目只出現一次，
如果串列中含有某特定值要刪除的項目有很多個時，要如何處理呢：
```python
pets = ['dog', 'cat', 'dog', 'goldfish', 'cat', 'rabbit', 'cat']
print(pets)

while 'cat' in pets:
    pets.remove('cat')

print(pets)
```
若要刪除串列中所有的 'cat' 項目時，可以用一個 while 迴圈不斷執行刪除，
直到串列中不再有 'cat'值時才停止。

#### 以使用者的輸入來填入字典中
可以用 while 迴圈以任意次數的迭代提示使用者輸入資訊，每個執行迴圈都會提示詢問使用者來輸入姓名和回答。
將蒐集來的資料存放到字典內，存放的方式是名字當成鍵，而回答文字為值，兩者關聯後儲存起來：
```python
responses = {}

# Set a flag to indicate that polling is active.
polling_active = True

while polling_active:
    # Prompt for the person's name and response.
    name = input("\nWhat is your name? ")
    response = input("Which mountain would you like to climb someday? ")

    # Store the response in the dictionary.
    responses[name] = response

    # Find out if anyone else is going to take the poll.
    repeat = input("Would you like to let another person respond? (yes/ no) ")
    if repeat == 'no':
        polling_active = False

# Polling is complete. Show the results.
print("\n--- Poll Results ---")
for name, response in responses.items():
    print(name + " would like to clim " + response + ".")
```
在 while 迴圈內提示輸入名字和想爬的山，並將資訊存放在 response 字典內，
若使用者不繼續（回答 "no"），則 polling_active 會設為 False 並離開迴圈，
接著跳到最後一個程式區塊輸出結果：
```text
What is your name? Eric
Which mountain would you like to climb someday? Denali
Would you like to let another person respond? (yes/ no) yes

What is your name? Lynn
Which mountain would you like to climb someday? Devil's Thumb
Would you like to let another person respond? (yes/ no) no

--- Poll Results ---
Eric would like to clim Denali.
Lynn would like to clim Devil's Thumb.
```
