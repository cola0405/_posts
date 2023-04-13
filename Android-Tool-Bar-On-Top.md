---
title: Android Tool Bar (On Top)
date: 2021-01-06 13:42:39
tags:
- Android
- Tutorial
categories:
- [Android,Tutorial]
---

XML

```xml
        <Toolbar
            android:id="@+id/tool_bar_for_student_signState"
            android:layout_width="match_parent"
            android:layout_height="0dp"
            android:layout_weight="1"
            android:navigationIcon="@drawable/back"
            android:background="@color/xui_config_color_titlebar"
            android:titleTextColor="@color/white">

            <TextView
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:layout_gravity="center"
                android:text="打卡"
                android:textColor="@color/white"
                android:textSize="20sp" />
        </Toolbar>
```

ConfigBackButton

```kotlin
    private fun configBackButton(){
        val backBtn = view?.findViewById<Toolbar>(R.id.tool_bar_for_student_signState)
        backBtn?.setNavigationOnClickListener {
            SignDataForStudent.DISPLAY_TYPE = SignDataForStudent.DISPLAY_SIGN_FIRST
            StudentActivity.tabSegment?.selectTab(1)
            NavUtil.navController?.popBackStack()
            NavUtil.navController?.navigate(R.id.signDataForStudent)
        }
    }
```



