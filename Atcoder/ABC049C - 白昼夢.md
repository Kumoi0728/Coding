# 题目
判断s是否由 `dream` `dreamer` `erase` `eraser`的组合构成。
问题是如何处理诸如`dreamer`的最后一个`er`被`erase`的第一个`er`所覆盖的领域。

# 自己的解法
最终结果`WA`，估计问题出现在列表上？
记录思路：递归，送头开始切分，最后一次剩余的是4个单词中的一个则YES
==-> 为减少递归，用repalce()==
```py
def f(s):
    if len(s) < 5 or (s[0] != 'e' and s[0] != 'd'):
        return False
        
    if s in ["dream", "dreamer", "erase", "eraser"]:
        return True
    elif s[0]=='d':
        for i in ["dream", "dreamer"]:
            return f(s.split(i)[-1])
    elif s[0]=='e':
        for i in ["erase", "eraser"]:
            return f(s.split(i)[-1])
    return False

if __name__ == '__main__':
    s = input()
    if f(s) == False:
        print("NO")
    else:
        print("YES")
```

# `replace()`法
最快最简单的方法。
不是从第一个字母开始分割，而是只要找到某个单词，就用`""`代替。

关键在于**按照什么顺序替换**四个单词。
dreamer含有er的部分，所以如果先替换dreamer，那么替换后有些erase会变成ase。所以先替换earser和earse。
```py
S = input() 

# eraser, erase, dreamer, dream の順に消していく 
S = S.replace('eraser', '') 
S = S.replace('erase', '') 
S = S.replace('dreamer', '') 
S = S.replace('dream', '') 

if S == '': 
	print('YES') 
else: 
	print('NO')
```

# 官方解答
反向查看四个单词。
反向后`dream`, `dreamer`, `erase`, `eraser`分别为`maerd`, `remaerd`, `esare`, `resare`，这样**任意一个单词都不是其他单词的前缀**了.
所以从后往前，如果发现符合的话就立即分解。S最终无法分解时输出NO，否则输出YES。
```py
s = input()[::-1]  

while s:  
	start = len(s)  
	for t in ['maerd', 'remaerd', 'esare', 'resare']:  
		if t == s[:len(t)]:  
			s = s[len(t):]  
	if start == len(s):  
		break

print("YNEOS"[len(s)>0::2]) # False=1
```

# 正则表达式法
```py
import re 

S = input() 
''' 
^：文字列の先頭
|：OR 
+：直前のパターンを1回以上繰り返し
$：文字列の末尾 
''' 
if re.match("^(dream|dreamer|erase|eraser)+$", S): 
	print('YES') 
else: 
	print('NO')
```
![[正则表达式.png]]