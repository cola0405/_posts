---
title: Android Layout Rule
date: 2021-01-04 23:15:12
tags:
- Android
categories:
- [Android,Layout]
---

1.About Weight

Allocate the rest space by it's weight

Pay attention to the "Rest Space"

So it's not right to use weight for all widgets

For widget like TextView, we should give it a fixed value of height

So that the text will not be strange

But for the widget like ScrollView we'd better use weight

because they should can be stretched

Note !

weight can be decimal ~

---

2.Center

If you want to put a image in the center of the whole page

Do like this 

```xml
<LinearLayout
            android:orientation="vertical"
            android:layout_weight="9"
            android:layout_width="match_parent"
            android:layout_height="0dp">
            
            <LinearLayout
                android:layout_weight="1"
                android:layout_width="match_parent"
                android:layout_height="0dp"/>
            
            <ImageView
                android:layout_gravity="center"
                android:src="@drawable/success_sign"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"/>

            <LinearLayout
                android:layout_weight="1"
                android:layout_width="match_parent"
                android:layout_height="0dp"/>
            
</LinearLayout>
```

That's the power of weight

With weight, the view can be stretched to fill the blank

Beside this center 

If You just want to put a view to the center of a layout

Then use the attribute "layout_gravity", assign it "center"

"layout_gravity", decide the position of a widget within a layout

"gravity", decide the text position within a widget

---

3.ViewGroup

Like 

```xml
<LinearLayout>
    
</LinearLayout>
```

\<LinearLayout>\</LinearLayout> is allow to add view into it

\</LinearLayout> is not allow add view into it