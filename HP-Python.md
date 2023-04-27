---
title:  HP_Python
date: 2022-08-12 10:40:24
tags: 
categories:
---



**vscode 安装c/c++插件后才能跳转**

# Python 原理

## PyObject*

![image-20220823162918787](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220823162918787.png)

![image-20220902183048816](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220902183048816.png)



## Basic rule

![image-20220818101844837](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220818101844837.png)







## CPython

![image-20220816162827683](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220816162827683.png)



id 就是内存地址



```python
import sys

print(sys.getsizeof([]))
```



Otherwise, [Memory protection](https://en.wikipedia.org/wiki/Memory_protection) rules imposed by the operating system will produce some sort of memory fault and ultimately kill the program trying to read "illegal" memory.

```
 <Address 0x1aed06b0 out of bounds>
 内存越界，访问到了不属于你的内存。可以用bt命令看调用堆栈
```









**Virtual memory address**

A virtual address is a [binary](https://www.techtarget.com/whatis/definition/binary) number in [virtual memory](https://www.techtarget.com/searchstorage/definition/virtual-memory) that enables a process to use a location in [primary storage](https://www.techtarget.com/searchstorage/definition/primary-storage) (main memory) independently of other processes and to use more space than actually exists in primary storage by temporarily relegating some contents to a [hard disk](https://www.techtarget.com/searchstorage/definition/hard-disk) or internal [flash drive](https://www.techtarget.com/searchstorage/definition/flash-based-solid-state-drive-SSD).





## compile

![image-20220821233759265](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220821233759265.png)

![image-20220821233914955](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220821233914955.png)





![image-20220821235639691](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220821235639691.png)









































## Python virtual machine

The Python interpreter does a lot of work to try to abstract away the underlying computing elements that are being used. 

At no point does a programmer need to worry about allocating memory for arrays

how to arrange that memory, or in what sequence it is being sent to the CPU. 

This is a benefit of Python, since it lets you focus on the algorithms that are being implemented. 

However, it comes at a huge performance cost.  

















## Source code structure

![image-20220828230521214](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220828230521214.png)





## sequence

![image-20220908103855135](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220908103855402.png)

![image-20220908104016495](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220908104016495.png)

![image-20220908112432400](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220908112432400.png)

```python
a = 2,3,4,5
print(type(a)) # Tuple
```

以致于`Tuple`没有专门的`iterable`的生成方法



ast只是构造语法树，具体Tuple的创建在compile

![image-20220908114033276](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220908114033276.png)

![image-20220908113951135](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220908113951135.png)

![image-20220908114555070](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220908114555070.png)

```
  1           0 LOAD_CONST               0 (1)
              2 STORE_NAME               0 (a)

  2           4 LOAD_CONST               1 (2)
              6 STORE_NAME               1 (b)

  3           8 LOAD_NAME                1 (b)
             10 LOAD_NAME                0 (a)
             12 ROT_TWO
             14 STORE_NAME               0 (a)
             16 STORE_NAME               1 (b)
             18 LOAD_CONST               2 (None)
             20 RETURN_VALUE

```

```
# 交换两个最顶层的堆栈项
# ps:只是取元素，并没有pop()出来
ROT_TWO 
```

![image-20220908115558851](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220908115558851.png)

紧接着

```
             14 STORE_NAME               0 (a)
             16 STORE_NAME               1 (b)
```





![image-20220908120816823](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220908120816823.png)



注意！取出来的不是字节码中的index，而是py对象指针

字节码和实际程序运行的堆栈不是一一对应的

字节码只是指令的集合



![image-20220908135823168](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220908135823168.png)



```
locals() 函数会以字典类型返回当前位置的全部局部变量
```

`LOAD_NAME` 找变量，然后`push`入栈

![image-20220908140820387](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220908140820387.png)



`STORE_NAME`

![image-20220908141049239](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220908141049239.png)









```python
a, b, c = map(int, "1 2 3".split(' '))

print(a)
```



对于可迭代的对象可以这么赋值，那么同理：

```python
a, b, c = "abc"

print(a)
```



Ps：

```python
# error
a, b, c = map(int, "1 2 3")

print(a)
```

因为一位一位迭代的，迭代到空格时，无法应用`int()`则出错



```python
a, b, c = map(int, "123")

print(a)
```

这样可以，但是只能应对一位数



```python
# error
a, b, c = map(int, "1234")

print(a)
```

超数位的话，会报错

因为map可以迭代4次， 但是左边只有3个对象









## vscode

![image-20220828205946122](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220828205946122.png)















## 官网文档

https://docs.python.org/zh-cn/3/library/language.html



https://docs.python.org/zh-cn/3/reference/index.html#reference-index









# Buildin

https://docs.python.org/3.9/library/





## assert

![image-20220924164159384](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220924164159384.png)



assert是应用在unittest或pytest环境中

不能应用到业务代码中, 因为断言会导致运行中断

但不可否认, 使用断言非常方便调试代码

通过研读assert的文档, 发现断言是可以被关闭的



启动命令行添加参数

```python
python -O main.py
```









## id()

![image-20220901140919154](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220901140919154.png)

![image-20220901140857842](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220901140857842.png)

就是当前指针指向的内存地址





## filter()

接收两个参数，第一个为函数，第二个为序列

序列的每个元素作为参数传递给函数进行判断，然后返回 True 或 False

最后将返回 True 的元素封装到可迭代的对象filter中

```python
def odd(num):
    if num%2 == 0:
        return False
    return True


lst = [1,2,3,4,5]
print(list(filter(odd, lst))) # [1,3,5]
```







## map()

说白了，就是迭代取每一个元素作为参数，调用指定的方法，把所有返回值封装到可迭代的map对象中，然后返回

```python
list(map(int, ["1", "2"]))
```



![image-20220923154125945](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220923154125945.png)





需要注意的是，map是允许多参数的

`int()`需要一个参数就够了，但是对于`max()`

可能需要两个参数，然后这种条件下：

```python
print(list(map(max, (1, 2, 3, 4, 5), (5, 4, 3, 2, 1))))
# [5,4,3,4,5]
```

![image-20220923154434851](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220923154434851.png)





以上是Python2.5.6的源码，返回的`result`是个`list`

但是，在python3中

![image-20220901141613297](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220901141613297.png)

返回的是可迭代的`mapobject`

所以，可以再把map转成list

```python
list(map(int, ["1", "2"]))
```

```python
print(list(map(int, "12345")))
```





## profile

性能分析



```python
def f1():
    lst = []
    for i in range(10000000):
        lst.append(i)

def f2():
    lst = [i for i in range(10000000)]

import cProfile
cProfile.run('f1()')
cProfile.run('f2()')
```

```
   ncalls  tottime  percall  cumtime  percall filename:lineno(function)
        1    0.127    0.127    1.780    1.780 <string>:1(<module>)
        1    0.997    0.997    1.653    1.653 t.py:1(f1)
        1    0.000    0.000    1.780    1.780 {built-in method builtins.exec}
 10000000    0.656    0.000    0.656    0.000 {method 'append' of 'list' objects}
        1    0.000    0.000    0.000    0.000 {method 'disable' of '_lsprof.Profiler' objects}


         5 function calls in 0.499 seconds

   Ordered by: standard name

   ncalls  tottime  percall  cumtime  percall filename:lineno(function)
        1    0.078    0.078    0.499    0.499 <string>:1(<module>)
        1    0.000    0.000    0.421    0.421 t.py:6(f2)
        1    0.421    0.421    0.421    0.421 t.py:7(<listcomp>)
        1    0.000    0.000    0.499    0.499 {built-in method builtins.exec}
        1    0.000    0.000    0.000    0.000 {method 'disable' of '_lsprof.Profiler' objects}


```





tottime

在指定函数中消耗的总时间（不包括调用子函数的时间）



cumtime

指定的函数及其所有子函数（从调用到退出）消耗的累积时间。这个数字对于递归函数来说是准确的。





## raise

抛出异常







## repr()

便于debug



```python
print(5) # 5
print(‘5’) # 5
```



```python
print(repr(5)) # 5
print(repr(‘5’)) # '5'
```













# Bool

特殊的int类型

```c
typedef PyIntObject PyBoolObject;
```

![image-20220916113420143](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220916113420143.png)



if 后面、and or 左右可以放任何类型的数据

只是在进行and or 操作的时候、在if判断的时候

每种类型有各自的计算bool值的方法——`object.c`里

数字--是否为0

序列--长度是否为0







## compare



```python
b = 1>2
```

```
              0 LOAD_CONST               0 (1)
              2 LOAD_CONST               1 (2)
              4 COMPARE_OP               4 (>)
              6 STORE_NAME               0 (b)

```



![image-20220916151025380](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220916151025380.png)



对于其他类型则各自处理

![image-20220916151048402](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220916151048402.png)





![image-20220916163900938](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220916163900938.png)





## expression

来者不拒。。各种类型都可以放里面

![image-20220916155615173](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220916155615173.png)



```python
print(abs or 1) # <built-in function abs>
```





## short-circuit

```python
a = "" or "It is a empty string"
```

```
  2           0 LOAD_CONST               0 ('')
              2 JUMP_IF_TRUE_OR_POP      6
              4 LOAD_CONST               1 ('It is a empty string')
        >>    6 STORE_NAME               0 (a)

```



![image-20220916150558247](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220916150558247.png)









## string to bool

![image-20220916113202232](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220916113202232.png)

如果是字符串，ok则为字符串长度

![image-20220916113223141](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220916113223141.png)



注意，else时返回1

也就是我们自定义的对象都是返回1





![image-20220916113301601](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220916113301601.png)



```python
print(bool(""))
```







# Class

[doc](https://docs.python.org/zh-cn/3/reference/datamodel.html#types)



## rewrite

可以自定义比较方法！

如`__eq__()` `__gt__()`等



甚至于其他的各种操作都能重写

`__xor__()`



但是要注意，有些只是回调函数，并不是重写，如`__del__()`





## buildin



### \__call__

```python
class o3:
    def __init__(self):
        print("init")
    def __call__(self, *args, **kwargs):
        print("call")


t = o3() # call class
t() 	 # call object
```

```python
# init
# call
```

发现`__call__`对应object的调用







### \__dict__

```python
class c:
    def __init__(self):
        self.a = 22


print(c().__dict__)# {'a': 22}
```

```python
class c:
    def __init__(self):
        self.a = 22


t = c()
t.a = 999
print(t.__dict__)  # {'a': 999}
```



说白了，就是成员变量，且`__dict__`会动态变化，不同于`__slot__`是静态的







### \__del__()

不仅仅是主动del

被动删除也会回调这个







## \__getitem__()

重写下标访问



```python
class d:
    def __getitem__(self, index):
        return 666
```



```python
s = d()
print(s[2]) # 666
```







### \__ne__(o)

Return self!=value

True 或 False







### \__setattr__(name, value)

其实就相当于

```python
object.name = "cola"
```





### \__slots__

The proper use of `__slots__` is to save space in objects. Instead of having a dynamic dict that allows adding attributes to objects at anytime, there is a static structure which does not allow additions after creation. 



slot 定义后，无法动态添加成员

该object的成员已经static化了



而且slots只接受**string类型**的数据，构一个元组，作**成员变量名**



然后slots中的成员变量记得赋值后再使用，不然会报错



```python
class c:
    __slots__ = ("good")

t = c()
t.good = 2
print(t.good)
```



## comment

```python
class hello:
    'Say hello'
    pass
```



![image-20221010094155638](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20221010094155638.png)







## object

Formally, an object is a collection of data and associated behaviors.  







## import

```python
from h import hello

t = hello()
```

这样就不用`h.hello()`了







### relative import

```python
# 引入module所在目录下的database module
from .database import Database
```



```python
# 引入module所在目录的上一级目录的database module
from ..database import Database
```







## iterable

实现了迭代相关的方法，那么这个方法就是iterable

1.实现`__iter__()`

2.实现了`__getitem__()`



```python
class oi:
    def __iter__(self):
        for i in range(10):
            yield i


for i in oi():
    print(i)
```





```python
class oi:
    def __getitem__(self, item):
        if item < 10:
            return item
        raise StopIteration


for i in oi():
    print(i)

# 0~9
```







## package and modules

A package is a collection of modules in a folder

一个`xx.py`就是一个module





### \__init__.py

老是会遇见`__init__.py`，它其实是用来标记`package`的

具体往下看：



注意！

常规的folder，是无法被import的

![image-20221010095111684](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20221010095111684.png)





然而在添加了`__init__.py` 标注成package后，就可以import了

![image-20221010095140198](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20221010095140198.png)











## pattern

## decorator pattern

参考subclass那一章节











## private

**两个**下划线开头的作private，可作用于变量和方法

```python
class o5:
    __name = "cola"

t = o5()
print(t.__name)

# AttributeError: 'o5' object has no attribute '__name'
```



可访问，但没办法直接修改

```python
class o6:
    __name = "cola"

    @property
    def name(self):
        return self.__name

t = o6()
print(t.name)
t.name = 99
print(t.name)

# cola
# AttributeError: can't set attribute
```







## self

本质上self是一个变量

然后在创建实例后，self就是对象实例

```python
class c:
    def __init__(self):
        print(isinstance(self, c))
        pass

c() # True
```









## static





## subclass

beverage.py

```python
class Beverage():
    def description(self):
        return "beverage"
    def get_cost(self):
        return  0.0
```

coffee.py

```python
from beverage import Beverage

class Coffee(Beverage):
    pass
```

t.py

```python
from coffee import Coffee

c = Coffee()
print(c.description())
```



可以重写，也直接用父类的

这就是最简单的Decorator pattern















# Concept

## asdl

Abstract Syntax Definition Language



## atom

“原子”指表达式的最基本构成元素。

 最简单的原子是标识符和字面值。 

以圆括号、方括号或花括号包括的形式在语法上也被归类为原子。 原子的句法为:

```
atom      ::=  identifier | literal | enclosure
enclosure ::=  parenth_form | list_display | dict_display | set_display
               | generator_expression | yield_atom
```





## Augassign and Assign

增强赋值

+=



assign 在compile

![image-20220908113725314](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220908113725314.png)





```c
struct {
	asdl_seq *targets;
	expr_ty value;
} Assign;
```





## base

进制

base = 16 表示16进制







## callable

![image-20220828110216742](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220828110216742.png)













## Closure functions 

闭包函数

函数里面的函数



```python
count = 1

def a():
    count = 'a函数里面'  　　#如果不事先声明，那么函数b中的nonlocal就会报错
    def b():
        print(count)
        count = 2
    b()
    print(count)

if __name__ == '__main__':
    a()
    print(count)
```







## cxt context？





## enclose

![image-20221124104850229](C:\Users\10201\AppData\Roaming\Typora\typora-user-images\image-20221124104850229.png)



函数里定义一个函数，那么enclose就是内函数外的命名空间

再就是在类里面定义一个函数，函数外，类内的命名空间









## expression

![image-20220909233623295](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220909233623295.png)







## factor？





## flags

![image-20220828202911546](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220828202911546.png)









## free variable

![image-20220828203343767](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220828203343767.png)







## Generator

`yield`



```python
def f():
    for i in range(10):
        yield i

a = f()
```

```python
  1           0 LOAD_CONST               0 (<code object f at 0x000001AE1E313660, file "t.py", line 1>)
              2 LOAD_CONST               1 ('f')
              4 MAKE_FUNCTION            0
              6 STORE_NAME               0 (f)

  5           8 LOAD_NAME                1 (print)
             10 LOAD_NAME                0 (f)
             12 CALL_FUNCTION            0
             14 LOAD_METHOD              2 (__next__)
             16 CALL_METHOD              0
             18 CALL_FUNCTION            1
             20 POP_TOP
             22 LOAD_CONST               2 (None)
             24 RETURN_VALUE

Disassembly of <code object f at 0x000001AE1E313660, file "t.py", line 1>:
  2           0 LOAD_GLOBAL              0 (range)
              2 LOAD_CONST               1 (10)
              4 CALL_FUNCTION            1
              6 GET_ITER
        >>    8 FOR_ITER                10 (to 20)
             10 STORE_FAST               0 (i)

  3          12 LOAD_FAST                0 (i)
             14 YIELD_VALUE
             16 POP_TOP
             18 JUMP_ABSOLUTE            8
        >>   20 LOAD_CONST               0 (None)
             22 RETURN_VALUE

```



```python
def f():
    for i in range(10):
        return i

print(f())
```



```
  1           0 LOAD_CONST               0 (<code object f at 0x00000251ACC33660, file "t.py", line 1>)
              2 LOAD_CONST               1 ('f')
              4 MAKE_FUNCTION            0
              6 STORE_NAME               0 (f)

  5           8 LOAD_NAME                1 (print)
             10 LOAD_NAME                0 (f)
             12 CALL_FUNCTION            0
             14 CALL_FUNCTION            1
             16 POP_TOP
             18 LOAD_CONST               2 (None)
             20 RETURN_VALUE

Disassembly of <code object f at 0x00000251ACC33660, file "t.py", line 1>:
  2           0 LOAD_GLOBAL              0 (range)
              2 LOAD_CONST               1 (10)
              4 CALL_FUNCTION            1
              6 GET_ITER
              8 FOR_ITER                10 (to 20)
             10 STORE_FAST               0 (i)

  3          12 LOAD_FAST                0 (i)
             14 ROT_TWO
             16 POP_TOP
             18 RETURN_VALUE
        >>   20 LOAD_CONST               0 (None)
             22 RETURN_VALUE

```







![image-20220923150008408](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220923150008408.png)



`yield`说白了，就是作 return 把一个值返回之后，继续那个function的执行



![image-20220923150201530](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220923150201530.png)







## inplace operator

+=

-=

......











## locals?

![image-20221124104840360](C:\Users\10201\AppData\Roaming\Typora\typora-user-images\image-20221124104840360.png)





## literal

固定值







## mapping

![image-20220912101459730](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220912101459730.png)

python里边

变量？

字典？







## mangling

public private 等修饰

can be considered a way to implement private members in python









## main不是主函数

![image-20220907181447776](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220907181447776.png)







## \_\_name\_\_

```
__name__ == '__main__' 就表示在当前文件中，可以在if __name__ == '__main__':条件下写入测试代码，如此可以避免测试代码在模块被导入后执行
```















## opname

人类可读的操作名称











## pyc

编译后的字节码文件

其实就是对应PyCodeObject保存在硬盘中的存在形式



![image-20220822000747996](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220822000747996.png)

![image-20220822000717627](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220822000717627.png)



![image-20220822000737299](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220822000737299.png)



Ps: Item 已经是对象了

![image-20220822001231853](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220822001231853.png)



常量的GETITEM

![image-20220822001451725](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220822001451725.png)







## ref

![image-20220910223512145](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220910223512145.png)

一个python对象被引用的时候ob_refcnt + 1

如果该对象减少一个引用的时候，则ob_refcnt - 1

比如说：

![image-20220912095541557](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220912095541557.png)





python3中不存在引用的说法

```python
red = 999
green = 888

def f():
    red = red + 1

f()
```

```
UnboundLocalError: local variable 'red' referenced before assignment
```



这里的referenced只是的取变量对应的值





## slot

![image-20220908095829386](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220908095829386.png)







## stmt

statement

an instruction that a Python interpreter can execute





## Suite

A group of individual statements, which make a single code block are called suites in Python.

Header lines begin the statement (with the keyword) and terminate with a colon (: ) and are followed by one or more lines which make up the suite. 



```python
if expr1==True:
  stmt1
  stmt2
```





## symtable

https://eli.thegreenplace.net/2010/09/18/python-internals-symbol-tables-part-1/

![image-20220828203230431](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220828203230431.png)



https://eli.thegreenplace.net/2010/09/20/python-internals-symbol-tables-part-2

![image-20220828203051815](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220828203051815.png)







## sys.getsizeof()

python2

```python
print sys.getsizeof(1) # 24
print sys.getsizeof(1l) # 28
```



```
int = pyobject_head + long = 20 + 4
long = pyobjecy_var_head + unsigh short*
	 = pyobject_head + ob_size + unsigh short* 
	 = 20 + 4 + 4 + 28
```











## typeObject

每个Object都有，用来表明type

包括申请内存、相关function等meta-information







## testlist

用`,`隔开的序列





```python
for i in 1,2,3:
    print i
```



```python
# error：参数列表不一样
print(type(1,2,3,4,5))
```





## varnames

变量名表





## Var Object

![image-20220818102051244](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220818102051244.png)





![image-20220818102324082](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220818102324082.png)![image-20220818102428257](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220818102428257.png)

![image-20220818104743139](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220818104743139.png)



![image-20220818103033036](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220818103033036.png)







## void(0)

null



## unary binary inplace 

unary => 一元，如: 负数-、取反~等

binary => 二元

inplace =>就地操作











## weak ref

![image-20220907010203957](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220907010203957.png)









# Compile

`compile.c`

![image-20220909231937202](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220909231937202.png)









## command

```
python -m dis 2.py
```









## index

```python
a = 999
b = 999+998
d = "h"
c = 1000
```





## LOAD_FAST

```c
TARGET(LOAD_FAST)
{
    x = GETLOCAL(oparg);
    if (x != NULL) {
        Py_INCREF(x);
        PUSH(x);
        FAST_DISPATCH();
    }
    format_exc_check_arg(PyExc_UnboundLocalError,
                         UNBOUNDLOCAL_ERROR_MSG,
                         PyTuple_GetItem(co->co_varnames, oparg));
    break;
}
```

```c
TARGET(LOAD_CONST)
{
	x = GETITEM(consts, oparg);
	Py_INCREF(x);
	PUSH(x);
	FAST_DISPATCH();
}
```

区别在于，一个是直接再local中拿，一个是在consts中拿









## optimize

![image-20220907003800206](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220907003800206.png)









## no matter fail

报错的代码也会把字节码给编出来（运行时报错，不是编译的报错）

![image-20220912102649055](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220912102649055.png)







## number+

![image-20220828200236499](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220828200236499.png)







![image-20220828235707513](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220828235707513.png)



```python
a = 666+666
```

![image-20220828235816873](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220828235816873.png)







## return 0



return之前的`LOAD_CONST`

表示当前Suite执行完毕









## VISIT

对应的visit方法

简单地说是把某个量push入栈









# Computer



## Memory

![image-20220812104258814](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220812104258814.png)







# Comprehension

速度比for循环+append快得多！

然后，不需要掌握复杂的，可读性不好

一层循环就够了



```python
def f1():
    lst = []
    for i in range(10000000):
        lst.append(i)

def f2():
    lst = [i for i in range(10000000)]

import cProfile
cProfile.run('f1()')
cProfile.run('f2()')
```

```
   ncalls  tottime  percall  cumtime  percall filename:lineno(function)
        1    0.127    0.127    1.780    1.780 <string>:1(<module>)
        1    0.997    0.997    1.653    1.653 t.py:1(f1)
        1    0.000    0.000    1.780    1.780 {built-in method builtins.exec}
 10000000    0.656    0.000    0.656    0.000 {method 'append' of 'list' objects}
        1    0.000    0.000    0.000    0.000 {method 'disable' of '_lsprof.Profiler' objects}


         5 function calls in 0.499 seconds

   Ordered by: standard name

   ncalls  tottime  percall  cumtime  percall filename:lineno(function)
        1    0.078    0.078    0.499    0.499 <string>:1(<module>)
        1    0.000    0.000    0.421    0.421 t.py:6(f2)
        1    0.421    0.421    0.421    0.421 t.py:7(<listcomp>)
        1    0.000    0.000    0.499    0.499 {built-in method builtins.exec}
        1    0.000    0.000    0.000    0.000 {method 'disable' of '_lsprof.Profiler' objects}
```



```python
numbers = [run_calculation(i) for i in range(10)]
```





## list

```python
lst = [i for i in range(100000000)]
```

```python
lst = [i for i in range(100000000) if i%2 ==0]
```





## dict

```python
D = {x: x**2 for x in range(5)}
```



```python
D = {0: 'A', 1: 'B', 2: 'C', 3: 'D', 4: 'E', 5: 'F'}
selectedKeys = [0, 2, 5]

X = {k: D[k] for k in selectedKeys}
```







## set

```python
a={x for x in range(5)}
```











# Dict

Dictionaries and sets use hash tables to achieve their O(1) lookups and insertions.  





![image-20220823172037306](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220823172037306.png)



entry 是dict内的每一个键值对

![image-20220823171609158](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220823171609158.png)





## Create

```python
d = {v: k for k, v in xx}
```







## Index

![image-20220823172803442](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220823172803442.png)





![image-20220823163552110](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220823163552110.png)



![image-20220823165856496](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220823165856496.png)



![image-20220823164605841](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220823164605841.png)







## ordered

![image-20221022104822018](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20221022104822018.png)

为什么现在的dict有序

因为是挨个存的

![image-20221022105023896](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20221022105023896.png)



而不是似set的一张散列表





## swap

交换key和value

```python
 my_dict = {1: 'a', 2: 'b', 3: 'c'}
    
 swapped = {v: k for k, v in my_dict.items()}
 swapped = dict((v, k) for k, v in my_dict.iteritems())
 swapped = dict(zip(my_dict.values(), my_dict))
 swapped = dict(zip(my_dict.values(), my_dict.keys()))
 swapped = dict(map(reversed, my_dict.items()))
```







# Exception



```python
class EvenOnly(list):
	def append(self, integer):
		if not isinstance(integer, int):
			raise TypeError("Only integers can be added")
		if integer % 2:
			raise ValueError("Only even numbers can be added")
		super().append(integer)
```



```
>>> e = EvenOnly()
>>> e.append("a string")
Traceback (most recent call last):
File "<stdin>", line 1, in <module>
File "even_integers.py", line 7, in add
raise TypeError("Only integers can be added")
TypeError: Only integers can be added
```



When an exception is raised, it appears to stop program execution immediately.  







## args

```python
try:
	raise ValueError("This is an argument")
except ValueError as e:
	print("The exception arguments were", e.args)
```

![image-20221011094753557](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20221011094753557.png)



## else

```python
try:
	choice = random.choice(some_exceptions)
	print("raising {}".format(choice))
	if choice:
	raise choice("An error")
except ValueError:
	print("Caught a ValueError")
except TypeError:
	print("Caught a TypeError")
except Exception as e:
	print("Caught some other error: %s" % ( e.__class__.__name__))
else:
	print("This code called if there is no exception")
finally:
	print("This cleanup code is always called")
```







## finally

```python
try:
	choice = random.choice(some_exceptions)
	print("raising {}".format(choice))
	if choice:
	raise choice("An error")
except ValueError:
	print("Caught a ValueError")
except TypeError:
	print("Caught a TypeError")
except Exception as e:
	print("Caught some other error: %s" % ( e.__class__.__name__))
else:
	print("This code called if there is no exception")
finally:
	print("This cleanup code is always called")
```







## own exception



```python
class InvalidWithdrawal(Exception):
	def __init__(self, balance, amount):
		super().__init__("account doesn't have ${}".format(amount))
		self.amount = amount
		self.balance = balance
raise InvalidWithdrawal(25, 50)
```



```python
try:
	raise InvalidWithdrawal(25, 50)
except InvalidWithdrawal as e:
	print("I'm sorry, but your withdrawal is more than your balance by ${}".format(e.overage()))
```





##  try-expect

The problem will not be stopped 

```python
try:
	no_return()
except:
	print("I caught an exception")
print("executed after the exception")
```





Note the indentation around try and except.

 The try clause wraps any code that might throw an exception.  

回调





We can even catch two or more different exceptions and handle them

```python
def funny_division2(anumber):
	try:
		if anumber == 13:
			raise ValueError("13 is an unlucky number")
		return 100 / anumber
	except (ZeroDivisionError, TypeError):
		return "Enter a number other than zero"
```













## multi-expect

```python
try:
	choice = random.choice(some_exceptions)
	print("raising {}".format(choice))
	if choice:
	raise choice("An error")
except ValueError:
	print("Caught a ValueError")
except TypeError:
	print("Caught a TypeError")
```











# for

![image-20220923141359247](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220923141359247.png)



![image-20220923142957328](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220923142957328.png)





说白了，for循环真的就是重复





## who is faster

```python
def f():
    for i in range(100000000):
        pass
def w():
    i = 0
    while i < 100000000:
        i += 1

import profile

profile.run("f()")
profile.run("w()")
```



```
         5 function calls in 1.125 seconds

   Ordered by: standard name

   ncalls  tottime  percall  cumtime  percall filename:lineno(function)
        1    0.000    0.000    1.125    1.125 :0(exec)
        1    0.000    0.000    0.000    0.000 :0(setprofile)
        1    0.000    0.000    1.125    1.125 <string>:1(<module>)
        1    1.125    1.125    1.125    1.125 for-while.py:1(f)
        1    0.000    0.000    1.125    1.125 profile:0(f())
        0    0.000             0.000          profile:0(profiler)


         5 function calls in 3.281 seconds

   Ordered by: standard name

   ncalls  tottime  percall  cumtime  percall filename:lineno(function)
        1    0.000    0.000    3.281    3.281 :0(exec)
        1    0.000    0.000    0.000    0.000 :0(setprofile)
        1    0.000    0.000    3.281    3.281 <string>:1(<module>)
        1    3.281    3.281    3.281    3.281 for-while.py:4(w)
        0    0.000             0.000          profile:0(profiler)
        1    0.000    0.000    3.281    3.281 profile:0(w())
```



for 比while快太多了。。



```python
  1           0 LOAD_NAME                0 (range)
              2 LOAD_CONST               0 (100000000)
              4 CALL_FUNCTION            1
              6 GET_ITER
        >>    8 FOR_ITER                 4 (to 14)
             10 STORE_NAME               1 (i)

  2          12 JUMP_ABSOLUTE            8

  4     >>   14 LOAD_CONST               1 (0)
             16 STORE_NAME               1 (i)

  5     >>   18 LOAD_NAME                1 (i)
             20 LOAD_CONST               0 (100000000)
             24 POP_JUMP_IF_FALSE       36

  6          26 LOAD_NAME                1 (i)
             28 LOAD_CONST               2 (1)
             30 INPLACE_ADD
             32 STORE_NAME               1 (i)
             34 JUMP_ABSOLUTE           18
        >>   36 LOAD_CONST               3 (None)
             38 RETURN_VALUE

```

比较宏观的一个解释是while的汇编要比for的汇编复杂







# function

```
<class 'function'>
<class 'builtin_function_or_method'>
```









## args

```python
def f(*args):
    print(type(args))

f(1, 2, 3) # tuple
```

```python
def f(*args, **kwargs):
    print(kwargs["height"])

f(1, 2, 3, height=100)
```



注意：重要的是星号，args只是变量名，可修改



python2.7

![image-20221124105844946](C:\Users\10201\AppData\Roaming\Typora\typora-user-images\image-20221124105844946.png)



python3.8

![image-20221124110226818](C:\Users\10201\AppData\Roaming\Typora\typora-user-images\image-20221124110226818.png)







## Nested function

Stack 结构





![image-20220829002937657](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220829002937657.png)






## Interesting

```python
def f():
    print(99)


f = 1
print(f)
```



## recursion

![image-20221124110059864](C:\Users\10201\AppData\Roaming\Typora\typora-user-images\image-20221124110059864.png)





## scope

![image-20221124104850229](C:\Users\10201\AppData\Roaming\Typora\typora-user-images\image-20221124104850229.png)



enclose：

函数里定义一个函数，那么enclose就是内函数外的命名空间

再就是在类里面定义一个函数，函数外，类内的命名空间











# Float

![image-20220824163821631](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220824163821631.png)







## String to Float



Ps:需要一位一位遍历的

![image-20220824165627136](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220824165627136.png)









![image-20220912171354414](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220912171354414.png)



## print

**print的并不一定是实际存的**

![image-20220912143421146](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220912143421146.png)



python3

```python
print(0.300000000000000004)
# 0.3
```



```python
print(0.30000000000000004)
# 0.30000000000000004
```

17位





python2.7

```python
print 0.3000000000004
# 0.3
```

```python
print 0.300000000004
# 0.300000000004
```

12位



![image-20220912142907529](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220912142907529.png)





C 库函数

```c
int snprintf(char *str, size_t size, const char *format, ...)
```

按照 format 格式化成字符串，并将字符串复制到 str 中，size 为要写入的字符的最大数目，超过 size 会被截断。



```c
/* Have PyOS_snprintf do the hard work */
    PyOS_snprintf(buffer, buf_size, format, d);
```

double值按照format去解析

然后把结果放到buffer里

（稀奇古怪的输出结果都是在这个函数里面。。但它是c的库函数。。。我觉得没有再往下研究的必要了）









```python
print 1.300000000004
# 1.3
```



小数减少一位

```python
print 1.30000000004
# 1.30000000004
# 1个整数+1个.+11位小数 = 13
```



```python
print 5.30000000004
# 5.30000000004
# 1+1+11 = 13
```

是因为申请的buffer就这么大

```python
print 10.30000000004
# 10.3
# 2+1+11 = 14 > 13 最后面的4被截断，然后除去多余的0
```



```python
print -1.30000000004
# -1.30000000004
# 1+1+1+11 = 14 ok 因为符号和数字不同处理的
```







```c
#define PyFloat_STR_PRECISION 12
```





```python
print(1.00)
# 1.0
```

![image-20220912143310143](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220912143310143.png)



further

```python
print(str(0.10000000000000001))
# 0.1
```



```python
print(str(0.1000000000000001))
# 0.1000000000000001
```











## 0.1+0.2!=0.3

两个误差

一个误差

```python
print(0.1+0.2 == 0.3)
```





```python
print(0.3) # 0.3
print(0.29999999999999999) #0.3
```



```python
0.30000000000000004
0.10000000000000001
0.20000000000000001

0.29999999999999999
```

















# if



比较运算符的结果是True或者False



and、or 的结果是栈顶元素！而不是True或者False

```python
print(True and "") # ""
```





然后if 栈顶元素的时候，则是

![image-20220916153334550](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220916153334550.png)











# Integer

**different in interact terminal**









# iterator

```python
class gg():
    # iter()返回值
    def __iter__(self):
        return self
    # 迭代next
    def __next__(self):
        return 999
```









## Byte

```c
typedef struct {
    PyObject_HEAD 
    long ob_ival; 
} PyIntObject; 
```



```c
struct _longobject {
	PyObject_VAR_HEAD   
	digit ob_digit[1]; 
}; 					  
```



![image-20220910220254778](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220910220254778.png)





## Create

![image-20220818103459613](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220818103459613.png)



![image-20220823173606048](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220823173606048.png)

```python
a = 10
print(id(a))

a += 10
print(id(a))

# 输出
2265003682384
2265003682704
```



![image-20220829004256082](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220829004256082.png)



![image-20220829004633348](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220829004633348.png)









## Compare

![image-20220818105009850](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220818105009850.png)







## Constant





## intern

`python3.9.6`的优化

![image-20220913013104725](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220913013104725.png)







## int()

![image-20220914093218199](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220914093218199.png)



![image-20220914093229851](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220914093229851.png)









## Init

![image-20220823175023720](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220823175023720.png)





## Object Meta-data

![image-20220823173829465](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220823173829465.png)![image-20220823173807342](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220823173807342.png)

![image-20220823173849213](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220823173849213.png)







可变对象

```c
typedef struct {
    PyObject ob_base;
    Py_ssize_t ob_size; /* Number of items in variable part */
} PyVarObject;
```

为什么int也是可变对象呢？

因为python 的大数机制

```python
import sys

print(sys.getsizeof(4000))
print(sys.getsizeof(999999999999999999))
```

output:

```
28
32
```











## Small Int

![image-20220823084031141](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220823084031141.png)



![image-20220823084219648](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220823084219648.png)





```c
struct _intblock {
	struct _intblock *next;
	PyIntObject objects[N_INTOBJECTS];
};
```





## sizeof

![image-20220910211016960](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220910211016960.png)



![image-20220910212703897](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220910212703897.png)













## +

![image-20220818105213076](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220818105213076.png)







![image-20220818111819810](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220818111819810.png)





## Small Int

如果是会被频繁使用的small int的话，则不再重新申请内存

```python
a = 10
b = int(10.0)

print(id(a))
print(id(b))
```

output:

```
2136571865680
2136571865680
```



small int 的范围[-5, 256]

![image-20220818144334419](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220818144334419.png)

![image-20220818144452626](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220818144452626.png)



如果不是small int的话

```python
a = 10000
b = int(10000.0)

print(id(a))
print(id(b))
```

output:

```
1775767656144
1775764920624
```











为什么要有对象池

![image-20220818111915501](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220818111915501.png)



修改python源码

![image-20220818112240243](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220818112240243.png)



具体过程

![image-20220818112549467](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220818112549467.png)



![image-20220818140616581](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220818140616581.png)



![image-20220818140445960](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220818140445960.png)

Ps：返回的是指针



如果不是small int，则新申请内存，不再用池

![image-20220818140949866](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220818140949866.png)







# keyword





## del

并不是直接释放内存！！！

![image-20220912111239395](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220912111239395.png)



```python
lst = [1,2,3,4,5]
lst1 = lst

del lst
print lst1
```





## nolocal

非局部声明变量指代的已有标识符是最近外面函数的已声明变量，但是不包括全局变量。

```python
count = 1

def a():
    count = 'a函数里面'  　　#如果不事先声明，那么函数b中的nonlocal就会报错
    def b():
        nonlocal count
        print(count)
        count = 2
    b()
    print(count)

if __name__ == '__main__':
    a()
    print(count)
```





## raise

像Java里的throw





## yield

v.出产

生成器

`yield` 是一个类似 `return` 的关键字，只是这个函数返回的是个生成器。



```python
def f():
    for i in range(10):
        yield i

a = f()
```

```python
  1           0 LOAD_CONST               0 (<code object f at 0x000001AE1E313660, file "t.py", line 1>)
              2 LOAD_CONST               1 ('f')
              4 MAKE_FUNCTION            0
              6 STORE_NAME               0 (f)

  5           8 LOAD_NAME                1 (print)
             10 LOAD_NAME                0 (f)
             12 CALL_FUNCTION            0
             14 LOAD_METHOD              2 (__next__)
             16 CALL_METHOD              0
             18 CALL_FUNCTION            1
             20 POP_TOP
             22 LOAD_CONST               2 (None)
             24 RETURN_VALUE

Disassembly of <code object f at 0x000001AE1E313660, file "t.py", line 1>:
  2           0 LOAD_GLOBAL              0 (range)
              2 LOAD_CONST               1 (10)
              4 CALL_FUNCTION            1
              6 GET_ITER
        >>    8 FOR_ITER                10 (to 20)
             10 STORE_FAST               0 (i)

  3          12 LOAD_FAST                0 (i)
             14 YIELD_VALUE
             16 POP_TOP
             18 JUMP_ABSOLUTE            8
        >>   20 LOAD_CONST               0 (None)
             22 RETURN_VALUE

```





![image-20220923150008408](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220923150008408.png)



`yield`说白了，就是作 return 把一个值返回之后，继续那个function的执行



![image-20220923150201530](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220923150201530.png)



我们所谓的挂起，就是说所有局部状态都会被保留下来，包括局部变量的当前绑定、指令指针、内部求值栈和任何异常处理等等。 









# Long

https://www.codementor.io/@arpitbhayani/how-python-implements-super-long-integers-12icwon5vk

```python
struct _longobject {
	PyObject_VAR_HEAD
	digit ob_digit[1];
};
```



![image-20220914102218285](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220914102218285.png)





fromstring

![image-20220914110204455](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220914110204455.png)





```python
print long("bbbbb", 16)
```

```python
print long("zzzzz", 36)
```











```
BASE = 2**15 = 1<<15
```



```python
import math
print(math.log(10)/math.log(1<<15)) # 0.22146187299249084
```



```python
print sys.getsizeof(1073741823l) # 28
print sys.getsizeof(1073741824l) # 32
```





`scan` - `str` < 5

最大的35进制数`9999` = 397224



```python
print 2**15 # 32768
print 2**16 # 65536

```





![image-20220914144129797](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220914144129797.png)





```
PyLong_BASE = 2**15 = 32768
```







## bit_length

有效bits的长度



![image-20220914141931549](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220914141931549.png)



msd

![image-20220914142355502](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220914142355502.png)



`ob_digit[0]`是低位











## sizeof

![image-20220914141437580](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220914141437580.png)



24+2x2

​	



## sign?







## int and long

```python
print sys.getsizeof(2**30) # 24
print type(2**30) # int

print sys.getsizeof(2**31) # 32
print type(2**31) # long
```







## fromstring

![image-20220914151701426](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220914151701426.png)

![image-20220914151835010](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220914151835010.png)



![image-20220914152128108](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220914152128108.png)



Ps: 1<<15

1是到了第16位，2**15

没有浪费

然后

```c
#define PyLong_BASE	((digit)1 << PyLong_SHIFT)
#define PyLong_MASK	((digit)(PyLong_BASE - 1))
```

mask是15位全1

剩下的一位，继承于`c>>=15`

**也就间接实现了2^15进制** 好好理解！

2^15（100...0）正好取不到



`convmultmax=10000`

`convwidth=4`





twodigits twodigits地处理 long是足够不溢出的



![image-20220914153256130](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220914153256130.png)

叠加是指1000和100叠加成100000

然后把低位放到digit[0]

右移c后把高位放到digit[1]



`ob_digit[0]`是低位





## long to string

![image-20220914154034628](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220914154034628.png)











# List

![image-20220822224903763](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220822224903763.png)





## Create

![image-20220901150220813](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220901150220813.png)

![image-20220824095533523](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220824095533523.png)



```python
list()
```

![image-20220908100618288](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220908100618288.png)

![image-20220908102148324](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220908102148324.png)







![image-20220908100835287](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220908100835287.png)



就是对应一个结构体———listType

list独有的一些function都在这（还有list对象创建、维护所需的一些字段）

![image-20220908101021903](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220908101021903.png)









## Access

`lst `和`lst[0]` 、`lst[:]`的区别

没啥区别，都是`PyObject*`

切片其实不会新建intobject









## String to List

为什么没有FromString

因为可以用extend完美等效实现



因为有new一个List，所以这个操作还是相对耗时的

![image-20220824170818187](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220824170818187.png)







这也是下面报错的原因（extend() 的对象一定要是iterable）

![image-20220824100513252](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220824100513252.png)









## Change value

![image-20220822231033293](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220822231033293.png)





## del

```python
del lst[1]
```



![image-20220912101903987](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220912101903987.png)

(不需要重新push() 因为这里不是`slice`操作，而是`slice`赋值，二者完全不是一个东西, slice赋值是在原list的基础上进行修改)

![image-20220912101840551](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220912101840551.png)

![image-20220912101813845](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220912101813845.png)



![image-20220912101742369](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220912101742369.png)





## extend

![image-20220912100913951](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220912100913951.png)

![image-20220912100851321](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220912100851321.png)









## List and Tuple

Python stores data in these buckets by reference

which means the number itself simply points to or refers to the data we actually care about.

As a result, these buckets can store any type of data we want (as opposed to numpy arrays

which have a static type and can store only that type of data).





## Overallocation

![image-20220816160111042](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220816160111042.png)

For example, if you create a list with 8,000 elements using appends,

Python will allocate space for about 8,600 elements, overallocating 600 elements! 

（It is for reduce the time for reallocate, but it actually do cost the extra resource）





**Why mention Overallocation?**



**1.time for copy**

we can reduce the number of times this allocation must happen and thus the total number of memory copies that are necessary. 

This is important since memory copies can be quite expensive, especially when list sizes start growing.   

![image-20220816160356867](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220816160356867.png)



**2.extra memory**

A list of size 100,000,000 created with any append operation actually uses 112,500,007 elements’ worth of memory 

（Because when it do the append(),  it already allocate 112,500,007 lements’ worth of memory ）







**Then what about the Tuple?**

a tuple holding the same data will only ever use exactly 100,000,000 elements’ worth of memory.

This makes tuples lightweight and preferable when data becomes static.  





**Furthermore**

even if we create a list without append (and thus we don’t have the extra headroom introduced by an append operation)

it will still be larger in memory than a tuple with the same data. 

This is because lists have to keep track of more information about their current state in order to efficiently resize. 

like current size etc

While this extra information is quite small (the equivalent of one extra element)

it can add up if several million lists are in use.  



## Negative index

slice中的index调整

```python
	if (*start < 0) {
        *start += length;
        if (*start < 0) {
            *start = (step < 0) ? -1 : 0;
        }
    }
```



```python
lst = [1,2,3,4]
```

-1

-1+4 = 3

刚好就是最末位



再就是之后的if判断

其实是在处理当step小于0，反向的时候，stop位是否+1









## Tuple and GC

Tuples is something Python does in the background: resource caching. 

Python is garbage collected, which means that when a variable isn’t used anymore

Python frees the memory used by that variable, giving it back to the operating system for use in other applications

 (or for other variables)

For tuples of sizes 1–20, however, when they are no longer in use

the space isn’t immediately given back to the system: up to 20,000 of each size are saved for future use.

This means that when a new tuple of that size is needed in the future

we don’t need to communicate with the operating system to find a region in memory to put the data

since we have a reserve of free memory already. 

However, this also means that the Python process will have some extra memory overhead.  





## Time to create List and Tuple

```
>>> %timeit l = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
95 ns ± 1.87 ns per loop (mean ± std. dev. of 7 runs, 10000000 loops each)

>>> %timeit t = (0, 1, 2, 3, 4, 5, 6, 7, 8, 9)
12.5 ns ± 0.199 ns per loop (mean ± std. dev. of 7 runs, 100000000 loops each)
```







## Pointer and Copy

```py
a = [1000, 2000]

print(id(a))
print(id(a[0]))
```

尝试思考输出的两个值分别是什么

- ListObject的address
- a[0]指向的内存的address，而不是a[0]的这个指针的地址



**a[0]是个Pointer！！！**

**所以! `id()` 其实是取指针的值**

![image-20220822234039747](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220822234039747.png)



```python
a = [1000, 2, 3]
b = a.copy()

a[0] = 10000

print(a)
print(b)
```



List中存的确实是指针

但是注意！



**只是修改了`a[0]`的pointer**

**并不是修改`a[0]` pointer的指向**

好好理解上面两句话！！！



再看：

```python
a = [1000, 2, 3]
b = a

a[0] = 10000

print(a)
print(b)

# 输出
[10000, 2, 3]
[10000, 2, 3]
```

这里是a和b指向同一个ListObject

a[0] = 10000 会影响a和b列表





再看！

```python
a = [[1,2,3], 2, 3]
b = a.copy()

a[0][0] = 10000
a[1] = 1000

print(a)
print(b)

# 输出
[[10000, 2, 3], 1000, 3]
[[10000, 2, 3], 2, 3]
```

`copy()`是 shallow copy 

只是单纯copy全部pointer，包括List里面的List



deep copy则是会确实重新构建一个List





## Overallocate

![image-20220818133303696](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220818133303696.png)

![image-20220818133908082](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220818133908082.png)





## append

![image-20220818134207085](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220818134207085.png)







## insert

![image-20220818134424126](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220818134424126.png)





## index -1

![image-20220910223902808](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220910223902808.png)













## Clear

![image-20220822223821775](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220822223821775.png)



## Remove（不推荐使用）

![image-20220822225314640](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220822225314640.png)



另外后续还有切片相关的操作。。也耗时的











## Pop

pop的核心其实只是修改ob_size

![image-20220822225726962](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220822225726962.png)







## Iteration

![image-20220823162436558](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220823162436558.png)







## Slice

![image-20220901143330354](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220901143330354.png)





```python
lst = [1, 2, 3, 4, 5]
lst[0:2][0] = 999

print(lst) # [1, 2, 3, 4, 5]
```

因为这只是在把`t`内的指针给替换了

**原指针的指向关系并没有发生改变**



Ps!!!!!

![image-20220901153447402](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220901153447402.png)

```python
# 切片赋值
lst = [1, 2, 3, 4, 5]
lst[0:2] = [99, 99]

print(lst) # [99, 99, 3, 4, 5]
```



```python
lst = [1,2,3,4]
lst[0:2] = [1,2,3,4,5,6,7]
print(lst) # [1, 2, 3, 4, 5, 6, 7, 3, 4]
```

解释如下：

![image-20220902094347411](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220902094347411.png)



再看：

```python
lst = [1,2,3,4]
lst[0:] = [5,6,7]
print(lst) # [5, 6, 7]
```

![image-20220902094729701](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220902094729701.png)

`lst[0:]`则表示是要把整个`lst`重新赋值

也就理所当然的原List的1234全没了





对于恶意的范围

![image-20220824170005377](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220824170005377.png)







## subscript



## sizeof

是会计算ob_item指向的那块内存的字节大小的











## Print

![image-20220824094800242](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220824094800242.png)







# Operator

## *

![image-20220924170604254](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220924170604254.png)

这里找到List对应的repeat方法

![image-20220924170832107](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220924170832107.png)







# Profiling

```
python -m cProfile -s cumulative 3.py
```

```
         12033 function calls in 10.707 seconds

   Ordered by: cumulative time

   ncalls  tottime  percall  cumtime  percall filename:lineno(function)
        1    0.000    0.000   10.707   10.707 {built-in method builtins.exec}
        1    0.002    0.002   10.707   10.707 3.py:5(<module>)
       11   10.702    0.973   10.702    0.973 {built-in method builtins.input}
     7776    0.001    0.000    0.001    0.000 3.py:21(exist)
        7    0.001    0.000    0.001    0.000 {built-in method builtins.print}
     1626    0.000    0.000    0.000    0.000 {method 'remove' of 'list' objects}
     1312    0.000    0.000    0.000    0.000 {method 'append' of 'list' objects}
     1296    0.000    0.000    0.000    0.000 {built-in method builtins.len}
        2    0.000    0.000    0.000    0.000 {built-in method time.time}
        1    0.000    0.000    0.000    0.000 {method 'disable' of '_lsprof.Profiler' objects}
```



`tottime` 函数本身所花费的时间

`cumtime` 函数本身所花费的时间+其中调用其他函数的时间（调用函数的时候，cur就转到其他函数中了）







## permutation

自己写的

```python
# 23.917
for i in range(1000):
    for j in range(1000):
        if i == j:
            continue
        print(i,j)
```



permutation 库

```python
# 24.786

from itertools import permutations

for i in permutations(list(range(1000)), 2):
    print(i)
```



稍微快一点，时间应该花在了permutations 的元组创建

再就是，也意识到，permutations 应该是迭代生成

不是事先全部存好













# Range



## Iter

![image-20220830132253776](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220830132253776.png)

所以！

`range()`其实并没有一次性生成一个序列！

只是每次返回一个`intobject`



Example

```python
lst = [1, 2, 3, 4, 5]
for i in range(len(lst)):
    lst.pop()

print(lst)


# output
[]
```

`range()`不会重复执行

这一行`for`语句，其实只是在推动`iterator`





## range 和 slice



```python
lst = [1,2,3,4,5]
print(lst[len(lst)-1:-1:-1])
for i in range(len(lst)-1,-1,-1):
    print(i)

# output
[]
4
3
2
1
0
```



range能正常输出，但是slice不行

先看range的实现

```c++
static PyObject *
rangeiter_next(rangeiterobject *r)
{
    if (r->index < r->len)
        /* cast to unsigned to avoid possible signed overflow
           in intermediate calculations. */
        return PyLong_FromLong((long)(r->start +
                                      (unsigned long)(r->index++) * r->step));
    return NULL;
}
```

每个值都是新计算出来的，直到stop为止

所以range都输出出来了







# String



## Compare

首先是对比较双方两边的数据类型的确认

![image-20220818180437920](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220818180437920.png)



其次，看a、b的地址

![image-20220818180350693](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220818180350693.png)



![image-20220818180158542](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220818180158542.png)



再对于单纯的比较==

![image-20220818175355624](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220818175355624.png)



memcmp

```
如果返回值 < 0，则表示 str1 小于 str2
如果返回值 > 0，则表示 str1 大于 str2
如果返回值 = 0，则表示 str1 等于 str2
```





最后

![image-20220818182840543](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220818182840543.png)





## Int to String

![image-20220818183138878](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220818183138878.png)





## + and join()

多字符串时，尽量避免使用+ —— 会调用`string_concat()`

![image-20220822235509102](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220822235509102.png)

![image-20220823000448297](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220823000448297.png)



**join**

![image-20220823000942352](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220823000942352.png)

```python
a = ''.join(["hell", "o"])
```

![image-20220823001028210](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220823001028210.png)





## hash

![image-20220913010547399](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220913010547399.png)

取实际值做hash

所以即使对象的id不一样

但他们hash 的结果是一样的





## interesting

```python
a = "111"
b = "11"+"1"

print(id(a))
print(id(b))
```

这是Python编译时的优化，常量直接计算出来

再看：

```python
a = "111"
t = "1"
b = "11" + t

print(id(a)) # 2317899936048
print(id(b)) # 2317899869040
```



”+“ 的原理（其实也是优化的结果）

![image-20220901115713035](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220901115713035.png)



## intern

是在`compile.c`中生产字节码文件时完成的

(int的hash是它的long value)

![image-20220909232146864](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220909232146864.png)



解析源代码的时候确实是一个个都放到List里的

但是转化成dict的consts时，优化掉了重复的，做了引用-1

![image-20220912224924690](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220912224924690.png)



然后这个是把dict转tuple做常量表用

![image-20220912230552236](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220912230552236.png)



optimize可能要删改，转成了List

![image-20220912230918094](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220912230918094.png)





优化完了又转回来了

Ps: 因为是List转Tuple

所以这里没有去重复优化！！！

![image-20220912230841370](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220912230841370.png)









## len

python 2中，字符串是有长度限制的

![image-20220821210401183](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220821210401183.png)



len()不需要便利整个字符串

![image-20220821213138627](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220821213138627.png)





单字符才会用到这个characters的池

![image-20220821223435366](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220821223435366.png)





例子：

```python
n = 123
a = str(n)
b = str(n)

print(id(a))
print(id(b))

# 输出
2321637949768
2321639465176
```





```python
n = "123"
a = str(n)
b = str(n)

print(id(a))
print(id(b))

# 输出
2344578105672
2344578105672
```



为什么！？

fromString

![image-20220821211446609](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220821211446609.png)



因为FromString的时候是直接拷贝str的内存数据



![image-20220821214527967](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220821214527967.png)







print string

![image-20220821213028574](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220821213028574.png)





python源码也这样，哈哈哈！

![image-20220821213408548](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220821213408548.png)





concat 实现

```python
memcpy(PyBytes_AS_STRING(*pv) + oldsize, wb.buf, wb.len);
```









## Short strings



![image-20220822235232971](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220822235232971.png)





长度为1的字符串会有share处理

![image-20220818174310557](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220818174310557.png)

![image-20220818174423273](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220818174423273.png)







## Strip

common case

do-while on left-end  and right-ebd

then return a string object

![image-20220909143031828](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220909143031828.png)



The given specified `str `as separator

![image-20220909143752109](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220909143752109.png)





## split



### Byte

```python
import sys

a = ''.split()
b = []

print sys.getsizeof(a) # 160
print sys.getsizeof(b) # 64
```



```python
import sys

a = ''.split()
b = [0]

print sys.getsizeof(a) # 160
print sys.getsizeof(b) # 72
```



```python
import sys

a = ''.split()
b = [0]*12

print sys.getsizeof(a) # 160
print sys.getsizeof(b) # 160
```





### parameter

```python
a = 'hello     world'.split()
print(a)

# ['hello', 'world']
```



```python
a = 'hello     world'.split(' ')
print a

# ['hello', '', '', '', '', 'world']
```

为什么！？？





默认split空格whitespace

![image-20220910221846345](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220910221846345.png)



这就是为什么默认时，若干个空格全给切了

![image-20220910221339526](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220910221339526.png)

![image-20220910221632807](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220910221632807.png)



![image-20220910221537149](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220910221537149.png)





![image-20220910222445850](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220910222445850.png)







## Hash

![image-20220824173739289](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220824173739289.png)













# Set



![image-20220830133520638](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220830133520638.png)

```
PySet_MINSIZE = 8
```







## add()

![image-20220830133743812](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220830133743812.png)





## compare++

!!?

```python
s1 = set((1, 2, 3, 4, 5))
s2 = set((2, 3, 4))

print(s1 > s2)

# output
True
```





![image-20220830153650050](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220830153650050.png)





## Create

![image-20220830140033271](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220830140033271.png)



也就是说，可迭代的对象都可以放进来生成Set

iter相关的代码：

![image-20220830140207930](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220830140207930.png)



![image-20220830140137877](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220830140137877.png)



## Difference

同上，支持`itertable`对象

![image-20220830153051324](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220830153051324.png)



![image-20220830152840661](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220830152840661.png)









## frozenset

Build an immutable unordered collection of unique elements.









## lookup

![image-20220830134410341](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220830134410341.png)



![image-20220830134701529](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220830134701529.png)





## iter

![image-20220830134843126](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220830134843126.png)

我们经常说Set是无序的

因为hash值映射出来的 `i` 是随机的



## intersection

与`Set`做`intersection`

![image-20220830152258580](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220830152258580.png)![image-20220830152110304](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220830152110304.png)



**与`iterable` 对象做`intersection`**

![image-20220830152237431](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220830152237431.png)





## merge

![image-20220830135118279](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220830135118279.png)







## Print Set

![image-20220830135358956](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220830135358956.png)

根据迭代的顺序

`table[i] `从左往右迭代，但它是无序的噢







## pop()

如果没有指定key的话，则是随机删除一个

你懂的

![image-20220830135713258](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220830135713258.png)









## subSet

![image-20220830153305250](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220830153305250.png)



然后，也支持iterable对象

![image-20220830153445636](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220830153445636.png)









# Tuple

请注意决定生成元组的其实是逗号而不是圆括号。 圆括号只是可选的，生成空元组或需要避免语法歧义的情况除外。



## why tuple

1.不用担心tuple在不知道的地方被修改

2.immutable的tuple可hash，可代替list进行set、dict的应用

3.空间开销







# Python2 Python3 Diff



## type

python3:

![image-20220818105437755](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220818105437755.png)

Python2:

![image-20220818105457749](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220818105457749.png)







## consts 的优化



```python

```



python2

```
  1           0 LOAD_CONST               0 (999)
              2 STORE_NAME               0 (a)

  2           4 LOAD_CONST               1 (1997)
              6 STORE_NAME               1 (b)

  3           8 LOAD_CONST               2 ('h')
             10 STORE_NAME               2 (d)

  4          12 LOAD_CONST               3 (1000)
             14 STORE_NAME               3 (c)
             16 LOAD_CONST               4 (None)
```



python3

```
  1           0 LOAD_CONST               0 (999)
              2 STORE_NAME               0 (a)

  2           4 LOAD_CONST               5 (1997)
              6 STORE_NAME               1 (b)

  3           8 LOAD_CONST               2 ('h')
             10 STORE_NAME               2 (d)

  4          12 LOAD_CONST               3 (1000)
             14 STORE_NAME               3 (c)
             16 LOAD_CONST               4 (None)
             18 RETURN_VALUE

```

