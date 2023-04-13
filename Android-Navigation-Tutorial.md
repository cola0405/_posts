---
title: Android Navigation Tutorial
date: 2021-01-06 12:49:10
tags:
- Android
- Tutorial
categories:
- [Android,Tutorial]
---

1.New A Navigation

"res" -- "New" -- "Android Resource File" -- "Resource Type" -- "Navigation"

Give your navigation a name, then click "OK"

Then you will got a xml file of your navigation

2.Add A NavHost To Your Activity

Go to the xml file of your activity

Use "Design" model 

"Palette" -- "Container" -- "NavHostFragment"

Drag it to the phone

And choose a navigation xml file for the container

Then we finish the basic of navigation

3.Add Fragments To Navigation

Go to the xml file of your navigation 

Still use "Design" model

Then "New Destination"

4.Use Navigation

```kotlin
val navHostFragment =supportFragmentManager?.findFragmentById(R.id.fragment) as NavHostFragment
val navController = navHostFragment?.navController
navController.navigate(R.id.hello)
```

Then you will be navigate to a fragment named "hello"

---

supportFragmentManager

```
the FragmentManager for interacting with fragments associated with this activity.
```



