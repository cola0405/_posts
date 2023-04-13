---
title: 工具-Git Basic Commands
date: 2021-01-04 19:52:08
tags:
- Git
- Github
- Tutorial
categories:
- [Git,Tutorial]
---



# gitignore

```
git rm -r --cached 文件夹名
```

```
git rm --cached 文件名
```





# Push

```
git push
```

```
git push -u origin master
```

push master branch



---

# Pull

```
git pull
```





```
git pull origin master --allow-unrelated-histories
```





## pull 指定分支

切换分支然后pull即可



# branch

```bash
git branch -a

# 显示当前分支和显示其他分支
```



```bash
# 如果已有分支
git checkout dev

# 如果本地第一次切换到目标分支
git checkout -b test origin/test
```



# Remote Address

```
git remote show
```



Add remote address

```
git remote add origin https://github.com/fengcangjun/learngit.git
```



Delete origin remote address

```
git remote rm origin
```



Reset

```
git reset --mixed origin/main
```



# init 

```
git init
git add .
git commit -m ""   (to current branch)
git branch -M main   (switch to main branch)
git remote add orgin main   (origin is a remote address)
git push -u origin main
```

