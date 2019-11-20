---
title: 變數和字串
categories: Python
tags: python, variable, string
---
### 變數的名命和使用
`Python`的變數需要遵守幾項規則，若違反這些規則會引起錯誤發生，而依照規則會使編寫出來的程式碼更易讀易懂。
1. 變數名稱只能有英文字母、數字和底線。變數名稱可以字母和底線開頭，但不能以數字開頭。
2. 變數名稱裡不能有空格，但可以用低線來做單字的分隔。
3. 避免使用`Python`的關鍵字和內鍵函式名稱來當作變數名稱（例如：print)
<!-- more -->
4. 變數名稱最好簡短又具有描述性
5. 小心使用小寫的l和大寫的O，因為它們跟1和0很像，容易搞混。

### 字串
字串(String)是一系列的字元組成，在`Python`中以引號括起來的都是字串，引號可以是單引號或雙引號。
```python
"This is a string."
'This is also a string.'
```
兩種引號運用的彈性讓我們在字串中也能放入不同的引號
```python
'I told my friend, "Python is my favorite language!"'
"The language 'Python' is named after Monty Python, not the snake."
"One of Python's strengths is its diverse and supportive community."
```

#### 使用方法變更字串的大小寫
```python
name = "charles wang"
print(name.title())
```
在`print()`的`name`變數後面出現了`title()`方法。
方法(method)是`Python`對某段資料所進行的操作，
在`name.title()`中的位在name後面句點(.)是用來告知`Python`對`name`變數進行`title()`的操作。
**`title()`方法的功用是讓字串的單字以標題首字大寫的方式呈現**
因此上面的範例輸出結果為：
```python
Charles Wang
```
也可以用其它方法來處理字串都改成大寫字母或小寫字母：
```python
name = "charles wang"
print(name.upper())
print(name.lower())
```
輸出結果為：
```text
CHARLES WANG
charles wang
```
其中`lower()`方法在儲存資料上特別有用。
大多數情況不會依靠使用者在輸入時用了正確大小寫，因此把字串都先轉換為小寫再儲存，這樣就能確保資料的一致性。
日後需要輸出顯示這些資訊時，再轉換適當的大小寫方式來顯示即可。

#### 字串的組合和連接
```python
first_name = "charles"
last_name = "wang"
full_name = first_name + last_name

print(full_name)
```
可以將名字的姓和名存放在不同的變數中，在顯示時才組合起來讓別人看到完整的名字。
`Python`是利用加號(+)組合字串，以上範例使用了`+`把`first_name`、空格和`last_name`組合成完整的名字。
輸出結果為：
```text
charles wang
```
這種組合字串的方法稱為「連接(concatenation)」。
可以利用連接的方式把存放在變數中的資訊連接起來組成完整的訊息：
```python
first_name = "charles"
last_name = "wang"
full_name = first_name + last_name

print("Hello, " + full_name.title() + "!")
```
使用完整姓名來問候，並用了`title()`方法將完整姓名設成首字大寫的格式，輸出結果為：
```text
Hello, Charles Wang!
```
也可以利用連接方式將字串訊息組合起來存放到一個變數內，這樣的方式讓`print()`陳述句變簡潔許多：
```python
first_name = "charles"
last_name = "wang"
full_name = first_name + last_name

message = "Hello, " + full_name.title() + "!"
print(message)
```

#### 使用定位符號和換行來增加空白 #
在編寫程式的過程中，空白(whitespace)是指不會印出來的各種字元，例如空格、定位符號和換行符號等。
我們可以利用空白來組織編排輸出的呈現，讓顯示的內容更容易閱讀。

若想加入定位空白到字串中，可以使用字元連接`\t`：
```python
print("Python")
Python

print("\tPython")
    Python
```

若想加入換行符號到字串中，可使用字元連接\n：
```python
print("Languages:\nPython\nC\nJavaScript")
Languages:
Python
C
JavaScript
```

也可以將定位符號和換行符號放在同字串中，`\n\t`會讓字串先換行，然後在新行開頭加入定位符號空白：
```python
print("Languages:\n\tPython\n\tC\n\tJavaScript")
Languages:
    Python
    C
    JavaScript
```
當以很少行的程式碼來產生多行輸出時，定位符號和換行符號會發揮很大功用。