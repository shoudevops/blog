---
title: 例外
categories: Python
tags:
  - python
  - exception
date: 2019-12-26 14:31:11
---

本篇會學習對出現錯誤時的處理，避免程式在面對例外時當掉。
我們將學習和認識例外這個 `Python` 所建立的特殊的物件，可用來管理程式執行時出現的錯誤。

學習處理例外可協助在出現「檔案不存在」的問題時做出適當的反應，與處理其它可能引起程式當掉的問題。
這能讓我們的程式在面對錯誤的資料時更強健，不管這些錯誤的資料是因為無意的錯誤，
還是惡意想破壞程式的企圖，有了例外的處理就能應對這些錯誤。

<!-- more -->

### 例外
`Python` 使用稱為「例外（exception）」的特殊物件來管理程式執行時期所產生的錯誤。
每當發生錯誤 `Python` 不知要怎麼處理時，就會建立一個例外物件。
如果編寫了處理此例外的程式碼，程式就能繼續依照例外處理來執行，
如果未有對例外進行處理，那麼程式就會停止，並顯示 traceback 錯誤訊息，其中含有關於例外的說明。

#### 處理 ZeroDivisionError 例外
您可能知道某個數字是不能除以 0 的，但還是讓 `Python` 進行這樣的處理：
```python
print(5/0)
```
當然 `Python` 沒辦法這樣運算，因此會看到一個 traceback 錯誤回報：
```text
Traceback (most recent call last):
  File "division.py", line 1, in <module>
    print(5/0)
ZeroDivisionError: division by zero
```
在 traceback 訊息的最後一行指出錯誤為 `ZeroDivisionError` ，這是種例外物件。
`Python` 無法依照我們的要求來處理時，就會建立這種物件。
在這種情況下 `Python` 會停止執行，並指出發生了哪種例外，而我們可依據這些資訊對程式進行修改。
當例外發生時，我們可告訴 `Python` 該進行什麼樣的處置，如此在錯誤發生時，就有處理準備了。

#### 使用 try-except 程式區塊
例外是使用 try-except 程式區塊來處理的，try-except 程式區塊可讓 `Python` 依照指示執行，
同時告知 `Python` 發生例外時要怎麼處理。

使用 try-except 程式區塊時，就算出現例外，程式也能繼續執行，
可顯示我們編寫較為好懂友善的錯誤訊息，而不是丟出讓使用者看不太懂的 traceback。

當您認為可能有錯誤發生時，可編寫一個 try-except 程式區塊來處理可能引發的例外。
可讓 `Python` 去執行某些程式，並告知如果這程式引發了某個特別的例外時，要做什麼樣的處置。

以下列出處理 ZeroDivisionError 例外的 try-except 程式碼區塊：
```python
try:
    print(5/0)
except ZeroDivisionError:
    print("You can't divide by zero!")
```
將會引發錯誤的程式碼 `print(5/0)` 放在 try 區塊內，如果 try 區塊中的程式執行時沒問題，`Python` 就會跳過 except 區塊。
如果 try 區塊中的程式碼引發錯誤，`Python`就會檢測 except 區塊是否為這種錯誤，並執行其中的程式碼。

這樣使用者端會看到一條我們寫的友善錯誤文字訊息，而不是 traceback：
```text
You can't divide by zero!
```
假如 try-except 程式區塊後面還有程式碼，這樣程式會接著執行，因為已告知 `Python` 如何處理錯誤了。

#### 使用例外避免程式當掉
發生錯誤時，假如程式還有工作沒完成，那麼好好處理錯誤就十分重要。
這種情況常出現在要求使用者輸入資料的程式中。
如果程式能好好處理無效的輸入，就能再提示使用者輸入有效合法的內容，而不會讓程式當掉。

