---
title: algorithm
date: 2023-02-20 18:20:21
tags:
categories:
---











## permutation 全排列

```python
def permute(nums):
    if len(nums) == 1:
        # 因为待会要for i in permutation
        # 然后把nums和其他[]做拼接
        # 所以这里需要用[nums]
        return [nums]
    result = []

    for i in range(len(nums)):
        curr = nums[i]
        # 移除当前元素
        remaining = nums[:i] + nums[i+1:]

        # 递归求剩余元素的 permutation
        remaining_permutation = permute(remaining)

        # 把curr加上各种permutation
        for permutation in remaining_permutation:
            result.append([curr] + permutation)

    return result

print(permute([1,2,3]))
```







## collections



### defaultdict

defaultdict是一个字典的子类，它重载了一个方法并添加了一个可调用的默认值。如果使用一个不存在的键访问defaultdict中的元素，那么该元素将被初始化为指定的默认值。

```python
from collections import defaultdict

d = defaultdict(int)
print(d['a'])

# output
0
```





### Counter

Counter是一个用于计数的容器类型，它可以自动统计元素出现的次数。Counter可以接受任何可迭代对象作为输入，并返回一个字典，其中元素作为键，它们出现的次数作为值。

```python
from collections import Counter

c = Counter('hello world')
print(c)  # 输出 Counter({'l': 3, 'o': 2, 'e': 1, 'h': 1, ' ': 1, 'w': 1, 'r': 1, 'd': 1})

```



### deque

deque是一个双端队列，它支持在队列的两端进行快速的插入和删除操作。与列表相比，deque能够更快地执行append和pop操作，特别是在队列中包含大量元素时。



```python
from collections import deque

q = deque([1, 2, 3])
q.appendleft(0)
q.append(4)
print(q)  # 输出 deque([0, 1, 2, 3, 4])

```











## concept



### 时间复杂度

![image-20230221101233462](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20230221101233462.png)





![image-20230221101715358](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20230221101715358.png)



### sum

![image-20230221101548008](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20230221101548008.png)







## Graph 图



```python
# 可作无向图，也可为有向图
graph = {
    'A': ['B', 'C'],
    'B': ['A', 'C', 'D'],
    'C': ['A', 'B', 'D'],
    'D': ['B', 'C']
}
```



```python
# 可为有向图
# 对于大型图来说，可能会导致存储和计算效率低下
import numpy as np

graph = np.array([
    [0, 1, 1, 0],
    [1, 0, 1, 1],
    [1, 1, 0, 1],
    [0, 1, 1, 0]
])

```





删除节点

```python
def remove_node(graph, node):
    # 从图中删除节点
    del graph[node]
    
    # 从其他节点的邻居列表中删除该节点
    for _, neighbors in graph.items():
        if node in neighbors:
            neighbors.remove(node)

```





dfs

```python
def dfs(graph, start, visited=None):
    if visited is None:
        visited = set()
    visited.add(start)
    print(start)
    for neighbor in graph[start]:
        if neighbor not in visited:
            dfs(graph, neighbor, visited)

```



bfs

```python
from collections import deque

def bfs(graph, start):
    visited = set()
    queue = deque([start])
    while queue:
        node = queue.popleft()
        if node not in visited:
            visited.add(node)
            print(node)
            for neighbor in graph[node]:
                if neighbor not in visited:
                    queue.append(neighbor)

```

