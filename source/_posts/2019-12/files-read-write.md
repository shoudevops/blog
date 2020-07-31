---
title: 檔案 － 讀取與寫入
categories: Python
tags:
  - python
  - files
date: 2019-12-19 18:31:49
---

本篇要學習處理檔案，讓程式能快速分析大量資料。

### 從檔案中讀取資料
當需要分析或修改儲存在檔案中的資訊時，能讀取檔案是很有用的能力，對資料分析應用程式來說更是不可少。
我們能編寫一支程式讀取某個文字檔的內容，重新設定這些資訊的格式，然後寫入檔案內，讓瀏覽器能顯示這些內容。

<!-- more -->

當我們想要處理文字檔中的資訊，第一步是要把資訊讀取到記憶體中。
可以一次讀取整個檔案的全部內容，也可以每次一行的方式逐步讀取。

#### 讀取整個檔案
首先我們需要一個含有幾行文字的檔案。
就以一個存放小數有30位數的 pi 圓周率的文字檔為例，其中小數位數每 10 位就換一行：
```text
3.1415926535
  8979323846
  2643383279
```
下列程式為開啟並讀取這個檔案的範例，然後再將內容顯示在畫面上：
```python
with open('pi_digits.txt') as file_object:
    contents = file_object.read()
    print(contents)
```
這支程式的第一行就處理大部分的工作。
`open()` 函式，要使用檔案之前，都要先開啟檔案，然後才能存取。
`open()` 函式接收一個引數：要開啟的檔案名稱，`Python` 會在目前執行的程式檔所在的資料夾內找這個檔案。
`open()` 函式會返回一個代表檔案的物件，在 `open('pi_digits.txt')` 這行會返回代表 `pi_digits.txt` 的物件，
`Python` 會把這個物件儲存到後面所用的 file_object 變數中。

關鍵字 with 會在不需要存取檔案後將其關閉。
在這支程式我們呼叫 open() 函式，但沒有用 close() 函式關閉。
也可以同時呼叫 open() 和 close() 來開啟和關閉檔案，但萬一程式有 bug 造成還沒執行 close() 陳述句就當掉，那檔案就不會關閉。
未能正常關閉檔案可能造成資料遺失或檔案損毀。
如果程式過早呼叫 close() ，也會造成取用檔案時卻已關閉的問題（無法存取），因而引發更多錯誤。
我們不一定能掌握各種狀況而能捉準關閉檔案的時機，但使用 with 語法就能讓 `Python` 自己去負責，
我們只管開啟檔案，並在需要時取用，至於關閉的時機就讓 `Python` 幫我們搞定。

取得代表 pi_digits.txt 檔案物件，程式第二行使用 `read()` 方法讀取檔案的全部內容，並將它當成字串存放到變數 `contents` 內。
接著用 print() 將文字檔的全部內容輸出：
```text
3.1415926535
  8979323846
  2643383279

```
輸出為什麼多一行空行呢？因為 read() 到達檔案尾端時會返回一個空字串，而這個空字串的顯示也會佔用一行空行。
若要刪除尾端的空行，可在 print 陳述句中使用 `rstrip()` 處理：
```python
with open('pi_digits.txt') as file_object:
    contents = file_object.read()
    print(contents.rstrip())
```
`rstrip()` 方法會刪除或剝除字串尾端右側所有的空白。現在輸出的結果與原始檔案的內容會完全一樣。

#### 檔案路徑
依照組織管和存氓檔案的方式不同，有時要開啟的檔案並不放在程式檔所在的資料夾。
若要讓 `Python` 開啟不放在與程式檔相同資料夾內的檔案，就需要提供檔案路徑，讓 `Python` 可以依照路徑指示到該路徑內尋找檔案。
相對檔案路徑可讓 `Python` 到指定的路徑位置中尋找，而該位置是「相對」是以目前執行程式所在的資料夾作比對。
在 Linux 和 MacOS X 系統中，可以像下列這樣寫入：
```text
with open('text_files/filename.txt') as file_object:
```
在 Windows 系統中，檔案路徑用的是反斜線（ \ ）而不是斜線（ / ）：
```text
with open('text_files\filename.txt') as file_object:
```
還可以把檔案在電腦中的絕對位置路徑告知 `Python` ，這樣更不需要擔心目前執行的程式檔所在的資料夾與要開啟檔案資料夾的路徑關係，
這個精確的位置就是「絕對檔案路徑」。
絕對路徑一般都會比相對路徑長很多，因此把它存放入一個變數內，再以這個變數傳給 open() 函式是比較好的作法。
在 Linux 和 MacOS X 系統中，絕對路徑像下列這樣寫：
```text
file_path = '/home/username/other_files/text_files/filename.txt'
with open(file_path) as file_object:
```
在 Windows 系統中，其寫法為：
```text
file_path = 'C:\Users\Username\other_files\filename.txt'
with open(file_path) as file_object:
```

