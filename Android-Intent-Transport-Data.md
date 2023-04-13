---
title: Android Intent Transport Data
date: 2021-01-04 19:59:36
tags:
- Android
- Tutorial
categories:
- [Android,Tutorial]
---

Example:

Send data

```kotlin
    private fun toStudentPage(loginInfo: JSONObject) {
        val intent = Intent(this, StudentActivity::class.java).apply {}
        intent.putExtra("studentId", loginInfo["studentId"].toString())
        intent.putExtra("studentName", loginInfo["studentName"].toString())
        intent.putExtra("classId", loginInfo["classId"].toString())
        intent.putExtra("className", loginInfo["className"].toString())
        startActivity(intent)
    }
```

Get data

```kotlin
    val studentId = intent.getStringExtra("studentId")
    val studentName = intent.getStringExtra("studentName")
    val classId = intent.getStringExtra("classId")
    val className = intent.getStringExtra("className")
```

Note:

Intent is like a build-in object in Kotlin