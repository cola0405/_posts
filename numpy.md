---
title: numpy
date: 2022-09-27 11:17:09
tags:
categories:
---





## axis

{0 or ‘index’, 1 or ‘columns’}, default 0

Whether to drop labels from the index (0 or ‘index’) or columns (1 or ‘columns’).



```python
# 删除 <Unnamed: 32> 这一列
# 多列的话，都放到list里，他自己去迭代
# 单列的话，不用list也许
x = df.drop(['Unnamed: 32'], axis='columns')
```

默认drop的参数是index



```python
# 删除index=1的那一行
x = df.drop(1)
```

```
         id diagnosis  ...  fractal_dimension_worst  Unnamed: 32
0    842302         M  ...                  0.11890          NaN
2  84300903         M  ...                  0.08758          NaN
3  84348301         M  ...                  0.17300          NaN
4  84358402         M  ...                  0.07678          NaN
5    843786         M  ...                  0.12440          NaN
```







## create

```python
import numpy as np

z = np.zeros((2,2), dtype = int)
print(z)
```



```python
import numpy as np 
 
x =  [1,2,3] 
a = np.asarray(x)  
print (a)
```

