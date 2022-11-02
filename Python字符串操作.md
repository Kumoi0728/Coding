[toc]

# 分割类
## Slicing
slicing切片，按照一定条件从列表或者元组中**取出部分元素**（比如特定范围、索引、分割值）
```py
str[start:end:step]
```
- 包含start**不包含end**。
- 
- step表示隔step-1。step为负值, 开始索引默认为-1，结束索引默认为开始（不能认为是0,也不能认为是-1）
```python
s = '   hello   '
s = s[:]

print(s)
#    hello
```

```python
s = '   hello   '
s = s[3:8]

print(s)
# hello
# 不包括第8位
```

## 按长度分割
内包列表，将s分割为长度为k的子串。
注意range按k增加。
```py
def cut(s,k):
    subs=[s[i:i+k] for i in range(0,len(s),k)]
```

## split()
对字符串做**分隔**处理，最终的结果是一个**列表**。当不指定分隔符时，默认按空格分隔。
```python
s = 'string methods in python'.split()

print(s)
# ['string', 'methods', 'in', 'python']


s = 'string methods in python'.split(',')

print(s)
# ['string methods in python']
```

此外，还可以通过`maxsplit`指定字符串的分隔次数。
```python
s = 'string methods in python'.split(' ', maxsplit=1)

print(s)
# ['string', 'methods in python']
```

## rsplit()
从右侧开始对字符串进行分隔。
```python
s = 'string methods in python'.rsplit(' ', maxsplit=1)

print(s)
# ['string methods in', 'python']
```

# 合并为字符串类
## join()
`string.join(list)`。以`string`作为分隔符，将`list`中所有的元素(的字符串表示)**合并**为一个新的字符串。
```python
list_of_strings = ['string', 'methods', 'in', 'python']
s = '-'.join(list_of_strings)

print(s)
# string-methods-in-python
```

## 直接 +
不推荐！因为在 Python 中字符串是「不可变对象」，**每次字符串拼接都会生成一个新字符串，效率低下**。

## 使用列表
**先append，最后一步再拼接为字符串**，因此只需要一次拼接操作。




# 改变内容类
## replace()
把字符串中的内容**替换**成指定的内容。
```py
s = 'string methods in python'.replace(' ', '-')

print(s)
# string-methods-in-python
```
```py
s = 'string methods in python'.replace(' ', '')

print(s)
# stringmethodsinpython
```

## re.sub()
`re`是正则的表达式，`sub`是substitute表示替换。`re.sub`则是相对复杂点的替换。
```python
import re

s = "string    methods in python"
s2 = s.replace(' ', '-')
print(s2)
# string----methods-in-python


s = "string    methods in python"
s2 = re.sub("\s+", "-", s)
print(s2)
# string-methods-in-python
```

## upper()
将字符串中的字母，**全部转换为大写**。
```python
s = 'simple is better than complex'.upper()

print(s)
# SIMPLE IS BETTER THAN COMPLEX
```

## lower()
将字符串中的字母，**全部转换为小写**。
```python
s = 'SIMPLE IS BETTER THAN COMPLEX'.lower()

print(s)
# simple is better than complex
```

## capitalize()
将字符串中的**首字母转换为大写**。
```python
s = 'simple is better than complex'.capitalize()

print(s)
# Simple is better than complex
```

## swapcase()
将字符串中大小写转换。
```py
str = "abCDE--RuNOob!!!"

print ( str.swapcase() )
# ABcde--rUnoOB!!!
```

## strip()
`strip()`方法用于**移除字符串头尾指定的字符**（默认为空格或换行符）或字符序列。

```python
s = '   hello   '.strip()

print(s)
# hello
```
```py
s = '###hello###'.strip('#')

print(s)
# hello
```

此外**当指定内容不在头尾处时，并不会被去除**。

例如，第一个`\n`前有个空格，所以只会去取尾部的换行符：
```python
s = ' \n \t hello\n'.strip('\n')

print(s)
#
#      hello
```

```python
s = '\n \t hello\n'.strip('\n')

print(s)
#      hello
```

`strip()`方法的参数是**剥离其值的所有组合**，最外层的首字符和尾字符参数值将从字符串中剥离。字符从前端移除，直到到达一个不包含在字符集中的字符串字符为止。在尾部也会发生类似的动作。

```python
s = 'www.baidu.com'.strip('cmow.')

print(s)
# baidu
```

## lstrip()
**移除**字符串**左侧**指定的字符（默认为空格或换行符）或字符序列。

```python
s = '   hello   '.lstrip()

print(s)
# hello
```

同样的，可以移除左侧所有包含在字符集中的字符串。

```python
s = 'Arthur: three!'.lstrip('Arthur: ')

print(s)
# ee!
```

