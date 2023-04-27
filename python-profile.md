---
title: python_profile
date: 2023-04-23 18:23:35
tags:
categories:
---







# operation

## +=

```python
# 0.062
def main():
   s = 0
   for i in range(1000000):
      s = s+i


import profile
profile.run('main()')
```



```python
# 0.062
def main():
   s = 0
   for i in range(1000000):
      s += i

import profile
profile.run('main()')
```









# List

## extend and +

```python
# 0.859
lst = [[123]]*1000000
def main():
   s = []
   for item in lst:
      s.extend(item)


import profile
profile.run('main()')
```



```python
# 0.062
lst = [[123]]*1000000
def main():
   s = []
   for item in lst:
      s += item

import profile
profile.run('main()')
```









## 列表生成式

```python
# 1.016
def main():
    lst = []
    for i in range(1000000):
        lst.append(i)

import profile
profile.run('main()')
```



```python
# 0.078
def main():
   lst = [i for i in range(1000000)]

import profile
profile.run('main()')
```









# lambda and function

```python
# 0.094
def main():
   s = 0
   step = 1
   for i in range(1000000):
      s = lambda s, step: s+step


import profile
profile.run('main()')
```

```python
# 1.23
def add(s, step):
   return s + step

def main():
   s = 0
   step = 1
   for i in range(1000000):
      s = add(s, step)

import profile
profile.run('main()')
```



```python
# 0.016
def main():
   s = 0
   step = 1
   for i in range(1000000):
      s += step


import profile
profile.run('main()')
```

封装个函数。。。效率差了近100倍







# O(n2)

```python
# 2.0
def main():
   for i in range(1000):
      for j in range(i, 1000):
         print(i)

import profile
profile.run('main()')
```

```python
# 3.89
def main():
   for i in range(1000):
      for j in range(1000):
         print(i)


import profile
profile.run('main()')
```



2倍无法弥补算法n2数量级的差距











# queue 的popleft() -- 数据结构的碾压

```python
# 0.031
from collections import deque

def main():
   queue = deque([0]*1000000)
   for i in range(1000):
      queue.popleft()


import profile
profile.run('main()')
```

```python
# 2.172
def main():
    lst = [0]*1000000
    for i in range(1000):
       lst.pop(0)


import profile

profile.run('main()')
```



所以，请根据各个数据结构的规则选择合适的数据结构





# build data structure

```python
# 0.031
from collections import deque

def main():
   queue = deque([0]*1000000)


import profile
profile.run('main()')
```



```python
# 0.016
def main():
    lst = [0]*1000000


import profile

profile.run('main()')
```

所以其实build 数据结构不需要画太多的时间的



```python
# 0.031
def main():
   s = set([0]*1000000)


import profile
profile.run('main()')
```



