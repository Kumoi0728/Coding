[toc]

# input()
默认读取类型为str。
实在不会的话，如果输入有限，可暴力**写多行input()**。

## 一行一个数据
注意类型转换
```python
# 文字
s = input()

# 数字
n = int(input())
```
  
## 一行多个数据（用空格分隔）
使用.split()分隔，后用map()映射成其他类型

```python
# 文字
s = input().split()
```

```python
# 数字
a,b,c,d = map(int, input().split())

>>> print(a,b,c,d)
1 3 5 7

# 或列表存储
num_list = list(map(int, input().split()))

>>> print(num_list)
[1, 3, 5, 7]
```

## N行数据，每行一个值
每行int()转换后，**内包for**到列表中。因为一行一个，所以不用map()

```python
# 数字
num_list = [int(input()) for _ in range(N)]
```

## N行数据，每行多个值
每行分隔后map()，再list()转成列表，最后用内包for集为一个大列表

```python
# 数字
l = [list(map(int, input().split())) for l in range(N)]

>>> print(l)
[[1, 2], [3, 4], [5, 6]]
```

## 补充：np和list转换
list转np
```python
import numpy as np

l2n = np.array(list) #要素数:l2n.size，形状:l2n.shape
>>> print(l2n)
[[1 2 3]
 [4 5 6]
 [7 8 9]]
```
np转list
```python
n2l = l2n.tolist()
>>> print(list_list)
[[1, 2, 3], [4, 5, 6], [7, 8, 9]]
```

# sys.stdin
## 一行一个数据
sys.stdin.readline()可视作input()，但读取速度更快。

注意使用.rstrip()去除末尾换行符。

```python
import sys

input = sys.stdin.readline().rstrip()
```

## 一行多个数据（用空格分隔）
先split()去除空格，再变换类型（不需要map映射）：

```python
A, B, C = [int(x) for x in stdin.readline().rstrip().split()]

>>> print(A, B, C)
1 2 3
```

## N行数据，每行一个值
使用内包for
```python
data = [sys.stdin.readline().rstrip().split() for _ in range(N)]

>>> print(data)
[['1', '2', '3'], ['4', '5', '6'], ['7', '8', '9']]

>>> print(*data, sep='\n') # 好看的输出，给参数加上*分解传递
['1', '2', '3']
['4', '5', '6']
['7', '8', '9']
```

#  args


