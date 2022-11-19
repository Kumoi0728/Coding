# deque用法
- 如果要经常从两端 append 数据，deque 比较好
- 如果要实现随机访问，建议用list
- 大多数函数和list相同
```python
# 定义
q = collections.deque()

# 如果构建deque 的时候,指定了maxlen, 则可以通过 d.maxlen 来获得dueue的最大长度。如果插入的数据大于 maxlen 则会自动删除旧的元素.删除什么元素取决于从哪边添加数据.
d = deque(list(range(5)),maxlen=5) # deque([0, 1, 2, 3, 4])
# 从左边添加元素, # 元素4 被挤出 队列
d.appendleft('frank') # deque(['frank', 0, 1, 2, 3])
# 从右边添加元素, 元素 'frank'  被挤出队列.
d.append('xiaoming')# deque([0, 1, 2, 3, 'xiaoming'])
q.maxlen # 查看

# 入队列：默认从右边加入，也可从左边；也可以加入一个列表
q.append(10) # Out[7]: deque([10])
q.appendleft('a')

q.extend(mylist) 
q.extendleft(mylist) # 从左边加入

# 出队列
q.pop() 
q.popleft()

# 查看队列里面元素个数
print len(q)

# 统计元素的个数
q.count('a')

# 在某个位置insert 一个元素 insert(i, x)
q.insert(2,'frank') # Out[33]: deque([10, 12, 'frank', 13, 14])

#翻转操作 
q.reverse()

# 移除某个元素 
mydeque.remove(10) # deque(['e', 'd', 'c', 'b', 'a', 12])

# 清空队列元素
mydeque.clear # Out[47]: <function deque.clear>
mydeque.clear() # deque([])

# 浅拷贝, Create a shallow copy of the deque.
d4 = d3.copy() # 等于d[:]？

# 对队列实行旋转操作（每个元素依次向后移动value步，最后一个移动到第一个算一步）
d = deque()
d.extend(['a', 'b', 'c', 'd', 'e'])
d.rotate(2)  # 指定次数，默认1次
print(d) # deque(['d', 'e', 'a', 'b', 'c'])
```
# 将列表当做堆栈
用 append() 把一个元素添加到堆栈顶。
用不指定索引的 pop() 把一个元素从堆栈顶释放出来。