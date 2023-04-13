---
title: Android px dp sp
date: 2021-01-04 23:33:26
tags:
- Android
categories:
- [Android,Layout]
---

px is for the general unit

Note !

```
devices only know px
dp and sp is just use for display the appropriate views on different screen
```



dp is usually use for layout

```
density-independent pixels (dip,dp)
```

```
px = dp * (dpi / 160)
```

```kotlin
        fun dip2px(context: Context?, dpValue: Float): Int {
            val scale = context?.resources?.displayMetrics?.density
            return (dpValue * scale!! + 0.5f).toInt()
        }
```

Note 

You can pass context as a parameter

> dpi: Dots Per Inch

sp is usually use for text size

```
scale-independent pixels
```





