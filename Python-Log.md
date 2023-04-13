---
title: Python Log
date: 2021-01-03 10:34:15
tags:
- Python
- Tutorial
categories:
- [Python,Tutorial]
---

Sometimes the error messages will be to long 

Then the console is not big enough to display all messages

And we can't see the root cause

The solution is output the error messages to a log file

Here is the example

```python
import traceback
import logging
 
logging.basicConfig(filename='log.log')
 
 
def error_func():
  b = 1 / 0
 
 
if __name__ == '__main__':
  try:
    error_func()
  except:
    s = traceback.format_exc()
    logging.error(s)
```

