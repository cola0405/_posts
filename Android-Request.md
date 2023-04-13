---
title: Android Request
date: 2021-01-04 19:16:01
tags:
- Android
- Kotlin
- HTTP
categories:
- [Android,HTTP]
---

How get data by request in Android?

Here is an example

```kotlin
        Thread(){
            val url = URL("https://api.thecatapi.com/v1/images/search")
            val connection = url.openConnection() as HttpURLConnection
            connection.requestMethod = "GET"
            val inputstream = connection.inputStream
            val reader = inputstream.bufferedReader()
            var response = StringBuilder()
            while (true)
            {
                val line = reader.readLine()
                if (line == null)
                    break
                response.append(line)
            }
            reader.close()
            connection.disconnect()
            val jsons = JSONArray(response.toString())
            runOnUiThread{
				...
            }
        }.start()
```

Note:

1.You can't request in UI thread, so you need to create a new thread to do this job

2.The connection is actually established when you get inputStream from connection

3.You can use try-catch here to deal with the issue that connect time out 

4.You can't update UI in this new thread directly, you must use runOnUiThread{} to update UI

5.Every time you establish a connection remember to close it, it's a good habit

---

How to deal with JsonArray in Android

```kotlin
val signDataList = responseJson["activityInfo"] as JSONArray
for(index in 0 until signDataList.length()){
	signDataList[index]
}
```



---

Note

```
The request codes can be integrated into a util class
So that you don't need to write the repeat codes again and again
That's the power of Refactor !
```

Just like this

```kotlin
        fun getDataByRequest(activity:Activity?, context:Context, urlForLogin:URL?) {
            try {
                getDataByUrl(urlForLogin)
            } catch (e: Exception) {
                e.printStackTrace()
                buildConnectFailDialog(context)
                activity?.runOnUiThread {
                    connectFailDialog = connectFailDialogBuilder?.create()
                    connectFailDialog?.show()
                }
                Thread.currentThread().join()
            }
        }
        fun getDataByUrl(url: URL?){
            connection = url?.openConnection() as HttpURLConnection
            connection?.requestMethod = "GET"
            inputStream = connection?.inputStream
            reader = inputStream?.bufferedReader()
            response = StringBuilder()
            while (true) {
                val line = reader?.readLine() ?: break
                response?.append(line)
            }
            reader?.close()
            connection?.disconnect()
            responseJson = JSONObject(response.toString())
        }
        fun buildConnectFailDialog(context: Context?) {
            if (connectFailDialogBuilder == null) {
                connectFailDialogBuilder = AlertDialog.Builder(context!!)
                connectFailDialogBuilder?.setTitle("提示信息")
                connectFailDialogBuilder?.setMessage("连接服务器失败")
                connectFailDialogBuilder?.setPositiveButton("确定") { dialog, id -> {} }
            }
        }

```

There is a problem --- in a separate util class how can util get the application's context or activity ?

Solution:

```
Just pass them as parameters !
```

Context, activity they are not something special

In program, they are can be represent just with memory address

So pass their address as parameter is the way to access them !

