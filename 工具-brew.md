---
title: 工具-brew
date: 2022-01-11 14:25:25
tags:
categories:
---





# Brew

## ustc

中科大的源



## Homebrew

Homebrew is a free and open-source software package management system 

that simplifies the installation of software on Apple's operating system, macOS, as well as Linux. 

The name is intended to suggest the idea of building software on the Mac depending on the user's taste.





# 源



查看brew.git的源

```bash
cd "$(brew --repo)" && git remote -v
```

查看homebrew-core.git的源

```bash
cd "$(brew --repo homebrew/core)" && git remote -v
```



## 中科大（ffmpeg装不了）

```bash
cd "$(brew --repo)" && git remote set-url origin https://mirrors.ustc.edu.cn/brew.git
```

```bash
cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core" && git remote set-url origin https://mirrors.ustc.edu.cn/homebrew-core.git
```

```bash
cd "$(brew --repo)/Library/Taps/homebrew/homebrew-cask" && git remote set-url origin https://mirrors.ustc.edu.cn/homebrew-cask.git
```



bootle domain

```bash
echo 'export HOMEBREW_BOTTLE_DOMAIN=https://mirrors.ustc.edu.cn/homebrew-bottles' >> ~/.zshrc
```

```bash
source ~/.zshrc
```



刷新源

```bash
brew update
```



## 阿里

```bash
cd "$(brew --repo)" && git remote set-url origin https://mirrors.aliyun.com/homebrew/brew.git
```

```bash
cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core" && git remote set-url origin https://mirrors.aliyun.com/homebrew/homebrew-core.git
```



bootle domain

```bash
echo 'export HOMEBREW_BOTTLE_DOMAIN=https://mirrors.aliyun.com/homebrew/homebrew-bottles' >> ~/.zshrc
```

```bash
source ~/.zshrc
```



刷新源

```bash
brew update
```





## 官方

```bash
cd "$(brew --repo)" && git remote set-url origin https://github.com/Homebrew/brew.git
```

```bash
cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core" && git remote set-url origin https://github.com/Homebrew/homebrew-core.git
```

```bash
cd "$(brew --repo)/Library/Taps/homebrew/homebrew-cask" && git remote set-url origin https://github.com/Homebrew/homebrew-cask
```



bootle domain，把别的源注释掉就行

```bash
vi ~/.zshrc
# export HOMEBREW_BOTTLE_DOMAIN=xxxxxxxxx
```

```bash
source ~/.bash_profile
```



刷新源

```bash
brew update
```

