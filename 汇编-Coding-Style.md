---
title: 汇编-Coding-Style
date: 2022-04-02 10:25:29
tags:
categories:
---



# python

[文档](https://peps.python.org/pep-0008/#blank-lines)



## 空行

Use blank lines in functions, sparingly, to indicate logical sections.



## import

```python
# Correct:
import os
import sys

# Wrong:
import sys, os
```





## whitespace

```python
# Correct:
spam(ham[1], {eggs: 2})
# Wrong:
spam( ham[ 1 ], { eggs: 2 } )


# Correct:
foo = (0,)
# Wrong:
bar = (0, )


# Correct:
if x == 4: print(x, y); x, y = y, x
# Wrong:
if x == 4 : print(x , y) ; x , y = y , x
    
    
# Correct:
ham[1:9], ham[1:9:3], ham[:9:3], ham[1::3], ham[1:9:]
ham[lower:upper], ham[lower:upper:], ham[lower::step]
ham[lower+offset : upper+offset]
ham[: upper_fn(x) : step_fn(x)], ham[:: step_fn(x)]
ham[lower + offset : upper + offset]
# Wrong:
ham[lower + offset:upper + offset]
ham[1: 9], ham[1 :9], ham[1:9 :3]
ham[lower : : upper]
ham[ : upper]


# Correct:
i = i + 1
submitted += 1
x = x*2 - 1
hypot2 = x*x + y*y
c = (a+b) * (a-b)
# Wrong:
i=i+1
submitted +=1
x = x * 2 - 1
hypot2 = x * x + y * y
c = (a + b) * (a - b)


```





## function

```
# Correct:
def complex(real, imag=0.0):
    return magic(r=real, i=imag)
# Wrong:
def complex(real, imag = 0.0):
    return magic(r = real, i = imag)
```

### function name

lowercase with words separated by underscores as necessary to improve readability.



### function return 

```python
# Correct:
def foo(x):
    if x >= 0:
        return math.sqrt(x)
    else:
        return None
def bar(x):
    if x < 0:
        return None
    return math.sqrt(x)



# Wrong:
def foo(x):
    if x >= 0:
        return math.sqrt(x)
def bar(x):
    if x < 0:
        return
    return math.sqrt(x)
```







## list

```python
# Correct:
FILES = [
    'setup.cfg',
    'tox.ini',
    ]
initialize(FILES,
           error=True,
           )
# Wrong:
FILES = ['setup.cfg', 'tox.ini',]
initialize(FILES, error=True,)
```





## comment

```python
x = x + 1                 # Increment x
```





## naming

```
b (single lowercase letter)
B (single uppercase letter)

lowercase
lower_case_with_underscores

UPPERCASE
UPPER_CASE_WITH_UNDERSCORES

CapitalizedWords
mixedCase
```



### avoid

Never use the characters ‘l’ (lowercase letter el),

 ‘O’ (uppercase letter oh)

or ‘I’ (uppercase letter eye) as single character variable names

In some fonts, these characters are indistinguishable from the numerals one and zero

When tempted to use ‘l’, use ‘L’ instead



## module name

Python packages should also have short all-lowercase names

although the use of underscores is discouraged.



### class name 

CapWords



## operation

`''.join()` form should be used instead





### file operation

use a `with` statement to ensure it is cleaned up promptly and reliably after use





## underscores

double leading underscores should be used only to avoid name conflicts 

with attributes in classes designed to be subclassed





## string

### substring

```python
# Correct:
if foo.startswith('bar'):
# Wrong:
if foo[:3] == 'bar':
```





### empty

(strings, lists, tuples), use the fact that empty sequences are false

```python
# Correct:
if not seq:
if seq:
# Wrong:
if len(seq):
if not len(seq):
```





### bool

```python
# Correct:
if greeting:
# Wrong:
if greeting == True:
```





# Java

![image-20220428210603194](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220428210603194.png)

## comment

```java
if (a == 2) {
    return TRUE;            /* special case */
} else {
    return isPrime(a);      /* works only for odd a */
}
```

Very short comments can appear on the same line as the code they describe



```java
if (foo > 1) {

    // Do a double-flip.
    ...
}
else {
    return false;          // Explain why here.
}
//if (bar > 1) {
//
//    // Do a triple-flip.
//    ...
//}
//else {
//    return false;
//}
```

It shouldn't be used on consecutive multiple lines for text comments

however, it can be used in consecutive multiple lines for commenting out sections of code



## variable

```java
int level;
int size;
```



## while

```java
while (condition) {
    statements;
}
```

A keyword followed by a parenthesis(括号) should be separated by a space





## try

```java
try {
    statements;
} catch (ExceptionClass e) {
     statements;
}
```





## package

should be one of the top-level domain names

currently com, edu, gov, mil, net, org, or one of the English two-letter codes 

identifying countries as specified in ISO Standard 3166, 1981

```
com.sun.eng
com.apple.quicktime.v2
edu.cmu.cs.bovik.cheese
```







## 原则

我觉得可读性是>简洁性的

当然，也不能太啰嗦

![image-20220428213114022](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220428213114022.png)





## 函数大小

一般不超过50行



# JSON

## 日期

![image-20220428214753281](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220428214753281.png)



## 多层级关系

![image-20220428215046699](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220428215046699.png)

















# SQL



Always use uppercase for the reserved keywords like `SELECT` and `WHERE`

## example

```sql
SELECT file_hash
  FROM file_system
 WHERE file_name = '.vimrc';
```

```sql
/* Updating the file record after writing to the file */
UPDATE file_system
   SET file_modified_date = '1980-02-22 13:19:01.00000',
       file_size = 209732
 WHERE file_name = '.vimrc';
```



## alias

```sql
SELECT first_name AS fn
  FROM staff AS s1
  JOIN students AS s2
    ON s2.mentor_id = s1.staff_num;
```

```sql
SELECT SUM(s.monitor_tally) AS monitor_total
  FROM staff AS s;
```



## insert

```sql
INSERT INTO albums (title, release_date, recording_date)
VALUES ('Charcoal Lane', '1990-01-01 01:01:01.00000', '1990-01-01 01:01:01.00000'),
       ('The New Danger', '2008-01-01 01:01:01.00000', '1990-01-01 01:01:01.00000');
```