以下是一個只執行除法運算的簡單計算機程式：
```python
print("Give me two numbers, and I'll divide them.")
print("Enter 'q' to quit.")

while True:
    first_number = input("\nFirst number: ")
    if first_number == 'q':
        break
    second_number = input("Second number: ")
    if second_number == 'q':
        break
    answer = int(first_number) / int(second_number)
    print(answer)
```
在 while 迴圈內程式會提示使用者輸入兩個數字，分別存入 first_number 與 second_number 變數內。
如果使用者輸入的是 q，就會離開程式，接著將兩個變數由字串轉換成整數型別，並計算兩個數字相除，算出的數字會存放到 answer 變數。
這支程式沒有使用錯誤處理的機制，因此當它執行到除數為 0 時，就會當掉並顯示 traceback：
```text
First number: 5
Second number: 0
Traceback (most recent call last):
  File "division.py", line 11, in <module>
    answer = int(first_number) / int(second_number)
ZeroDivisionError: division by zero
```
程式當掉不太好，但讓使用者看到 traceback 訊息也不太秒。
不懂技術的使用者會被這些訊息搞混，而且萬一使用者懷有惡意，他能從 traceback 訊息中獲取不希望讓使用者知道的訊息，
他會知道您的程式檔名，還會看到部份不能正確執行的程式碼。
有技術底的攻擊者有時候能利用這些訊息來確定對程式碼使用哪種攻擊最有效。

#### else 程式碼區塊
我們把可能引起錯誤的程式碼放入 try-except 程式區塊中，這樣能提高程式抵抗錯誤的因應能力。
錯誤是執行除法運算時引起的，因此我們要把這程式放入 try-except 區塊內。
下列範例含有 else 程式碼區塊，當 try 區塊內的程式都成功執行，else 區塊內的程式就會執行：
```python
print("Give me two numbers, and I'll divide them.")
print("Enter 'q' to quit.")

while True:
    first_number = input("\nFirst number: ")
    if first_number == 'q':
        break
    second_number = input("Second number: ")
    if second_number == 'q':
        break
    try:
        answer = int(first_number) / int(second_number)
    except ZeroDivisionError:
        print("You can't divide by 0!")
    else:
        print(answer)
```
讓 `Python` 試著執行 try 程式碼區塊中的除法運算，這個區塊只含有可能引起錯誤的程式碼，
要在 try 區塊都成功執行後才會執行的程式碼是放在 else 程式碼區塊內。

except 程式碼區塊則是告知 `Python` 當出現 ZeroDivisionError 例外時才要執行的處置，
如果 try 程式碼區塊中的除法運算因除以 0 的錯誤而失敗，就會執行 except 區塊中的程式，
輸出一條較友善的文字訊息，告訴使用者錯誤的原因及避免方法。
程式隨後再繼續執行，使用者是看不到 traceback 的：
```text
Give me two numbers, and I'll divide them.
Enter 'q' to quit.

First number: 5
Second number: 0
You can't divide by 0!

First number: 5
Second number: 2
2.5

First number: q
```
try-except-else 程式碼區塊的運作原理大致如下：
1. `Python` 試著執行 try 區塊中的程式碼，只有可能引起例外的程式碼才需要放入 try 區塊內。
2. 若有些程式是在 try 區塊的程式成功執行無誤後才要執行的，這些程式就放入 else 區塊內。
3. `Python` 在試著執行 tr益區塊中的程式引發了指定的例外時，except 區塊中放置的是要處理的程式碼。

藉由預測可能引起錯誤的程式碼，我們可編寫出更強固的程式，就算在配對無效不合法的資料或是資源不足時，
也都能處置得當繼續執行，因此能抵抗使用者無意或惡意的輸入或攻擊。

#### 處理 FileNotFoundError 例外
使用檔案時有一種常見的錯誤是找不到檔案，要用的檔案可能在其它路徑，也可能檔名打錯或這個檔案根本不存在。
這些狀況我們都可以用 try-except 程式區塊以直接的方式進行處理。