#### 逐行讀取
讀取檔案時常需要逐一檢查每一行讀入的內容，可能要在檔案中尋找某個特定資訊，或是要以某種方式修改檔案中的某個文字。
若想以每次一行的方式檢查檔案，可以對檔案物件以 for 迴圈遍訪：
```python
filename = 'pi_digits.txt'

with open(filename) as file_object:
    for line in file_object:
        print(line)
```
為了要檢查檔案的內容，這裡利用 for 迴圈對檔案物件進行遍訪，以逐行的方式的處理。
當逐行輸出時，會發現空白變多了：
```text
3.1415926535

  8979323846

  2643383279

```
因為在文字檔案中每行結尾都有一個看不見的換行符號，而 print 陳述句輸出後也會加上一個換行，
因此每輸出一行時末尾都有兩個換行符號，一是來自檔案本身，一個是 print 加上的。
要刪除多的空行，可在 print 陳述句內使用 `rstrip()`:
```python
filename = 'pi_digits.txt'

with open(filename) as file_object:
    for line in file_object:
        print(line.rstrip())
```
現在輸出的結果會與文件內容相符。

#### 把檔案內每一行內容存成的串列
使用關鍵字 with 時， open() 返回的檔案物件只能在 with 的程式區塊中使用，
若想要在 with 程式區塊之外存取檔案內容，可在 with 程式區塊中將檔案的每一行內容存入一個串列內，
並在 with 程式區塊外使用這個串列。
這樣可以選擇馬上處理檔案的各個部份，或是存放入串列內，待稍後再進行相關處理。

下列範例在 with 程式區塊中把 pi_digits.txt 的每一行內容存成串列，再到 with 程式區塊之外才輸出：
```python
filename = 'pi_digits.txt'

with open(filename) as file_object:
    lines = file_object.readline()

for line in lines:
    print(line.rstrip())
```
`readlines()` 方法會逐行讀取檔案內容並存成串列，然後再將串列指定存放到 lines 變數內。
在 with 程式區塊之外（檔案已關閉），我們依然可以使用這個變數。
接著使用 for 迴圈輸出 lines 變數中每一行。由於 lines 串列內的每個項目元素都對應檔案中的每一行，
因此輸出內容會和檔案內容完全一樣。

#### 處理檔案的內容
將檔案讀取到記憶體之後，就可以用任一種方式處理這些資料。
試著以簡單的方式呈現圓周率的值。
首先建立一個字串，內含檔案中存放的圓周率的完整數字，且沒有多餘空行或空格：
```python
filename = 'pi_digits.txt'

with open(filename) as file_object:
    lines = file_object.readlines()

pi_string = ''
for line in lines:
    pi_string += line.rstrip()

print(pi_string)
print(len(pi_string))
```
與前面相同，會先開啟檔案，並將其中所有行都存放到一個串列內。
再來建立 pi_string 變數，用來存放圓周率的值。
之後用 for 迴圈將各行內容都放入 pi_string 變數，並刪除每行尾端的換行符號。
最後輸出這個字串及其長度：
```text
3.1415926535  8979323846  2643383279
36
```
pi_string 變數存放的字串中含有原本位在檔案中每左側的空格，若要刪除可使用 strip()：
```python
filename = 'pi_digits.txt'

with open(filename) as file_object:
    lines = file_object.readlines()

pi_string = ''
for line in lines:
    pi_string += line.strip()

print(pi_string)
print(len(pi_string))
```
如此得到的字串就是個含有精準度到小數30位數的圓周率數值：
```text
3.141592653589793238462643383279
32
```
字串的長度是32個字元，因為包括前面的 3 和小數點。

*讀取文字檔時，Python 會將其中所有文字都解讀為字串，*
*如果要將其當成「數值」型別使用，就必須使用 int() 函數或是 float() 函式轉換。*

#### 大型檔案：含有一百萬位數
假如有個文字檔，內含有精準到小數點後 1,000,000 位數，也能用程式建立一個完整呈現這個圓周率數字的字串。
小數點後百萬位數圓周率檔案：{% asset_link pi_million_digits.txt.zip 下載 %}

不需要修改前面的程式碼，只需把這個檔案傳入即可。
在這裡只輸出到小數位數 50 位，以免終端視窗為顯示全部一百萬位數而不斷翻頁：
```python
filename = 'pi_million_digits.txt'

with open(filename) as file_object:
    lines = file_object.readlines()

pi_string = ''
for line in lines:
    pi_string += line.strip()

print(pi_string[:52] + "...")
print(len(pi_string))
```
從輸出結果來看，建立的字串確實含有精準到小數點後一百萬位數的圓周率數值：
```text
3.14159265358979323846264338327950288419716939937510...
1000002
```
`Python` 沒有限制我們能處理的資料量，只要系統的記憶體夠，想處理多少就處理多少。

