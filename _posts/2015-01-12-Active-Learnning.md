---
layout: post
title: "Active Learning"
description: ""
category: 
tags: []
---
{% include JB/setup %}

<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML"></script>
<script src="https://google-code-prettify.googlecode.com/svn/loader/run_prettify.js"></script>

#引言
谈到Active Learning，我们将从机器学习说起。传统机器学习大致可以分为两类，训练数据已经标注类别的学习过程称之为有监督学习，而训练数据没有标注类别的叫做无监督学习。有监督学习的训练数据必须是已经标注好的。但在实际应用中，标注是相当耗时、困难的，因此标注样本的获得是很昂贵的。但是它的准确率比较容易保证。相对而言无标注数据是比较容易获得，但是无监督学习又有准确率不高的缺点。因此人们开始研究标注数据和无标注数据的结合。基于这一想法，提出了三种改进的机器学习方法

1）半监督学习, 综合利用有类标的数据和没有类标的数据，来生成合适的分类函数，它特指学习算法不需要人工的干预，基于自身对未标记数据加以利用。

2）直推学习，它与半监督学习一样不需要人工干预，不同的是，直推学习假设未标注的数据就是最终要用来测试的数据，学习的目的就是在这些数据上取得最佳泛化能力。

3）主动学习（Active Learning），该算法可以主动地提出一些标注请求，将一些经过筛选的未标注数据提交给专家进行标注，然后添加到训练集。而训练过程就是传统有监督学习过程。本文的主题就将对主动学习进行一个分析。

#主动学习

##主动学习的意义
主动学习的目的就是综合利用有标注和无标注样本进行训练，从而实现减少人工标注样本的工作量。其意义就是在保证准确率的前提下，使用较少的有标注样本。

##主动学习的一般过程
一般过程就是：从无标注数据集中选择部分数据交由人工进行标注，添加到训练集中，用新的训练数据集进行训练，如此周而复始，直至分类器达到预定的终止条件，则终止循环，达到训练目的。训练过程就是传统的有监督学习的过程，它的核心就是如何去选择一部分数据进行标注。

由以上分析可以得出主动学习算法的一般过程可以分为两个关键的部分：训练引擎、选择引擎。其流程图如下：

<p><img src="/img/al1.png"></p>

#采样方法

##不确定采样
依据信息论的理论，对于二分类问题，如果样本划分为这两类的概率相等，则信息熵最大。由此可以推广到多分类问题中。

我们定义：

$$M=|P(y1|x)-max{P(y2|x)}|$$

其中，x为当前样本；

y1和y2是x在当前分类器下最可能的两个分类；

M称之为差额，用它来衡量不确定性。

容易理解：如果M越小则说明当前分类器很容易判定错误，这样的样本应该交由人工标定；反之说明该样本很容易判定类别，没有什么信息量，则不需要标定。即没必要添加到训练集中。

##假设空间采样
假设空间就是所有给定已标定样本的多个假设函数的集合，该查询策略就是要减少版本空间。其中最有名的算法当属QBC(查询委员会),它包含一个有当前标定训练集的训练的一个委员会。委员会的成员代表了不同的假设函数，然后每一个假设函数都要对要查询的样本进行标注，差别最大的样本则需要进一步标定。而生成多个假设函数的一个方法就是基于boosting 和bagging，它们就用于从给定训练数据集生成查询委员会的。有许多标准可以用来估计委员会的不一致，比如投票熵定义为:

$$D=-\frac{1}{logk}\sum\frac{V(c,e)}{k}log\frac{V(c,e)}{k}$$

其中，k是假设空间的假设函数个数；

V(c,e)代表把样本e(当前样本)标定为c类的假设函数个数；

求和号是对所有类中e样本标定出现的类求和。

可以分析，如果所有假设函数对样本e的标定一致的话，V(c,e)=k,则D为0，则该样本没有什么信息量；如果V(c,e)均为1，则D值达到最大值，即假设函数分类分歧最大，则这样样本应该交由人工标定。

##Expect Error
该算法是估算添加新样本之后训练的模型，在候选集为测试集上的预期错误。选择最小的预期错误样本，进行专家标注。预期错误就用代价函数衡量，常用的代价函数有0/1-loss函数和log-loss函数。在这算法当中，要遍历每一个候选集样本，对它添加标定是由当前训练模型完成的。对于这个算法还有一个改进。因为误差就是由输出偏差导致的，所以我们可以把误差转换成分析输出的偏差，由此可以选择输出偏差最小的样本进行标注。

#采样方式

##流采样
候选集的样本顺序的交由选择器去分析判断，决定是否要进行标注，直至有T个需要进行标注则停止。(T目标添加样本数)。

##池采样
选择器去分析候选集中的所有样本，然后对分析结果进行排序，选择前T个样本进行标注。其中T同上。

对比两种方法，可以看出两种的根本区别在于：

前者选择器是独立判断单个样本是否标定，后者是进行全盘搜索之后，对其分析结果进行排序，然后选择最靠前的一个或者多个交由专家标定。

#结束语
在主动学习中，训练过程就是传统的有监督学习过程。训练过程不是本文内容涉及的重点，故本文重点分析了样本选择方法和方式。其实从训练过程来说，主动学习就是一个传统的有监督学习的过程，它的特点是训练集更新，当然最主要的优势是它利用了相对传统有监督学习要少的多的标注样本。既减少了人工标注的工作量；其实从侧面也防止了大量冗余数据而造成的过拟合，提高分类器的泛化能力。