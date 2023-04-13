---
title: Android Dialog Processing
date: 2021-01-04 22:11:27
tags:
- Android
- Tutorial
categories:
- [Android,Tutorial]
---

Display a circle in dialog when loading something

```kotlin
    private fun configLoadingProgress() {
        var loadingDialogBuilder = AlertDialog.Builder(this)
        val loadingProgress = ProgressBar(this)
        loadingDialogBuilder.setView(loadingProgress)
        loadingDialogBuilder.setTitle("正在登陆...")
        runOnUiThread {
            loadingDialog = loadingDialogBuilder.create()
            loadingDialog!!.show()
        }

    }
```

The circle is just a ProgressBar widget in dialog

Note !

1.Create and show a dialog should be done by UI Thread

2.There are some callback functions about the dialog, you can check the document

If you want to close the dialog by program 

```kotlin
loadingDialog?.cancel()
```

Note !

1.You should invoke cancel() from dialog but not dialogBuilder

2.dialog = dialogBuilder.create()

```kotlin
var loadingDialogBuilder = AlertDialog.Builder(this)
```

