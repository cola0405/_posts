---
title: Flask Cors
date: 2021-01-02 19:45:07
tags:
- Config
- Python
categories:
- [Config,Python]
---

Cors solution

```
from flask_cors import *
CORS(app, supports_credentials=True)
```

Then Note ! ! !

Flask default listen on localhost

if you want to use Flask to deploy an application

do the thing below :

```python
app.run(host='0.0.0.0', port=5000, debug=False)
```

