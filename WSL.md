---
title: WSL
date: 2021-03-08 20:34:40
tags:
categories:
---

"cmd" with "administrator"

(Some simulator(e.g. Android simulator ) need to close hp-v virtual machine in win10)

```
bcdedit /set hypervisorlaunchtype off
```

open WSL(WSL base on hp-v virtual machine in win10)

```
bcdedit /set hypervisorlaunchtype auto
```

