---
title: NewPython
date: 2023-04-22 17:40:51
tags:
categories:
---







## cls

`cls`参数是一个类对象，它可以用来访问类的属性或方法。











## exec()

```python
code = """
x = 5
y = 10
print(x + y)
"""
exec(code)
```

输出

```
15
```







## eval()

```python
x = 5
y = 10
code = "x + y"
result = eval(code)
print(result)
```

输出

```
15
```







## lambda 表达式

1. Lambda表达式的语法

Lambda表达式的语法如下：

```python
lambda arguments: expression
```

其中，arguments表示Lambda表达式的参数列表，可以为空或者包含一个或多个参数；expression表示Lambda表达式的函数体，可以是一个表达式或者一段代码块。

例如，下面是一个简单的Lambda表达式：

```python
lambda x: x * x
```

这个Lambda表达式的参数是一个整数x，函数体是返回x的平方。

1. Lambda表达式的应用

Lambda表达式可以应用于各种场景，例如：

- 列表的排序和过滤：

```ini
list1 = [1, 3, 2, 5, 4]
list2 = sorted(list1, key=lambda x: x)
list3 = filter(lambda x: x % 2 == 0, list1)
```

- GUI事件的处理：

```less
button.bind("<Button-1>", lambda event: print("Button clicked!"))
```

- 函数的返回值：

```python
def make_incrementor(n):
    return lambda x: x + n
```

这个函数返回一个Lambda表达式，它的参数是一个整数x，函数体是返回x加上n的结果。

Lambda表达式可以使代码更加简洁、易读、易维护，但也需要注意Lambda表达式的使用场景和适当性。





## 可变参数

可变参数是一种用于接收任意数量参数的语法，它可以接收任意数量的位置参数和关键字参数。可变参数的语法如下：

```python
def function(*args, **kwargs):
    pass
```

其中，args是一个元组，用于接收位置参数；kwargs是一个字典，用于接收关键字参数。例如：

```scss
def my_function(*args, **kwargs):
    print(args)
    print(kwargs)

my_function(1, 2, 3, a=4, b=5)
```

这个例子中，my_function函数接收任意数量的位置参数和关键字参数，并将它们打印出来。

```
(1, 2, 3)
{'a': 4, 'b': 5}
```













## 列表推导式

```python
squares = [x*x for x in range(10)]
even_squares = [x*x for x in range(10) if x % 2 == 0]
```





## 生成器表达式

```python
squares = (x*x for x in range(10))
even_squares = (x*x for x in range(10) if x % 2 == 0)
```





## \_\_slot\_\_

__slots__语句：__slots__语句用于限制类实例可以具有的属性。它的语法如下：

```kotlin
class MyClass:
    __slots__ = ["x", "y"]
```





## @staticmethod、@classmethod区别



@staticmethod 是静态方法

@classmethod 是类方法（同一class的各个对象通用），必须传递`cls`参数（对象则是通过 self 来访问对象内属性）



```python
class Person:
    count = 0

    def __init__(self, name, age):
        self.name = name
        self.age = age
        Person.count += 1

    def get_age(self):
        return self.age

    @classmethod
    def get_count(cls):
        return cls.count

# 通过类名调用类方法
print(Person.get_count())  # 输出 0

# 创建两个 Person 对象
p1 = Person("Alice", 25)
p2 = Person("Bob", 30)

# 再次调用类方法
print(Person.get_count())  # 输出 2
```









## yield

yield说白了，就是作 return 把一个值返回之后，继续那个function的执行

```python
def f():
    for i in range(3):
        print('it is me')
        yield i

for i in f():
    print(i)

```

输出

```
it is me
0
it is me
1
it is me
2
```











## 装饰器

装饰器是一种用于修改函数或类的行为的语法，它可以在不修改函数或类本身的情况下，增加或修改它们的功能。它的语法如下：

```python
@decorator
def function():
    pass
```

其中，decorator是一个函数或类，用于修改function的行为。例如：

```python
def my_decorator(func):
    def wrapper():
        print("Before function is called.")
        func()
        print("After function is called.")
    return wrapper

@my_decorator
def say_hello():
    print("Hello, world!")

say_hello()
```

这个例子中，my_decorator是一个装饰器函数，它用于在say_hello函数被调用前后输出一些信息。
