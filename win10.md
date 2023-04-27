---
title: win10
date: 2023-04-22 18:30:50
tags:
categories:
---





1. 打开注册表编辑器（regedit.exe）。
2. 找到以下路径：HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Command Processor
3. 在右侧窗格中，找到名为“Autorun”的**字符串值**（如果没有，请创建它）。
4. 右键单击“Autorun”并选择“修改”。
5. 在“编辑字符串”对话框中，输入 `chcp 65001` 并单击“确定”。
6. 关闭注册表编辑器。
