---
title: Android Studio SDK config
date: 2021-03-08 21:39:26
tags:
categories:
---

```
Emulator: emulator: ERROR: Unknown AVD name [Pixel_2_API_29], use -list-avds
```



出现这种情况一般是.android文件不在ANDROID_SDK_HOME目录下
只需要将系统默认的存放文件的地方：C:/用户/***/.android 复制到你ANDROID_SDK_HOME所指目录下即可