## rstrip()
**移除**字符串**右侧**指定的字符（默认为空格或换行符）或字符序列。

```python
s = '   hello   '.rstrip()

print(s)
#    hello
```

## removeprefix()
Python3.9中**移除前缀**的函数。和strip()相比，并不会把字符集中的字符串进行逐个匹配。

```python
# python 3.9
s = 'Arthur: three!'.removeprefix('Arthur: ')

print(s)
# three!
```

## removesuffix()
Python3.9中移除后缀的函数。

```python
s = 'HelloPython'.removesuffix('Python')

print(s)
# Hello
```

# 判断类
## islower()
**判断**字符串中的所有字母**是否都为小写**，是则返回`True`，否则返回`False`。
```py
print('SIMPLE IS BETTER THAN COMPLEX'.islower()) # False

print('simple is better than complex'.islower()) # True
```

## isupper()
**判断**字符串中的所有字母**是否都为大写**，是则返回`True`，否则返回`False`。
```py
print('SIMPLE IS BETTER THAN COMPLEX'.isupper()) # True

print('SIMPLE IS BETTER THAN complex'.isupper()) # False
```

## isalpha()
如果字符串**至少有一个字符并且所有字符都是字母**，则返回 `True`，否则返回 `False`。
```python
s = 'python'
print(s.isalpha())
# True

s = '123'
print(s.isalpha())
# False

s = 'python123'
print(s.isalpha())
# False

s = 'python-123'
print(s.isalpha())
# False
```

## isnumeric()
如果字符串中**只包含数字字符**，则返回 `True`，否则返回 `False`。
```python
s = 'python'
print(s.isnumeric())
# False

s = '123'
print(s.isnumeric())
# True

s = 'python123'
print(s.isnumeric())
# False

s = 'python-123'
print(s.isnumeric())
# False
```

## isalnum()
如果字符串中**至少有一个字符并且所有字符都是字母或数字**，则返回`True`，否则返回 `False`。
```python
s = 'python'
print(s.isalnum())
# True

s = '123'
print(s.isalnum())
# True

s = 'python123'
print(s.isalnum())
# True

s = 'python-123'
print(s.isalnum())
# False
```

# 检测类
## count()
返回**指定内容**在字符串中**出现的次数**。
```python
n = 'hello world'.count('o')
print(n) # 2

n = 'hello world'.count('oo')
print(n) # 0
```

## find()
**从左开始**检测**指定内容是否包含在字符串中**，如果是**返回开始的索引值**，否则返回`-1`。
```python
s = 'Machine Learning'
idx = s.find('a')

print(idx) # 1
print(s[idx:]) # achine Learning
```
```py
s = 'Machine Learning'
idx = s.find('aa')

print(idx) # -1
print(s[idx:]) # g
```
此外，还可以指定开始的范围。
```py
s = 'Machine Learning'
idx = s.find('a', 2)

print(idx) # 10
print(s[idx:]) # arning
```

## rfind()
类似于`find()`函数，返回字符串**最后一次出现的位置（相当于从右开始第一次出现位置）**，如果没有匹配项则返回 `-1`。
```python
s = 'Machine Learning'
idx = s.rfind('a')

print(idx) # 10
print(s[idx:]) # arning
```
## partition()
`string.partition(str)`，有点像`find()`和`split()`的结合。

从`str`出现的第一个位置起,把字符串`string`分成一个3元素的元组`(string_pre_str, str, string_post_str)`.
```python
s = 'Python is awesome!'
parts = s.partition('is')
print(parts)
# ('Python ', 'is', ' awesome!')
```

如果`string`中不包含`str`则 `string_pre_str==string`。
```python
s = 'Python is awesome!'
parts = s.partition('was')
print(parts)
# ('Python is awesome!', '', '')
```

## startswith()
检查字符串**是否是以指定内容开头**，是则返回 `True`，否则返回 `False`。
```python
print('Patrick'.startswith('P'))
# True
```

## endswith()
检查字符串**是否是以指定内容结束**，是则返回 `True`，否则返回 `False`。
```python
print('Patrick'.endswith('ck'))
# True
```

# 格式化类
## format
format完整的语法格式为：
`{ [index][ : [[fill] align] [sign] [#] [width] [.precision] [type] ] }`
注意，格式中用` [] `括起来的参数都是可选参数。

各个参数的含义如下：
- `index`：指定`:`后边设置的格式要**作用到第几个数据**。如果省略此选项，则会根据先后顺序自动分配。
- `fill`：指定空白处填充的字符。
- `align`：指定数据的对齐方式。
  
  | align | 含义 |
  |---|---|
  |<    | 左对齐
  |>    | 右对齐
  |=	| 右对齐，同时将符号放置在填充内容的最左侧，只对数字类型有效
  |^	| 数据居中，需和 width 参数一起使用

