---
title: 微软AI训练营笔记
date: 2022-01-05 09:53:25
tags:
categories:
---



# 微软的产品

Bing是微软的产品

微软把自己的服务部署在自己的服务器Azure





## Hackathon

![image-20220105101825322](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220105101825322.png)





## 二次广告

![image-20220105103448931](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220105103448931.png)

## 虚拟老师

在线英语教学市场准备迎接虚拟老师



1000+堂课就可以训练出一个虚拟老师





## VIPKid

外教英语

已经用过虚拟老师了

## AI技术

![image-20220105103730230](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220105103730230.png)





## chat bot

80% 已经是很好的了



## SAAS

现在很多的AI 都是SaaS了

调接口



## Responsable AI

（负责任的AI）

“我是AI”

工具，还是武器？——直面人类科技最紧迫的争议性问题

## AI的透明性

>如果 人工智能的内部工作机制完全处于暗箱之中，公众怎么可能会 对人工智能有信心，同时未来的监管机构又怎么来评估对前4条 准则的遵守情况？

## 隐私保护

一键删除所有数据



## 责任

自动驾驶---驾驶人，因为是驾驶人启用了自动驾驶的功能

特斯拉也改了广告标语，不是完成全部工作，而只是作为一个辅助功能





# AI

就像是前好多年时的计算机、网络

## 图灵测试

![image-20220105134730992](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220105134730992.png)

看人能否能区分人的回答和AI的回答

目前还没有能通过图灵测试的AI



## 发展史

现在处于第三轮的顶峰（深蓝，阿尔法狗）

![image-20220105135112839](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220105135112839.png)

![image-20220105135010332](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220105135010332.png)

第三次顶峰的原因

数据和算力的飞跃





## TPU

专门训练Tensorflow





# 深度学习(深度神经网络)

![image-20220105135914892](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220105135914892.png)

分类：

CV、自然语言、语音处理

传统机器学习，我们知道它干了什么事

但是深度学习。。。

（还有人在研究每一层到底在干什么）



## 深度神经网络

隐藏层数较多的

参数量大

需要很多标注数据

但其泛化能力强

现在上百层上千层已经不是问题了。。。



![image-20220105140923729](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220105140923729.png)



## 激活函数

sigmoid 是激活函数

![image-20220107094432522](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220107094432522.png)

ReLu、Leaky ReLu

![image-20220107091959977](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220107091959977.png)

激活函数共性 - 非线性

线性的叠加还是线性的

加入激活函数的话，为了有非线性性





z=wx+b

a=sigmoid(x)



一开始随机w、b

之后通过不断拟合，使得loss最小

（使得a与y接近 - 交叉熵函数）

得到w、b






## 交叉熵函数

loss(a)

可以转化为 loss(w,b)



然后使用梯度下降法不断迭代，达到一个最优的结果





## 前向传播

直接得出a

设置参数，得出预测





## 反向传播算法（反向传播）

![image-20220107094839313](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220107094839313.png)



反向得出参数值



## 步长（学习率）

步长太小，会影响收敛速度

主要调的就是这个





## 权重初始化

![image-20220107105619872](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220107105619872.png)

防止梯度爆炸



## 复杂一些的神经网络的反向传播推导





## 神经网络

神经元和连接

神经网络的结构还有多种

CNN、 等等





## 深度学习的发展

随着算力和数据的发展，深度学习迅速发展

语音识别和图像识别体现出了深度学习的新生强大力量





## 不可知性

模仿人脑

人脑本身还不可知

神经网络也具有一定不可知性

像是古人在炼丹



## 数据集

![image-20220107103556027](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220107103556027.png)



## k-fold cross validation

![image-20220107103645170](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220107103645170.png)



## high bias and high variance

偏差与方差

![image-20220107104009963](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220107104009963.png)



![image-20220107104210981](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220107104210981.png)



过拟合，方差高

欠拟合，验证集都不太行，偏差严重



我们想要的是偏差和方差都低







## 正则化xx

L2 普遍使用



dropout 关闭一些神经元

![image-20220107104839074](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220107104839074.png)

参数少，训练快，反而准确率更高

（避免过拟合）

dropout 习惯0.4 ~ 0.5



## 数据增强

![image-20220107105028867](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220107105028867.png)

应用在数据量不足的情况

需要召回率高

