---
title: 使用者輸入
categories: Python
tags: python, input
---
大多數的程式製作出來的目的就是為了解決終端使用者的問題，要達到這個目的，通常需要從使用者那裡取得一些資訊。
本篇將學習如何接收使用者的輸入，讓程式能進行其它處理。
若在程式中需要名字時，就提示輸入名字，若需要一份名單時，就提示輸入一系列名字。
這些輸入的運用都要透過 input() 函式來達成。

<!-- more -->

### input() 函式的工作原理
input() 函式會讓程式暫停，等待使用者輸入一些文字。
`Python` 在取得使用者輸入的文字後，會把這些文字存放到一個變數內以方便運用：
```python
message = input("Tell me something, and I will repeat it back to you: ")
print(message)
```
input() 函式中可放入一個引數，此引數為向使用者顯示的文字說明，讓使用者知道要做什麼：
```text
Tell me something, and I will repeat it back to you: Hello everyone!
Hello everyone!
```

#### 編寫清楚的提示
每次在使用 input() 函式時，最好都提供清楚易懂的提示，精確告知使用者您希望他們輸入什麼資訊：
```python
name = input("Please enter your name: ")
print("Hello, " + name + "!")
```
可將提示文字和使用者要輸入的內容分隔開，讓使用者清楚知道其輸入的內容是從哪裡開始：
```text
Please enter your name: Eric
Hello, Eric!
```
有時提示的文字可能會超過一行，這些很長的文字可以存放在一個變數內，再把此變數當成 input()的引數：
```python
prompt = "If you tell us who you are, we can personalize the messages you see."
prompt += "\nWhat is your first name? "
name = input(prompt)
print("\nHello, " + name + "!")
```
第一行程式把訊息文字前半部存放在 prompt 變數內，而第二行程式則用 += 運算子在 prompt 變數後新連接上其它字串，
並在問號後多加一格空白，讓提示與輸入清楚分隔開來：
```text
If you tell us who you are, we can personalize the messages you see.
What is your first name? Eric

Hello, Eric!
```

#### 使用 int() 來取得數值的輸入
使用 input()函式時 `Python` 會從使用者所取得的輸入是「字串」：
```text
>>> age = input("How old are you? ")
How old are you? 21
>>> age
'21'
```
使用者輸入的是數值21，但 `Python` 把存放在 age 變數中的值取出時，返回的是 '21'，因為輸入的數值是以字串型別來存放。
若想要把輸入的內容當成數字來運算，就會引發錯誤：
```text
>>> age = input("How old are you? ")
How old are you? 21
>>> age >= 18
Traceback (most recent call last):
  File "<pyshell#2>", line 1, in <module>
    age >= 18
TypeError: '>=' not supported between instances of 'str' and 'int'
```
`Python`會顯示錯誤訊息，因為它不能用字串來和整數進行比較，
要使用 int()函式來解決這個問題，告訴 `Python` 把字串轉換成數值：
```text
>>> age = input("How old are you? ")
How old are you? 21
>>> age = int(age)
>>> age >= 18
True
```
在實際的程式使用 int() 函式要如何做呢？
用一個判別某個人是否能坐雲霄飛車的身高要求：
```python
height = input("How tall are you, in inches? ")
height = int(height)

if height >= 36:
    print("\nYou're tall enough to ride!")
else:
    print("\nYou'll be able to ride when you're a little older.")
```
這支程式可以讓 height 和 36 進行比較運算，如果輸入的數字大於36，會告知使用者身高多高，可以坐雲霄飛車：
```text
How tall are you, in inches? 71

You're tall enough to ride!
```
輸入的數字要用來進行數學運算和比較運算之前，記得先要轉換成數值型別。

#### 模數運算子
模數運算子（ % ）是處理數值資訊的好用工具，它會把兩個數字相除並返回餘數：
```text
>>> 4 % 3
1
>>> 5 % 3
2
>>> 6 % 3
0
>>> 7 % 3
1
```
模數運算子不會算出某個數是另一個數的幾倍，它只會求出餘數是多少。
如果某個數能被另一個數整除，則餘數為 0，因此模數運算子會返回 0。
我們可以利用這一點來判別某個數是奇數或偶數：
```python
number = input("Enter a number, and I'll tell you if it's even or odd: ")
number = int(number)

if number % 2 == 0:
    print("\nThe number " + str(number) + " is even.")
else:
    print("\nThe number " + str(number) + " is odd.")
```
偶數能被 2 整除，因此如果某數字和 2 進行模數運算的結果為 0，那麼這個數字就是偶數，若不是則為奇數：
```text
Enter a number, and I'll tell you if it's even or odd: 42

The number 42 is even.
```
