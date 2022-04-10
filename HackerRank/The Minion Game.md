# 题目

两个玩家都被赋予相同的字符串S。
两个玩家都必须使用字符串中的字母制作子字符串。
Stuart 必须造以辅音开头的单词，Kevin 必须造以元音开头的单词。
当两个玩家都做出所有可能的子串时，游戏结束。
子字符串在字符串中出现时，得分+1。

例如：
![](https://s3.amazonaws.com/hr-challenge-images/9693/1450330231-04db904008-banana.png)

以辅音和元音开头的子串出现次数 
=> 以辅音和元音开头的，可重复计数的子串个数
=> 以某字符开头的可重复计数的子串个数 = 以该字符开头的**最长子串长度**
所以不能太拘泥于“出现次数”这一表达！

# 自己的解法
针对每个字母计算子串，把所有子串存入列表，列表长度即为分数。
注意**列表降维**用`sum(list,[])`，或者`+`即可。

```py
def minion_game(string):
    c="BCDFGHJKLMNPQRSTVWXYZ"
    v="AEIOU"

    S,K=[],[]
    for i in range(len(string)):
        if string[i] in c:
            S+=[string[i:j] for j in range(i+1,len(string)+1)]
        elif string[i] in v:
            K+=[string[i:j] for j in range(i+1,len(string)+1)]
    
    if len(S)>len(K):
        print("Stuart",len(S))
    elif len(S)<len(K):
        print("Kevin",len(K))
    elif len(S)==len(K):
        print("Draw")

# 针对BANANA
# S = ['B', 'BA', 'BAN', 'BANA', 'BANAN', 'BANANA', 'N', 'NA', 'NAN', 'NANA', 'N', 'NA']
# K = ['A', 'AN', 'ANA', 'ANAN', 'ANANA', 'A', 'AN', 'ANA', 'A']
# 若要去除列表重复元素：list(set(list))
```
方法对，但是==计算量太大，导致一些test没通过。==

修改为只计算子串出现次数（即列表长度），不实际保存列表：
```py
def minion_game(string):
    c="BCDFGHJKLMNPQRSTVWXYZ"
    v="AEIOU"

    S,K=0,0
    for i in range(len(string)):
        if string[i] in c:
            S+=len([string[i:j] for j in range(i+1,len(string)+1)])
        elif string[i] in v:
            K+=len([string[i:j] for j in range(i+1,len(string)+1)])
            
    if S>K:
        print("Stuart",S)
    elif S<K:
        print("Kevin",K)
    elif S==K:
        print("Draw")
```
不再出现abort called错误，但是仍不在规定运行时间内，因为循环里又**内包循环**了！！

# 官方解答
自己的思路距离正确答案只差一步：`len([string[i:j] for j in range(i+1,len(string)+1)])` 实际上就是当前字符到字符串末尾的长度啊！！
所以直接计算 `len(string) - i` 就好了！

==**如果多次循环字符串，考虑如何从数学上得出答案，而不是检查每个可能的迭代。**==

还有一点可以简化：只用打出元音列表就好了。
```py
def minion_game(string):
    vowels = 'AEIOU'

    Stuart, Kevin = 0, 0
    for i in range(len(string)):
        score = len(string) - i
        if string[i] in vowels:
            Kevin += score
        else:
            Stuart += score

    if Stuart == Kevin:
        print('Draw')
    if Stuart > Kevin:
        print('Stuart {}'.format(Stuart))
    if Stuart < Kevin:
        print('Kevin {}'.format(Kevin))
```

# 利用子串总数
利用数学方法减少一次循环：意识到在一个**长度为 n 的单词中有 $ n+(n-1)+(n-2)+...+2+1=n(n+1)/2 $ 个子串**。
因此，只需要计算以元音开头的子串的数量，然后**从子串的总数中减去以元音开头的子串的数量**，就可以得到以辅音开头的子串的数量。

```py
vow = "AEIOU"

slen = len(string)
tsub = int(slen * (slen + 1) / 2)

k = sum(slen - i for i in range(slen) if string[i] in vow)   
s = tsub - k # 不用循环计算了

if s > k: 
    print(f"Stuart {s}")
elif s < k: 
    print(f"Kevin {k}")
else: 
    print("Draw")
```
