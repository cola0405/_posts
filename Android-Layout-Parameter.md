---
title: Android Layout Parameter
date: 2021-01-06 13:30:11
tags:
- Android
- Tutorial
categories:
- [Android,Tutorial]

---

Build

```kotlin
var layoutParamsForInfoUnit: LinearLayout.LayoutParams? = null
fun buildLayoutParamsForInfoUnit(context: Context?){
layoutParamsForInfoUnit =
                LinearLayout.LayoutParams(ViewGroup.LayoutParams.MATCH_PARENT, DpUtil.dip2px(context,100f))
layoutParamsForInfoUnit?.setMargins(DpUtil.dip2px(context, 10f), DpUtil.dip2px(context,10f), DpUtil.dip2px(context,10f), 0) // left,top,right,bottom
}
```

Use

```
signDataView!!.layoutParams = LayoutUtil.layoutParamsForInfoUnit
```



