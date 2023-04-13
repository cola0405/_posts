---
title: CSharp-Pasker
date: 2022-06-22 09:37:51
tags:
categories:
---



## 窗体跳转

```c#
page.Main mainForm = new page.Main();
this.Hide();
mainForm.Show();
```



然后添加`FormClosed`事件到新窗体

```c#
private void Main_FormClosed(object sender, FormClosedEventArgs e)
{
	Application.Exit();
}
```



## 包引用

```c#
using HelloWorld.entity;
```





## 循环次数不对

其实是回调函数的问题

```
private void itemList_Paint(object sender, PaintEventArgs e)
```

每添加一个新组件，又会重新回调一下这个函数

所以List里面只有1个元素，但是却循环了3次





## 数据持久化

setting中存数据



数据读取

首先，第三方库利用NuGet安装

```
install-package newtonsoft.json 
```



反序列化：

```c#
List <Password> json = JsonConvert.DeserializeObject<List<Password>>(Properties.Settings.Default.password1);
```



序列化：

```c#
List<Student> lstStuModel = new List<Student>(){
	new Student(){ID=1,Name="張飛",Age=250,Sex="男"},
	new Student(){ID=2,Name="潘金蓮",Age=300,Sex="女"}
};

//Newtonsoft.Json序列化
string jsonData = JsonConvert.SerializeObject(lstStuModel);
```





