---
title: commandline tool
date: 2023-04-11 11:09:26
tags:
categories:
---







# 创建

①

```
npm init -y
```



②

create `bin/index.js`

```
#!/usr/bin/env node
console.log('hello');
```

We place a `hashbang` directive at the top of our file stating which interpreter will be used to execute our script.





③

`package.json`

add a new property

```json
"bin": "bin/index.js",
```



④

打包

```
npm link
```





# 发布

```
npm login
```



```
npm publish
```

如果报403，说明 cli 重名了

进入 `package.json` 修改 `name` 属性



这个 `name` 属性用于install 也用于该 cli 工具的使用

```
npm install cola-test044 -g
```

```
C:\Users\10201\Desktop>cola-test044
hello
```
