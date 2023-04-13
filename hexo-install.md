---
title: hexo install
date: 2023-03-14 15:41:21
tags:
categories:
---



# 一、安装主题

```
cd hexo-site
git clone https://github.com/next-theme/hexo-theme-next themes/next
```





# 二、安装 search engine

```ssh
npm install hexo-generator-searchdb --save
```



`root/_config.yml` 新增

```yml
search:
  path: search.json
  field: post
  format: html
  limit: 10000
```



`theme/_config.yml`

```yml
local_search:
  enable: true
  # if auto, trigger search by changing input
  # if manual, trigger search by pressing enter key or search button
  trigger: auto
  # show top n results per article, show all results by setting to -1
  top_n_per_article: 1
  # unescape html strings to the readable one
  unescape: false
```





# 三、数学公式

```ssh
npm uninstall hexo-renderer-marked --save
npm install hexo-renderer-kramed --save
```

`theme/_config.yml`

```yml
math:
  # Default (false) will load mathjax / katex script on demand.
  # That is it only render those page which has `mathjax: true` in front-matter.
  # If you set it to true, it will load mathjax / katex script EVERY PAGE.
  every_page: true

  mathjax:
    enable: true
    # Available values: none | ams | all
    tags: none
```



