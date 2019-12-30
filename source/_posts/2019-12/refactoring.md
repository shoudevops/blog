---
title: 重構
categories: Python
tags:
  - python
  - refactoring
date: 2019-12-30 16:07:59
---

### 重構
我們可能常碰到程式雖然能正確執行，但還想要再進一步改進修調，
把程式劃分成一系列能完成某些紟定工作的函式，這樣的過程就稱為重構（refactoring）。
重構能讓程式碼變得更清晰、更易讀好懂、更容易擴充。

<!-- more -->

若想要重構程式，可將其中大部份的邏輯處理放到一個函式內。
下面的範例重點在問候使用者，因此我們把所有程式碼都放入名為 greet_user() 函式中：
```python
import json

def greet_user():
    """Greet the user by name."""
    filename = 'username.json'
    try:
        with open(filename) as f_obj:
            username = json.load(f_obj)
    except FileNotFoundError:
        username = input("What is your name? ")
        with open(filename, 'w') as f_obj:
            json.dump(username, f_obj)
            print("We'll remember you when you come back, " + username + "!")
    else:
        print("Welcome back, " + username + "!")


greet_user()
```
greet_user() 函式不只是問候使用者而已，還能用儲存了使用者名字時擷取它來用，
並在沒有儲存使用者名字時提示使用者輸入一個。

接著再來重構 greet_user() ，讓一個函式不要執行那麼多項工作。
我們先把取得使用者名字的程式移到另一個函式內：
```python
import json

def get_stored_username():
    """Get stroed username if available."""
    filename = 'username.json'
    try:
        with open(filename) as f_obj:
            username = json.load(f_obj)
    except FileNotFoundError:
        return None
    else:
        return username

def greet_user():
    """Greet the user by name."""
    username = get_stored_username()
    if username:
        print("Welcome back, " + username + "!")
    else:
        username = input("What is your name? ")
        filename = 'username.json'
        with open(filename, 'w') as f_obj:
            json.dump(username, f_obj)
            print("We'll remember you when you come back, " + username + "!")

greet_user()
```
新增一個 get_stored_username() 函式，如果儲存了使用者名稱，此函式就能擷取並返回。
如果 username.json 檔案不存在，此函式會返回 None。
這樣能讓我們尸用函式的返回值來進行簡單的檢測。

在 greet_user() 函式，如果成功取得使用者名字，就輸出一條歡迎使用者回來的訊息，
不然就提示要求使用者輸入名字。

我們還要把 greet_user() 中的另一組程式碼擷取出來，
那就是沒有儲存使用者名字時提示使用者輸入的程式碼，
把它們都放入一個單獨的函式內：
```python
import json

def get_stored_username():
    """Get stroed username if available."""
    filename = 'username.json'
    try:
        with open(filename) as f_obj:
            username = json.load(f_obj)
    except FileNotFoundError:
        return None
    else:
        return username

def get_new_username():
    """Prompt for a new username."""
    username = input("What is your name? ")
    filename = 'username.json'
    with open(filename, 'w') as f_obj:
        json.dump(username, f_obj)
    return username

def greet_user():
    """Greet the user by name."""
    username = get_stored_username()
    if username:
        print("Welcome back, " + username + "!")
    else:
        username = get_new_username()
        print("We'll remember you when you come back, " + username + "!")

greet_user()
```
在重構的最終版本內，每個函式都單獨處理一件清楚的工作，
我們呼叫 greet_user() 就會輸出一條適當的訊息，是歡迎使用者回來，或是問候新的使用者。

處理上它會先呼叫 get_stored_username() 函式，此函式只負責取得儲存的使用者名字（如果已儲存了），
若有必要時呼叫 get_new_username() 函式，此函式則只負責取得並儲存新使用者的名字。

想要設計編寫出清楚又易維護和擴充的程式碼，這種重構劃分的工作是不能少的。