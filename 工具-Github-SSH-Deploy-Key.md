---
title: 工具-Github SSH Deploy Key
date: 2021-01-04 19:35:50
tags:
- Git
- Github
- Tutorial
categories:
- [Github,Tutorial]
---

With Deploy key you can push directly, do not need to input username and password every time

Generate SSH key

```
ssh-keygen -f deploy_key_blog -C "1020151695@qq.com"
```



 Then press "Enter" twice is OK

```
E-mail address like an "id"
So that Github repository know who you are
And you don't need to input username and password again
```



Then it will create a new file named "deploy_key_blog.pub"

Check it's content use the command:

```
more deploy_key_blog.pub
```



Then copy the content and go to the project in Github

"Setting"--"Deploy keys"

Just do it !

And SSH key absolutely just support the ssh way

If you use HTTPS remote address, you need to switch it 

```
git remote rm origin      // delete origin remote address 

git remote add origin git@github.com:nickchou/gocode.git  // apply new remote address
```