尽可能找出各种奇形怪状的（旋转、平移、镜像）

那么这个数据增强就派上用场了

（提高泛化能力）



## 归一化xx

![image-20220107105317517](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220107105317517.png)



代码可以帮你做掉





## 批量梯度性下降（Bath GD）xx

一次拿m个样本进行训练

很多数据的时候，梯度下降太慢了

100w



## 小批量梯度下降（mini-Bath GD）xx

64 128 



## Adam算法

Adam = 动量梯度下降 + RMsProp

无脑用Adam算法

解决摆动幅度过大的问题

b1 = 0.9

b2 = 0.999

3 = 10的-8次方











## 超参数xx

很固定很固定的



## 学习率衰减xx





## 跳出局部最优xx





# 迁移学习xx

现在一般都是迁移学习



# 机器学习



![image-20220105141426414](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220105141426414.png)







## 目标函数（损失函数）







## 强化学习

![image-20220106135511223](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220106135511223.png)

奖励机制

走迷宫，撞墙扣分



## 生成对抗网络（GAN）





## 三要素

模型、数据、算法





## 统计学

《统计学习方法》

李航 清华大学出版社



## 模型分类

![image-20220106135036390](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220106135036390.png)

![image-20220105164705159](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220105164705159.png)

### 分类模型

KNN、NB（朴素贝叶斯）、DT（决策树）、LR（逻辑回归）

SVC（support vector）

### 回归模型

（预测，有一个return）

线性回归、SVR

### 聚类模型

（无监督）

K-Means



### 特殊的模型

HMM、CRF



### 无监督学习和有监督学习

不需要标注数据

监督学习：有正确答案，是猫是狗

半监督是之后的热点，比较难

（现在没有完美的解决方案）







# 数据处理

## 数据集

![image-20220106140628139](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220106140628139.png)

验证集：调参

测试集：验证



## 准确率

其中还涉及到混淆矩阵

![image-20220106141745314](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220106141745314.png)

## 精确率和召回率

![image-20220106141818732](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220106141818732.png)



新冠检测，宁可错s，不放过一个



上面这两者，鱼与熊掌不可兼得

看应用场景



精确率高：测出是假币，尽量100%就是假币

召回率高：全部个体里，有问题的都已测出



## 不平衡的数据集

![image-20220106142641703](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220106142641703.png)



## 数据集网站

kaggle









## ROC曲线

![image-20220106141609660](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220106141609660.png)

越靠近左上角，模型越好（100%阳性）

B比AC要好



## 数据收集



## 数据清洗

错误、冗余、异常值



## 数据编码



## 数据归一化

![image-20220106103958585](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220106103958585.png)



Pandas、Dataframe







## 特征抽取





# 

# 线性回归



## 最小二乘法



## 梯度下降法

简单，通用

但不保证最优解





# 分类器

## 二分类

阈值



## 线性回归与分类器

如果有一点比较偏则影响很大





## 逻辑回归

逻辑回归 = 线性回归 + Sigmoid函数

![image-20220106150128763](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220106150128763.png)



## 目标函数（损失函数）

![image-20220106150636664](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220106150636664.png)

为了方便后面的计算





## 朴素贝叶斯

![image-20220106150827683](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220106150827683.png)

P(A|B)=1/6

在B的前提下，A的概率

20个人，男生有6个，穿白袜子的人4个

穿白袜子的人里，是男生，的概率是0.25，则4x0.25=1，则只有一个男生穿了白袜子

则一个人是男生，他穿袜子，真的概率是1/6



“朴素”

特征之间相互独立



![image-20220106151755049](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220106151755049.png)

数据集中没有，不代表现实中没有（多变量的情况）







## 分类器实例

识别十二生肖

若干个二元分类

![image-20220106150731203](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220106150731203.png)



# 决策树

![image-20220106152100069](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220106152100069.png)



叶子节点是返回结果





## 决策树生成算法



## ID3

筛选offer

薪资低于多少的直接不要



## C45

![image-20220106152846452](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220106152846452.png)



## 信息熵



# 聚类 Clustering

![image-20220106153115031](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220106153115031.png)



## 欧氏距离

（一般是欧式距离）

表示相近





## 余弦距离





## 曼哈顿距离



## KNN算法

有监督





## K-Means

无监督

除了名字相似，没什么联系的