#### 圓周率數值中含有您的生日嗎？
想知道自己的生日是否有在圓周率的數值內嗎？
來擴充前面剛寫好的程式，以確定某個人的生日是否有在圓周率的前一百萬位數中：
```python
filename = 'pi_million_digits.txt'

with open(filename) as file_object:
    lines = file_object.readlines()

pi_string = ''
for line in lines:
    pi_string += line.rstrip()

birthday = input("Enter your birthday, in the form mmddyy:")
if birthday in pi_string:
    print("Your birthday appears in the first million digits of pi!")
else:
    print("Your birthday does not appear in the first million digits of pi.")
```
作法是把生日變成一組數字的字串，再檢查這個字串是否包含在 pi_string 中，
並提供使用者輸入生日數字，再檢測這個字串是否有在 pi_string 中，結果如下：
```text
Enter your birthday, in the form mmddyy:061078
Your birthday appears in the first million digits of pi!
```
讀取檔案的內容後，我們可用任何想到的方式來進行分析處理。

---

### 寫入檔案
儲存資料最簡單的方式之一就是把資料寫入檔案之中。
這樣就算關閉顯示程式輸出的終端視窗，輸丑的結果仍然保存著，
還能在程式結束執行之後查閱輸出的內容，或與別人分享這個輸出，
還可編寫程式將輸出內容讀取到記憶體中進行其它處理。

#### 寫入空檔案
要把文字寫入檔案中，在呼叫 open() 時要提供一個引數，告知 `Python` 要寫入開啟的檔案。
我們來寫入一條簡單的文字訊息，儲存到檔案之中，而不是輸出到畫面：
```python
filename = 'programming.txt'

with open(filename, 'w') as file_object:
    file_object.write("I love programming.")
```
呼叫 open() 時放入兩個引數，第一個是要開啟的檔名，第二個引數 'w' 是告知 `Python` 要以寫入模式開啟檔案。
開啟檔案時可指定是：
- 讀取模式（ 'r' ）
- 寫入模式（ 'w' ）
- 附加模式（ 'a' ）
- 讀寫模式（ 'r+' ）
如果省略這個引數， `Python` 預設是以讀取模式開啟檔案。
要寫入的檔案不存在時， open() 函式會自動建立，不過以寫入模式（ 'w' ）開啟檔案時要非常小心，
因為如果指定的檔案已存在， `Python` 會在返回檔案物件前清空這個檔案。
使用檔案物件的 `write()` 方法把字串寫入檔案中，程式不會在終端視窗中顯示輸出，但如果開啟 programming.txt，
就會看到下列文字：
```text
I love programming.
```
與電腦中其它的檔案相比，這個檔案沒有什麼不同，我們可以進行開啟、在其中輸入文字、複製內容、內容貼上等處理。

#### 寫入多行內容
write() 函式不會在寫入文字結尾處加入換行符號，所以當寫入多行內容時，
若沒有指定換行符號，檔案內容看起來可能不是想像中的樣貌：
```python
filename = 'programming.txt'

with open(filename, 'w') as file_object:
    file_object.write("I love programming.")
    file_object.write("I love creating new games.")
```
開啟 programming.txt 檔，就會發現兩行內容是連在一起的：
```text
I love programming.I love creating new games.
```
要讓每個字串單獨佔一行，要在 write() 陳述句中也加入換行符號：
```python
filename = 'programming.txt'

with open(filename, 'w') as file_object:
    file_object.write("I love programming.\n")
    file_object.write("I love creating new games.\n")
```
現在輸出的檔案呈現會是兩行文字：
```text
I love programming.
I love creating new games.
```
像顯示在畫面上的輸出一樣，還可以使用空格、定位符號和換行符號來設定這些輸出的內容。

#### 附加到檔案後面
要在檔案後面加上內容，而不是覆蓋原有的內容時，可以用附加模式（'a'）來開啟檔案。
以附加模式開啟檔案時， `Python` 不會在返回檔案省件前清空檔案，而寫入到檔案的內容都會新增到檔案尾端。
假如指定的檔案不存在， `Python` 會建立一個空的檔案。

接著來修改程式內容，將現有的 programming.txt 中再附加入一些喜歡程式設計的原因：
```python
filename = 'programming.txt'

with open(filename, 'a') as file_object:
    file_object.write("I also love finding meaning in large datasets.\n")
    file_object.write("I love creating apps that can run in a browser.\n")
```
以附加模式 'a' 當引數開啟檔案，以便將內容新增在檔案的尾端，而不是覆蓋原來內容。
在 with 程式內縮區塊是寫入二行文字，它們是被新增到 programming.txt 檔的尾端：
```text
I love programming.
I love creating new games.
I also love finding meaning in large datasets.
I love creating apps that can run in a browser.
```
最後的結果是檔案原來的內容還在，在其後面新增了兩行內容。