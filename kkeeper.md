---
title: kkeeper
date: 2022-03-29 14:11:15
tags:
categories:
---



# sqlite

```sql
create table password(
	id INTEGER PRIMARY KEY AUTOINCREMENT,
    username varchar(100),
	password varchar(100),
	ip varchar(50),
    domain varchar(100)
);
```



```sql
insert into password values(null,'admin','admin',null,'baidu.com');
```



## 自增

关键字 AUTOINCREMENT 的使用，必须满足以下两点:

1、只能用于整型（INTEGER）字段，INT类型是不可以；

2、只能用于PRIMARY KEY字段；





# QT



## 启动报错

卸了重装

```
pip uninstall pyqt5
```







## enter响应

```python
login = QtWidgets.QPushButton("login")
login.setShortcut('Return')
```



## 布局

![image-20220329182211173](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220329182211173.png)





[参考文档](https://www.pythonguis.com/tutorials/pyqt-layouts/)



### QVBoxLayout

 vertical

![image-20220330101842957](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220330101842957.png)



!!!

默认

![image-20220330105621161](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220330105621161.png)

其实是两个组件已经把窗口填满了！



### QHBoxLayout

horizonal

![image-20220330101854165](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220330101854165.png)





### QGridLayout

![image-20220330101939056](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220330101939056.png)





### QStackedLayout

你可以显示你想要的那一层的layout

![image-20220330105321139](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220330105321139.png)



```python
from PyQt5.QtWidgets import QStackedLayout  # add this import


class MainWindow(QMainWindow):
    def __init__(self):
        super().__init__()

        self.setWindowTitle("My App")

        layout = QStackedLayout()

        layout.addWidget(Color("red"))
        layout.addWidget(Color("green"))
        layout.addWidget(Color("blue"))
        layout.addWidget(Color("yellow"))

        layout.setCurrentIndex(3)

        widget = QWidget()
        widget.setLayout(layout)
        self.setCentralWidget(widget)
```





### 批量添加组件



![image-20220330102224983](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/image-20220330102224983.png)



```python
import sys

from PyQt5.QtCore import Qt
from PyQt5.QtWidgets import (
    QApplication,
    QCheckBox,
    QComboBox,
    QDateEdit,
    QDateTimeEdit,
    QDial,
    QDoubleSpinBox,
    QFontComboBox,
    QLabel,
    QLCDNumber,
    QLineEdit,
    QMainWindow,
    QProgressBar,
    QPushButton,
    QRadioButton,
    QSlider,
    QSpinBox,
    QTimeEdit,
    QVBoxLayout,
    QWidget,
)


# Subclass QMainWindow to customize your application's main window
class MainWindow(QMainWindow):
    def __init__(self):
        super().__init__()

        self.setWindowTitle("Widgets App")

        layout = QVBoxLayout()
        widgets = [
            QCheckBox,
            QComboBox,
            QDateEdit,
            QDateTimeEdit,
            QDial,
            QDoubleSpinBox,
            QFontComboBox,
            QLCDNumber,
            QLabel,
            QLineEdit,
            QProgressBar,
            QPushButton,
            QRadioButton,
            QSlider,
            QSpinBox,
            QTimeEdit,
        ]

        for w in widgets:
            layout.addWidget(w())

        widget = QWidget()
        widget.setLayout(layout)

        # Set the central widget of the Window. Widget will expand
        # to take up all the space in the window by default.
        self.setCentralWidget(widget)


app = QApplication(sys.argv)
window = MainWindow()
window.show()

app.exec()
```





### layout 嵌套

```python
layout1.addLayout( layout3 )
```



### 居中

```python
layout.addWidget(self.login, alignment=Qt.AlignHCenter)
```

表示水平方向居中



### 间距

```python
layout.setSpacing(20)
```



### align

```
Qt.AlignLeft | Qt.AlignTop
```









## 组件



### 组件大小

```python
password.setFixedSize(120,30)
```

resize不好使





### label

#### 文字大小

```
label.setStyleSheet('font: 30px')
```





### table

#### button in table

```python
button = QtWidgets.QPushButton('c')
tableWidget.setCellWidget(i, j, button)
```





## 位置

```python
setGeometry (0, 0, 30, 35)
```

从屏幕上（0，0）位置开始（即为最左上角的点），显示一个30*35的界面（宽30，高35）





# Python

## 异常捕获

```python
try:
	self.tableWidget.setItem(i, j, QTableWidgetItem(str(res[i][j])))
except Exception as error:
	print(error)
```

