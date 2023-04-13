---
title: django
date: 2023-02-01 15:00:37
tags:
categories:
---



pycharm pro



demo

https://www.youtube.com/watch?v=rHux0gMZ3Eg



## 管理员账号

sqlite3的问题

importError: DLL load failed while importing _sqlite3: 找不到指定的模块



解决方法：

在`anaconda\Library\bin`下找到`sqlite3.dll`

把他放到`anaconda\DLLs`下即可



```
python manage.py migrate
```

```
python manage.py createsuperuser
```