試著讀取一個不存在的檔案，下列程式會讀取 alice.txt 檔案，但我們並沒在這個文字檔：
```python
filename = 'alice.txt'

with open(filename) as f_obj:
    contents = f_obj.read()
```
執行時 `Python` 找不到要讀取的文字檔，因此引發一個例外：
```text
Traceback (most recent call last):
  File "alice.py", line 3, in <module>
    with open(filename) as f_obj:
FileNotFoundError: [Errno 2] No such file or directory: 'alice.txt'
```
在上述的 traceback 中，最後一行列出 FileNotFoundError 例外，
這是 `Python` 找不到要開啟的檔案所引發的例外。
這個範例中，錯誤是由 open() 函式所引起，因此要處理這個錯誤，就必須把使用到 open() 的程式放入 try 區塊之中：
```python
filename = 'alice.txt'

try:
    with open(filename) as f_obj:
        contents = f_obj.read()
except FileNotFoundError:
    msg = "Sorry, the file " + filename + " does not exist."
    print(msg)
```
如果出現 FileNotFoundError 錯誤，會輸出一條較友善的文字訊息，而不是顯示 traceback:
```python
Sorry, the file alice.txt does not exist.
```
假如檔案不存在，那麼程式就什麼都不用做，因此錯誤側理的程式就意義不大。
下面會繼續擴充這個範例，看看使用多個檔案時，例外處理能幫上什麼忙。

#### 分析文字
很多文學作品都是用簡單的純文字檔格式儲存，因為這些作品已經沒有版權問題，不受版權限制。
這裡使用的文字是取自於 Gutenberg （古騰堡計劃，http://gutenberg.org/），
這個計劃專案的網站中提供了一系列可自由使用、沒有版權問題。

讓我們來試著計算「Dracula」這部作品文字檔中的單字數量有幾個。
這裡會使用 `split()` 方法，此方法會從字串來建立一個單字串列。
`split()` 方法會以空格為分隔符號來把字串分拆成獨立項目，並把這些項目存到一個串列中。
這個結果是一個含有該字串所有單字的串列，這種分拆法會讓有些單字含有逗號。
現在要計算「Dracula」這部作品到底含有多少單字，因此對整篇小說呼叫 `split()` 方法，
然後再計算取得的串列含有多少個項目元素，就能算出這部作品有多少單字了：
```python
filename = 'Dracula.txt'

try:
    with open(filename) as f_obj:
        contents = f_obj.read()
except FileNotFoundError:
    msg = "Sorry, the file " + filename + " does not exist."
    print(msg)
else:
    # Count the approximate number of words in the file.
    words = contents.split()
    num_words = len(words)
    print("The file " + filename + " has about " + str(num_words) + " words.")
```
在 else 程式區塊，先對 contents 變數（目前存放很長的字串，是 Dracula 這部作品全部內容）呼叫 split() 方法，
生成一個串列，內含這部作品中所有的單字。當使用 len() 來求出串列長度時，就知道字串中含有多少個單字了：
```text
The file Dracula.txt has about 164424 words.
```

