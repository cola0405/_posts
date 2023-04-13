---
title: Android Swip Refresh
date: 2021-01-06 13:39:00
tags:
- Android
- Tutorial
categories:
- [Android,Tutorial]
---

XML

```xml
<androidx.swiperefreshlayout.widget.SwipeRefreshLayout
	android:id="@+id/location_swipe_for_student"
	android:layout_width="match_parent"
	android:layout_height="100dp">
</androidx.swiperefreshlayout.widget.SwipeRefreshLayout>
```

Config

```kotlin
    private fun configSwipeRefresh() {
        val swipe =
            view?.findViewById<SwipeRefreshLayout>(R.id.location_swipe_for_student)
        swipe?.setOnRefreshListener {
            MapUtil.mLocationClient?.startLocation()
            refreshActivity()
            swipe.isRefreshing = false
        }
    }
```

