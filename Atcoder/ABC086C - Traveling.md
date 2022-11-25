
# 题目
シカのAtCoDeerくんは二次元平面上で旅行をしようとしています。 AtCoDeerくんの旅行プランでは、時刻 00 に 点 (0,0)(0,0) を出発し、 11 以上 NN 以下の各 ii に対し、時刻 t_iti​ に 点 (x_i,y_i)(xi​,yi​) を訪れる予定です。

AtCoDeerくんが時刻 tt に 点 (x,y)(x,y) にいる時、 時刻 t+1t+1 には 点 (x+1,y)(x+1,y), (x-1,y)(x−1,y), (x,y+1)(x,y+1), (x,y-1)(x,y−1) のうちいずれかに存在することができます。 **その場にとどまることは出来ない**ことに注意してください。 AtCoDeerくんの旅行プランが実行可能かどうか判定してください。

### 入力
入力は以下の形式で標準入力から与えられる。
```
N
t1 x1 y1
::
tN xN yN
```

### 出力
旅行プランが実行可能なら`Yes`を、不可能なら`No`を出力してください。

# 自己的解法
计算出t时间所有可能到达的距离，判断是否在该距离list内。
**超时！** 计算时使用递归，且计算的是直线距离！
```python
def cal_d2(t):
    d2=[]
    if t%2==0:
        for i in range(t):
            d2.append(i*i)
            d2.append(i*i//2)
        d2=list(set(d2))
    else:
        if t<1:
            d2=[]
        else:
            d2=cal_d2(t-2)
            for i in range(t//2+1):
                d2.append(i*i+(t-i)*(t-i))
    return d2


if __name__ == '__main__':
    n=int(input())
    l=[list(map(int,input().split())) for _ in range(n)] # not input.split()!!

    res=0
    for t,x,y in l:
        distance = cal_d2(t)
        if x*x+y*y in distance:
            res+=1
    if res==n:
        print("Yes")
    else:
        print("No")
```

# 官方解说
因为运动只能向上、向下、向左或向右进行，所以这是==**曼哈顿距离，可直接用绝对值计算**d(i,j)=|xi-xj|+|yi-yj|==，可以理解为步数而不是直线距离。

起点与终点之间的曼哈顿距离，即移动步数为 d = abs(x0 - x) + abs(y0 - y)，可用时间内最长移动步数为dt = t-t0。
- 如果d>dt，只考虑时间就来不及，所以不可行。
- 如果d<dt，只考虑时间是有可能到达的，需要再考虑能否到达该终点。
  - 如果dt-d是偶数，说明不论中途移动到终点以外的哪个点，都使用了剩余的偶数个步数回到该终点（到别的点->回到终点需要2步）。
  - 如果dt-d是奇数，说明中途只能从终点移到别的点，而无法返回终点。
```python
N = int(input())
check = 1 # True
here = [0, 0]
t0 = 0

for i in range(N):
    t, x, y = map(int, input().split())
    cost =  (t-t0) - abs(x + y - sum(here)) # dt-d
    if cost < 0:
        check = 0
        break
    elif cost % 2:
        check = 0
        break
    else :
        t0 = t
        here[0] = x
        here[1] = y

if check:
    print("Yes")
else :
    print("No")
```