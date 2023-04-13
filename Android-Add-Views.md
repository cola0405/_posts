---
title: Android Add Views
date: 2021-01-06 13:33:16
tags:
- Android
- Tutorial
categories:
- [Android,Tutorial]
---

Example

```kotlin
signDataView = SuperTextView(requireContext())
buildSignDataView(signDataView, signData)
activity?.runOnUiThread {
	signDataListLayout?.addView(signDataView)
}
```



