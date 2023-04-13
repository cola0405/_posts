---
title: 汇编-python游记
date: 2022-06-06 12:02:55
tags:
categories:
---



## 赋值List（非copy）

```python
x = [1, 2, 3]
y = x[:]
x[0] = 111

print(x)
print(y)
```

