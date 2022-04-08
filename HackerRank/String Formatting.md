# 题目
Prints
The four values must be printed on a single line in the order specified above for each `i` from `1` to `number`. Each value should be space-padded to match the width of the binary value of  and the values should be separated by a single space.

输出十进制，八进制，十六进制，二进制。注意大写、对齐。

Sample Input
```
17
```
Sample Output
```
    1     1     1     1
    2     2     2    10
    3     3     3    11
    4     4     4   100
    5     5     5   101
    6     6     6   110
    7     7     7   111
    8    10     8  1000
    9    11     9  1001
   10    12     A  1010
   11    13     B  1011
   12    14     C  1100
   13    15     D  1101
   14    16     E  1110
   15    17     F  1111
   16    20    10 10000
   17    21    11 10001
```

# 自己的解法

- 直接输出oct()的结果会带0o，其余同理，所以要切片。
- 注意十六进制的字母要转为大写。
- 不带0b的二进制数的长度为对齐的宽度，使用 **rjust()** 实现右对齐。

```py
def print_formatted(number):
    w = len(bin(number)[2:])
    for i in range(1, number+1):
        print(str(i).rjust(w," "),
              oct(i)[2:].rjust(w," "),
              hex(i)[2:].upper().rjust(w," "),
              bin(i)[2:].rjust(w," "))
 ```

 # 利用format
```py
def print_formatted(number):
    width = len("{0:b}".format(number))
    for i in range(1,number+1):
        print("{0:{width}d} {0:{width}o} {0:{width}x} {0:{width}b}".format(i, width=width))
 ```
 format完整的语法格式为：
`{ [index][ : [[fill] align] [sign] [#] [width] [.precision] [type] ] }`
注意，格式中用 [] 括起来的参数都是可选参数。

各个参数的含义如下：
- **index**：指定`:`后边设置的格式要作用到第几个数据。如果省略此选项，则会根据先后顺序自动分配。
- **fill**：指定空白处填充的字符。
- **align**：指定数据的对齐方式。
  
  | align | 含义 |
  |---|---|
  |<    | 左对齐
  |>    | 右对齐
  |=	| 右对齐，同时将符号放置在填充内容的最左侧，只对数字类型有效
  |^	| 数据居中，需和 width 参数一起使用

- **sign**：指定有无符号数。

  | type类型值 | 含义 |
  |---|---|
  |+    | 正数前加正号，负数前加负号
  |-    | 正数前不加正号，负数前加负号
  |空格	| 正数前加空格，负数前加负号
  |#	| 显示二进制数、八进制数和十六进制数 0b、0o、0x前缀

- **width**：指定输出数据时所占的宽度。
- **.precision**：指定保留的小数位数。
- **type**：指定输出数据的具体类型。
   
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