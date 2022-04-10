# 题目
Output Format

Print the absolute difference $t_1 -t_2$ in seconds.

Sample Input 0
```
2
Sun 10 May 2015 13:54:36 -0700
Sun 10 May 2015 13:54:36 -0000
Sat 02 May 2015 19:54:36 +0530
Fri 01 May 2015 13:54:36 -0000
```

Sample Output 0
```
25200
88200
```
简而言之就是要计算时区差。

# 自己的解法
读取每行后分割再计算，太麻烦！

# 官方解答
利用datatime库
- `strptime()`根据指定的格式把一个时间字符串解析为时间元组。
    |格式化符号|含义|
    |---|---|
    |%y |两位数的年份表示（00-99）
    |%Y |四位数的年份表示（000-9999）
    |%m |月份（01-12）
    |%d |日期（0-31）
    |%H |24小时制小时（0-23）
    |%I |12小时制小时（01-12）
    |%M |分钟（00-59）
    |%S |秒（00-59）
    |%a |简化星期
    |%A |完整星期
    |%b |简化月份
    |%B |完整月份
    |%c |本地相应的日期表示和时间表示
    |%j |年内的一天（001-366）
    |%p |本地A.M.或P.M.的等价符
    |%U |一年中的星期数（00-53）星期天为星期的开始
    |%w |星期几（0-6），星期天为 0，星期一为 1
    |%W |一年中的星期数（00-53）星期一为始
    |%x |本地相应的日期表示
    |%X |本地相应的时间表示
    |%Z |当前时区的名称
    |%% |%号本身
- `seconds`获取的是时间差的秒数，遗漏了天
- `total_seconds()`获取两个时间之间的总差


注意：可**在循环里读取input()后操作**
```py
from datetime import datetime

# Sun 10 May 2015 13:54:36 -0700
# 星期 日期 月份 年份 24小时 分钟 秒 时区
format_string = "%a %d %b %Y %H:%M:%S %z" 
T = int(input())

for test in range(T): # 在循环里读取input()
    t1 = str(input())
    t2 = str(input())

    parsed_t1 = datetime.strptime(t1, format_string)
    parsed_t2 = datetime.strptime(t2, format_string)

    diff = parsed_t2 - parsed_t1

    print (int(abs(diff.total_seconds())) # 不要忘了绝对值
```