k 人工指定



## Lloyd 算法

是K-Means 的标准方法，但是没有办法保证最优解

3次聚类，选一个指标最好的

（避免局部最优）

对非球形簇的效果不咋好



# 谱聚类

![image-20220106154757309](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220106154757309.png)





# 实践

## Python 机器学习包 scikit-learn

![image-20220106160445059](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220106160445059.png)





![image-20220106161143799](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220106161143799.png)







## 模型选择

![image-20220106170608708](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220106170608708.png)

![image-20220106171204547](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220106171204547.png)

![image-20220106171221060](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220106171221060.png)

![image-20220106171239685](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220106171239685.png)

# 计算机视觉（CV computer version）

照片唱歌，随着歌曲而动嘴





## 图像处理

![image-20220105141639228](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220105141639228.png)



## deepface



## yolo

目标检测





# first order model

checkpoint

tar 放到目录下





# 语音处理

![image-20220105142001960](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220105142001960.png)





## 微软speech studio



情感能力调节技术



## TTS





# 自然语言处理

![image-20220105142236010](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220105142236010.png)

主要处理文本



## GTP-3xx







## 知识图谱xx

谷歌提出来的

连接主义和符号主义



## 连接主义xx



## 符号主义xx









# AI 人才栈



![image-20220105145623375](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220105145623375.png)



## 算法工程师

现在基本上是博士（还得是top的高校）

（以前有硕士）

新算法的研究

阿里达摩院



## KPI

部门/个人的业绩指标

量化绩效管理



## 多线程

几百G甚至上T的数据处理

对多线程的需求很大



## 测试pipeline



## 模型的部署





## 数据标注

> 在我的理解来看，数据标注是非常非常重要的
>
> （验证标注质量）





## 数学储备

![image-20220105164537475](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220105164537475.png)





![image-20220106091506181](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220106091506181.png)





# 数据分析

大概有两种分析：描述性分析和预测性分析（推送、用户需求）



## 极大似然估计

> 极大似然估计太重要太重要了





## 贝叶斯估计





## 信息熵



# 数据处理数据可视化



## 塔夫特原则

![image-20220106105259381](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220106105259381.png)



### 尊重事实

![image-20220106105649029](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220106105649029.png)



就差了3cm

但是比例看起来好像差了10几cm

![image-20220106113244160](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220106113244160.png)









### 标注

比例尺，不同颜色的点代表什么

![image-20220106111711526](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220106111711526.png)



###内容重要形式

![image-20220106110039933](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220106110039933.png)

右边一目了然最好

左边的太多噪声了



## 图表



### 直方图histogram



### KDE图

平滑

![image-20220106110939071](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220106110939071.png)





### 箱形图（盒）

![image-20220106111046266](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220106111046266.png)

上/下四分位数：25%

异常值：上下限之外的值

（和传统的异常值不是一个概念）



### 小提琴图

![image-20220106111336119](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220106111336119.png)





### 条形图

和直方图的区别



### 多维度散点图

![](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220106111711526.png)

不同颜色再做区分



### 热力图

![image-20220106112147292](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220106112147292.png)

![image-20220106112253289](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220106112253289.png)

用颜色表达程度

（更多是基于地理信息，如：天气信息、人口流动）



### 高维数据可视化

现在依旧是问题

尽量避免





## 数据可视化与机器学习

聚类可视化来选择更加合适的模型

![image-20220106112923076](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220106112923076.png)

单单看数据没感觉的

可视化出来之后，能更清晰选择拟合方式





# CNN

## 卷积 Filter

乘卷积核（fliter kernel），就把矩阵给卷起来了



## 填充 Paddingxx





## 步幅 Stride



## 池化

压缩且保留信息

卷积层 + 池化层 = layer



### 平均池化xx











## 神经网络一般结构

![image-20220107112816793](https://picgo-freejim.oss-cn-beijing.aliyuncs.com/to_upload/image-20220107112816793.png)





## LeNet-8 (1998)xx





## AlexNet



## VGG-16（2015）

16个卷积层，16个全连接层

1.38亿个参数



## Inception Network(2014)

v3







## 为什么卷积有效







# 抽象

抽象之后，可以有这样的问题

“有没有连续但是不可比较的数据”

有！如颜色RGB，数值连续，但是没有优劣之分

























