---
title: Android Fragment Tutorial
date: 2021-01-06 09:42:02
tags:
- Android
- Tutorial
categories:
- [Android,Tutorial]
---

1.New A Fragment

"New" -- "Fragment" -- "Fragment Blank"

Then we can get an fragment activity and relative layout file

2.Add Fragment To Activity

In target xml file

```xml
    <fragment
        android:id="@+id/xxx"
        android:name="xxx"
        android:layout_width="match_parent"
        android:layout_height="match_parent"/>
```

 Note !

Name and Id is essential ! ! !

Name is the fragment activity you just created

(Just the class name of the fragment activity)

```
com.exmaple.BlankFragment
```

```
class BlankFragment : Fragment()
```

Then you can name id as you like, but do not forget it, it is really important ! !

---

After two steps, you can see a fragment is added to an activity