# 题目
In this challenge, the user enters a string and a substring. You have to **print the number of times that the substring occurs in the given string**. String traversal will take place from left to right, not from right to left.

也就是输出子串出现次数。

Sample Input
```
ABCDCDC 
CDC
```

Sample Output
```
2
```


# 自己的解法
`find`找到子串第一次出现在i，删除i以及之前的串，再在剩余串中寻找子串，直到子串为空。
```py
def count_substring(string, sub_string):
    i=1
    count=0
    while(string!=None):
        i=string.find(sub_string)
        #print(i)
        if i!=-1: # 如果不存在则会返回-1
            count+=1
            string=string[i+1:]
        else:
            break
        #print(count,string)
    return count
```

# 使用startswith()
循环长度使用切片，省去实际删除子串的操作。
```py
def count_substring(string, sub_string):
    count = 0
    for i in range(len(string)):
        if string[i:].startswith(sub_string):
            count += 1
    return count
```

# 暴力解法
内包简写：
```py
def count_substring(string, sub_string):
    return sum([ 1 for i in range(len(string)-len(substring)+1) if string[i:i+len(substring)] == substring])
```

扩写以后其实就是暴力解法啦
```py
def count_substring(string, sub_string):
    count=0
    for i in range(len(string)-len(substring)+1):
        if string[i:i+len(substring)] == substring]:
            count+=1
    return count
```