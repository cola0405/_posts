---
title: Python Class
date: 2021-01-02 23:21:14
tags:
- Python
- Tutorial
categories:
- [Python,Tutorial]
---

simple example: (within the same package)

Speaker.py

```python
class Speaker:
    def sayHello():
        print('hello')
```

Test.py

```python
import Speaker
speaker = Speaker()
speaker.sayHello()
```

If in different package:

Test.py

```python
from packageName.Speaker import Speaker

speaker = Speaker()
speaker.sayHello()
```



You can also build a Constructor to initialize the object

```python
class Speaker:
	name = None
	def __init__(self,name):
    	self.name = name
	
    def sayHello():
        print('hello')
```

---

Generally, we use import like this

Lib.py

```python
def hello(): # this .py file do not have class, so do not need to instantiate
    print('hello')
```

Test.py

```python
import Lib

Lib.hello() 
```

How can we import a class

A class Import other class and use that class's function

Test.py

```python
from packageName.Speaker import Speaker
class Test:
	speaker = Speaker() # you need to instantiate the object, so that you can use it
    def testSpeak():
        speaker.sayHello()
```



