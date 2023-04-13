---
title: Android Bundle
date: 2021-01-04 22:26:13
tags:
- Android
categories:
- [Android,Transport Data]
---

Bundle can be  use for transport data between Fragment

Send

```kotlin
val bundle = Bundle()
bundle.putString("key1", "GFG :- Main Activity")
NavUtil.navController?.navigate(R.id.signStateForStudent,bundle)
// When you use navigation
```

Get

```kotlin
val bundle = Intent.getExtras()
bundle.getString("key1", "Default") 
// arg2 will be return when "key1" can't be foud in bundle
```

But it can just be transported one time ! !

When you back to the fragment, the bundle will gone 

Bundle just can be use for the "one-time" issue

---

For the data you need to use many time 

You can use companion object {} to solve that problem

All fragments can get the data directly from the companion object {} within an activity