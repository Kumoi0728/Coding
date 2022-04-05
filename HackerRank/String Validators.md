# 题目
You are given a string .
Your task is to find out if the string  contains: alphanumeric characters, alphabetical characters, digits, lowercase and uppercase characters.

判断字符串中是否含有：字母或数字字符，字母字符，数字字符，小写字符，大写字符。

Sample Input
```
qA2
```
Sample Output
```
True
True
True
True
True
```

# 自己的解法
`isalnum()` `isalpha()` `isdigit()` `islower()` `isupper()`都是判断**所有字符**的，所以需要循环。

暴力解法，依次判断每个字符，如果有符合的就break跳出循环。
```py
if __name__ == '__main__':
    s = input()
    for i in range(len(s)):
        if s[i].isalnum():
            break
    print(s[i].isalnum())

    for i in range(len(s)):
        if s[i].isalpha():
            break
    print(s[i].isalpha())
    
    for i in range(len(s)):
        if s[i].isdigit():
            break
    print(s[i].isdigit())
    
    for i in range(len(s)):
        if s[i].islower():
            break
    print(s[i].islower())
    
    for i in range(len(s)):
        if s[i].isupper():
            break
    print(s[i].isupper())
```

# 使用any()简化
`any()`用于判断给定的可迭代参数 iterable 是否全部为 False，则返回 False，**如果有一个为 True，则返回 True**。
```py
print any(c.isalnum() for c in str)
print any(c.isalpha() for c in str)
print any(c.isdigit() for c in str)
print any(c.islower() for c in str)
print any(c.isupper() for c in str)
```

# 存在则改变标记值
用四个变量存放标记，均初始化为False。
依次判断，如果存在则标记为True。
```py
l=list(string)
a,b,c,d,e=False,False,False,False,False
for i in l:
    if i.isalnum():
        a=True
    if i.isalpha():
        b=True
    if i.isdigit():
        c=True
    if i.islower():
        d=True
    if i.isupper():
        e=True
print a
print b
print c
print d
print e
```