- `sign`：指定有无符号数。

  | type类型值 | 含义 |
  |---|---|
  |+    | 正数前加正号，负数前加负号
  |-    | 正数前不加正号，负数前加负号
  |空格	| 正数前加空格，负数前加负号
  |#	| 显示二进制数、八进制数和十六进制数 0b、0o、0x前缀

- `width`：指定**输出数据时所占的宽度**。
- `.precision`：指定**保留的小数位数**。
- `type`：指定**输出数据的具体类型**。
   
  | type类型值 | 含义 |
  |---|---|
  |s    | 对字符串类型格式化
  |d    | 十进制**整数**
  |c	| 将十进制整数转换成对应的 **Unicode 字符**
  |e 或 E| 	转换成**科学计数法**
  |g 或 G|	自动在 e 和 f（或 E 和 F）中切换
  |b	| 将十进制转换成**二进制**表示
  |o	| 将十进制转换成**八进制**表示
  |x    | 将十进制转换成**十六进制**表示
  |f    | 转换为**浮点数**（默认保留小数点后 6 位）
  |%    | 显示百分比（默认显示小数点后 6 位）。
  
## center(n, s)
返回一个原字符串**居中**，并**使用空格填充至长度width**的新字符串。
```python
s = 'Python is awesome!'
s = s.center(30, '-')

print(s)
# ------Python is awesome!------
```

## ljust()
返回一个原字符串**左对齐**，并**使用空格填充至长度width**的新字符串。
```python
s = 'Python is awesome!'
s = s.ljust(30, '-')

print(s)
# Python is awesome!------------
```

## rjust()
返回一个原字符串**右对齐**，并**使用空格填充至长度width**的新字符串。
```python
s = 'Python is awesome!'
s = s.rjust(30, '-')

print(s)
# ------------Python is awesome!
```

## f-Strings
格式化字符串的新语法，与其他格式化方式相比，不仅更易读，更简洁，不易出错，而且速度更快！使用`f'{变量名}'`即可。
```python
num = 1
language = 'Python'
s = f'{language} is the number {num} in programming!'

print(s)
# Python is the number 1 in programming!
```

```python
num = 1
language = 'Python'
s = f'{language} is the number {num*8} in programming!'

print(s)
# Python is the number 8 in programming!
```

## zfill()
`string.zfill(width)`。返回长度为`width`的字符串，原字符串`string`**右对齐**，前面**填充0**。
```python
s = '42'.zfill(5)
print(s)
# 00042

s = '-42'.zfill(5)
print(s)
# -0042

s = '+42'.zfill(5)
print(s)
# +0042
```

## print时利用`sep=""`去掉空格
```python
a, b = 2, 3

print(a, "/", b) 
# 2 / 3

print(a, "/", b, sep="") 
# 2/3
```
# 其他
## ord()转换为ASCII码
`ord()`将字母转换成ASCII码值，`chr()`将ASCII码值转换成字母.
- 0~9 对应 48~57。
- A~Z 对应 65~90，a~z 对应97~122。**同一个字母大小写值相差 32**。
```py
def to_lower=(text):
    low_text = ""
    for c in text:
        if 65 <= ord(c) <= 90:
            c = chr(ord(c) + 32) # 转换为小写
        low_text += c
    return low_text
```

## textwrap包实现自动换行

```py
import textwrap

string = "This is a very very very very very long string."

print textwrap.wrap(string,8)
# ['This is', 'a very', 'very', 'very', 'very', 'very', 'long', 'string.'] 

print textwrap.fill(string,8)
# This is
# a very
# very
# very
# very
# very
# long
# string.
```

# 思路注意点
## 是否重排
- 若 $s_1, s_2$ 中**出现字符相同，且对应字符数量也相同**，则「互为重排」。

## 子串数量
- 在一个长度为 n 的串中有 $ n+(n-1)+(n-2)+...+2+1=n(n+1)/2 $ 个子串。
- 以某字符开头的子串个数 = 以该字符开头的**最长子串长度** = 串长-该字符位置
  例如，`s="BANANA"`：
  以`s[0]='B'`开头的子串有`(len(s)-0)=6`个：`['B', 'BA', 'BAN', 'BANA', 'BANAN', 'BANANA']`
  以`s[1]='A'`开头的子串有`(len(s)-1)=5`个：`['A', 'AN', 'ANA', 'ANAN', 'ANANA']`
  以`s[3]='A'`开头的子串有`(len(s)-3)=3`个：`['A', 'AN', 'ANA']`