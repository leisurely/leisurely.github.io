---
layout: post
title: "Expectation maximization"
description: ""
category: static
tags: [static]
---
{% include JB/setup %}

语言是一种基于对象的编程语言，对象中存储我们需要的数据，每个对象又可能会包含多个属性。所有的对象都有两个内在属性：类型和长度。类型是对象元素的基本种类，共有四种：数值型，字符型，复数型、逻辑型和因子型。在此基础上还有几种更为常用的数据类型包括Arrays（数组），matrices（矩阵），Data Frames（数据框）和Lists（列表）。其中，数据框和列表两种类型可以允许同一个对象中包含多种类型。接下来主要介绍多维数组和list的运用。

多维数组很易于理解，可以通过array()函数来定义，并通过元素的编号或者位置进行访问：

	#生成4*2*2的多维数组，其中每个数组大小为4*2
		MultiArray <- array(1:16, c(4,2,2))```     
		print(MultiArray)```
	#在访问多维数组的时候，有以下两种方式：
	#方式1：按照顺序访问
		print(MultiArray[1]) #访问第一个元素
		print(MultiArray[9]) #访问第九个元素
	#方式2：MultiArray[x,y,z]中z代表第几个数组，
	x和y分别代表第z个数组中的第x行第y列
		print(MultiArray[3,1,2]) #访问第十个元素，
	即第二个数组第三行第一列位置的元素值

对于list变量，可能我们在初次使用的过程中可能会出现一些使用上的错误。列表是一个以对象的有序集合构成的对象。列表中包含的对象又称为它的分量（components），分量可以是不同的模式或者类型。在访问列表变量的过程中，一般存在两种方式：利用编号访问分量（双中括号）；利用分量名字访问。如果列表变量（Lst）含有三个分量， 这些分量可以用 Lst[[i]]（其中i=1,2,3）独立访问。而Lst[[i]][1] 就是第i个分量的第一个元素。
如果列表变量（Lst）的三个分量分别对应三个名字：x，y和z，那么Lst$x v.s. Lst[[1]] 以及Lst$x[2] v.s. Lst[[1]][2]返回结果都是一样的。
	
	#创建list变量，变量包含三个分量。
		Lst <- list(name="drafly", age=26, date=c(2014,11,11))
		print(Lst)
	#访问Lst变量的第一个分量
		Lst[[1]]
	#列表变量的长度：函数length(Lst)返回结果是分量的数目(最高层次的列表变量的长度)
		length(Lst)
	#列表变量的两种访问方式
		Lst[[1]]
		Lst$name
		Lst[[3]][2]
		Lst$date[2]

这里还需要注意为列表变量分量命名和列表变量转换类型的两个问题，其中可以采用names()函数赋予列表分量名称，使用unlist将列表转换为字符串型的行向量： 

	#创建list变量，变量包含三个分量。
		Lst <- list("drafly", 26, c(2014,11,11))
		print(Lst)
	#赋给列表变量Lst各个分量名称
		names(Lst) <- c("name", "age", "date")
	#同样，也可以为列表变量的分量的元素命名
		names(Lst[[3]]) <- list("year", "month", "day")
	#列表变量类型转换:将列表变量转换为行向量
		tmp <- unlist(Lst)
		typeof(tmp) #str(tmp)
		tmp_compn <- unlist(Lst[[3]])
		str(tmp_compn)
		tmp_compn["month"] #tmp_compn[2]

上面一部分介绍了R中一些变量类型的操作，一般来讲，当R运行时，所有变量，数据，函数及结果都以对象(objects)的形式存在计算机的活动内存中，我们可以通过用一些运算符(如算术，逻辑，比较等)和一些函数(其本身也是对象)来对这些对象进行操作。但是如果该对象已经存在，那么它以前的值将会自动被新值冲掉。对于数据操作而言，常用指令有：

##描述统计函数
str()/summary()/typeof()等。summary()函数是一个用于描述统计的函数，它可以从大量数据中压缩提取基本信息，或者用来给出各种模型的拟合函数结果的基本信息。str()函数也是一个用于描述变量信息的函数，其可以返回对象的结构或内容，也可用于查看R中常用的内置函数的参数信息。个人认为str函数还是最为好用的。 

	#R中常用的描述统计函数
		summary(Lst)
	#对矩阵各列信息的基本统计描述
		summary(matrix(1:15, nrow=5, ncol=3, dim=list(c(1,2,3,4,5), c("x","y","z"))))
	#变量基本信息描述
		str(Lst) #names(Lst);
		typeof(Lst);
		class(Lst);
		mode(Lst)
	#常用函数基本信息描述
		str(lm)

##attach()/detach()/with()

attach()函数可以使列表或者数据框的分量可以通过它们的名字直接调用，该函数通过将数据框或者列表添加到R的搜索路径中，并当R在遇到一个变量名检查搜索路径中的数据框或者列表时，以定位到这个变量。该函数可以用于解除用$ 符号访问对象不方便的问题。这种调用是暂时性的，没有必要每次都显式的引用列表名字。而detach()函数可以将数据框从搜索路径中移除。with()函数则是对函数内的变量执行上述过程，用于解决当名称相同的对象不止一个时产生的冲突问题。attach()函数通常是将数据框绑定在搜索路径的位置2（position 2）上。如果位置1没有相同名称的变量，那么该数据框的变量名称对应的变量将直接被访问；相反，如果存在，则任何操作仅是针对搜索路径位置1工作空间中的变量。这时要对数据框中的变量进行操作，最好还是通过$符号或者with()函数。

	#attach函数
		str(iris)
		Species
		iris$Species
	#加载变量名称用于搜索变量名，代替$符号
		attach(iris)
		Species
		detach(iris)
		Species
	#with函数
		data=data.frame(c1=c(1,2,3,4),c2=c(5,6,7,8))
		attach(data)
	#当定义一个新的变量c1时，会产生冲突
		c1 = 1
	#data$c1的值不会被改变,对原数据框的数据未产生影响
		data$c1
		c1
	#使用with()函数解决冲突问题
		summary(c1)
		with(data, summary(c1))

##by()/tapply()
二者以及apply()函数的变体均属于嵌套函数，可用于分组统计变量的信息。 

	#by函数和tapply等嵌套函数
		attach(iris)
		by(Sepal.Length, Species, mean)
		tapply(Sepal.Length,Species, mean)
		detach(iris)

##ls()/ls.str()/rm()

ls()函数是列出当然目录变量，其结果是一个字符串向量。如果没有定义的赋值变量，则会返回一个空向量。rm()函数可以删除用户中已定义的变量，但该函数删除的变量无法撤销，也可以传入多个变量来进行删除。

	#ls函数和rm函数
		ls()
		ls.str()
		rm(c1) #删除变量c1
		ls()    