#### 處理多個檔案
接著加入更多對書籍的分析處理。再進行之前，先把這支程式的大部份內容移動到取名為 count_words() 函數中。
這樣對多本書籍進行分析時會更容易：
```python
ef count_words(filename):
    """Count the approximate number of words in a file."""

    try:
        with open(filename) as f_obj:
            contents = f_obj.read()
    except FileNotFoundError:
        msg = "Sorry, the file " + filename + " does not exist."
        print(msg)
    else:
        # Count the approximate number of words in the file.
        words = contents.split()
        num_words = len(words)
        print("The file " + filename + " has about " + str(num_words) + " words.")


filename = 'Dracula.txt'
count_words(filename)
```
現在可以寫一個簡單的迴圈，用來處理計算分析多個文字檔到底含有多少個單字。
把要分析的檔案名稱都存放入一個串列內，然後以迴圖遍訪串列中每個檔案，
並呼叫 count_word() 函式來處理。
假設先在要分析 Dracula、Siddhartha、Moby Dick、Little Women 等作品，
看看他們有多少個單字，這些作品都是版權沒問題可以取用的。
我們會故意沒有把 little_women.txt 放入 word_count.py 所在的資料夾內，
看看這支程式在處理找不到檔案是回應是如何：
```python
def count_words(filename):
    """Count the approximate number of words in a file."""

    try:
        with open(filename) as f_obj:
            contents = f_obj.read()
    except FileNotFoundError:
        msg = "Sorry, the file " + filename + " does not exist."
        print(msg)
    else:
        # Count the approximate number of words in the file.
        words = contents.split()
        num_words = len(words)
        print("The file " + filename + " has about " + str(num_words) + " words.")


filenames = ['Dracula.txt', 'siddhartha.txt', 'little_women.txt', 'moby_dick.txt']
for filename in filenames:
    count_words(filename)
```
就算 little_women.txt 檔不存在，也不受影響的處理分析其它檔案：
```text
The file Dracula.txt has about 164424 words.
The file siddhartha.txt has about 42166 words.
Sorry, the file little_women.txt does not exist.
The file moby_dick.txt has about 215830 words.
```
這個範例中使用 try-except 程式區塊有兩個優點：
+ 避免讓使用者看到 traceback 訊息
+ 讓程式能繼續分析其它找得到的檔案

#### 出錯時無聲無息
在前一個範例中，我們告知使用者有個檔案找不到，但並不是每次捉取到例外時都需要告知使用者，
有時候只希望程式在發生例外時無聲無息繼續執行。
可以像平常一樣編寫 try 程式碼區塊，但在 except 程式碼區塊中明確告知 `Python` 什麼都不做，
`Python` 有一條 pass 陳述句，可在程式碼區塊中寫入，`Python` 就會無聲無息地跳過：
```python
def count_words(filename):
    """Count the approximate number of words in a file."""

    try:
        with open(filename) as f_obj:
            contents = f_obj.read()
    except FileNotFoundError:
        pass
    else:
        # Count the approximate number of words in the file.
        words = contents.split()
        num_words = len(words)
        print("The file " + filename + " has about " + str(num_words) + " words.")


filenames = ['Dracula.txt', 'siddhartha.txt', 'little_women.txt', 'moby_dick.txt']
for filename in filenames:
    count_words(filename)
```
不同的地方在於 except 區塊內的 pass 陳述句。
當程式執行出現 FileNotFoundError 例外時，就會執行 except 區塊內的 pass 陳述句。
這種錯誤發生時也不會出現 trackback ，也沒有輸出，無聲無息。
使用者只會看到有存在的檔案算出有多少個單字，但沒有顯示其中有個檔案不存在的訊息：
```text
The file Dracula.txt has about 164424 words.
The file siddhartha.txt has about 42166 words.
The file moby_dick.txt has about 215830 words.
```
pass 陳述句也充當了佔位符號，提醒我們在程式的某個位置什麼都錯，
保留位置讓我們將來在這裡可以再進行些什麼處理。

#### 決定回報哪些錯誤訊息
如果使用者知道要分析哪些檔案，則可能希望在檔案沒有被分析時顯示一條訊息，將原因告知。
如果使用者只想看到結果，並不想知道分析了哪些檔案，則無需把哪些檔案不存在的訊息顯示出來。
向使用者顯示他們不想看到的訊息可能會降低程式的可用性。

編寫得很好並經過詳細測試的程式碼不容易出現內部錯誤，但只要程式要依靠外部的因素，
如使用者輸入、存放在資料夾的檔案、網外連接等，就有可能出現例外。
藉由經驗的判斷可讓程式在什麼位置放入例外處理的程式區塊，以及出錯時要給使用者多少相關的訊息。