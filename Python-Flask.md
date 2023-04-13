---
title: Python Flask
date: 2021-03-08 20:30:35
tags:
- Python
- Flask
categories:
- [Python,Flask]
---

1.Listener 

```python 
app.run(host='0.0.0.0')
```

2.Template

```python 
from flask import Flask
app = Flask(__name__)

@app.route('/')
def hello_world():
   return 'Hello World'

if __name__ == '__main__':
   app.run(host='0.0.0.0')
```



