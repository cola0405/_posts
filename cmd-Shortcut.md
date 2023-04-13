---
title: cmd Shortcut
date: 2021-03-08 21:28:30
tags:
- Shortcut 
categories:
- [Shortcut]
---

1.源文件

```
Windows Registry Editor Version 5.00

[HKEY_CLASSES_ROOT\Directory\Background\shell\OpenCMDHere]
"ShowBasedOnVelocityId"=dword:00639bc8

[HKEY_CLASSES_ROOT\Directory\Background\shell\OpenCMDHere\command]
@="cmd.exe /s /k pushd \"%V\""
```



2.想要Windows Terminal 

把其快捷方式放到System32下（即和cmd.exe一起）

然后

```
Windows Registry Editor Version 5.00

[HKEY_CLASSES_ROOT\Directory\Background\shell\OpenCMDHere]
"ShowBasedOnVelocityId"=dword:00639bc8

[HKEY_CLASSES_ROOT\Directory\Background\shell\OpenCMDHere\command]
@="wt.exe cmd.exe /s /k pushd \"%V\""
```

pushd 相当于cd

你也可以在cmd下输入

```
cmd pushd g:
```

相当于

```
cd g:
```

具体原理我不是很想研究。。

会用就好了 这玩意儿



3.进入注册表

win+r

regedit 

你可以根据源代码找到注册表的对应位置



4.这里是微软介绍reg的[文档](https://support.microsoft.com/en-us/help/310516/how-to-add-modify-or-delete-registry-subkeys-and-values-by-using-a-reg)

虽然我看不太懂

简单地说了最上面的version不是简单的注释

而是对应了不同的windows版本

然后下面的是具体的值的设置

你也可以一GUI的形式到regedit下修改