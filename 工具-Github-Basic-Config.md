---
title: 工具-Github Basic Config
date: 2021-01-04 19:54:48
tags:
- Github
- Tutorial
categories:
- [Config,Github]
---

1.Usage of ".gitignore " file

When you push, you can exclude some files using ".gitignore " 

```
*.properties
```

means exclude all ".properties" file

You can also exclude a single file, just type it's whole file name

Usually, ".gitignore " file can't work directly, you need to do this also

```
git rm -r --cached .
```

Then push again

---

error

>OpenSSL SSL_read: Connection was reset, errno 10054

```
git config --global http.sslVerify "false"
```

---

zip 和 git clone 的区别在于是否有.git的隐藏文件