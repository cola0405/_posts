---
title: 工具-Hexo Live2D
date: 2021-03-08 21:31:03
tags:
- Hexo 
categories:
- [Hexo]
---

[github](https://github.com/EYHN/hexo-helper-live2d) (You can download model here)

(1) Install hexo-helper-live2d

```
npm install --save hexo-helper-live2d
```

(2)prepare model file

put the folder in "node_modules"

```
e.g. folder name "live2d-widget-model-miku"
```

(2) install model

```
npm install {your model's package name}
```

(3) _config.yml in Hexo root folder add:

```yml
# Live2D
## https://github.com/xiazeyu/live2d-widget.js
## https://l2dwidget.js.org/docs/class/src/index.js~L2Dwidget.html#instance-method-init
live2d:
  model:
    use: live2d-widget-model-miku
    scale: 1
    hHeadPos: 0.5
    vHeadPos: 0.618
  display:
    superSample: 2
    width: 150
    height: 300
    position: right
    hOffset: 0
    vOffset: -20
  mobile:
    show: true
    scale: 0.5
  react:
    opacityDefault: 0.7
    opacityOnHover: 0.2
```

