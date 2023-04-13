---
title: Android Fragment And Activity
date: 2021-01-04 22:57:17
tags:
- Android
categories:
- [Android,Fragment]
---

Fragment's feature is reusable

A fragment is a completed page, and you can use a fragment tag(\<fragment/>) to insert it to any Layout

The code in fragment activity and normal activity is different

```
Yes, fragment also has it's activity called "Fragment Activity"
```

Difference

1.You can use "applicationContext" directly in normal activity 

But in Fragment Activity, you can't !

You need to invoke a method --- getContext()

```
kotlin can use "context" directly, but in fact, it invoke the method getContext()
```

2.You can use "runOnUiThread" directly in normal activity 

But in Fragment Activity,  you can't !

You need to get the Activity which is connected to UI Thread

Then 

```kotlin
activity?.runOnUiThread {
	...
}
```

Conclusion:

There are some difference, but that's not a big deal

Android SDK has solved that problem for us  

