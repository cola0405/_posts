---
title: QT
date: 2022-03-28 23:33:11
tags:
categories:
---



# 报错

## This application failed to start because no Qt platform plugin could be initialized

Copy the following files:

```py
\Anaconda3\Lib\site-packages\PySide2\plugins\platforms\qminimal.dll
\Anaconda3\Lib\site-packages\PySide2\plugins\platforms\qoffscreen.dll
\Anaconda3\Lib\site-packages\PySide2\plugins\platforms\qwindows.dll
```

to:

```py
\Anaconda3\Library\plugins\platforms\
```
