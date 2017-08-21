---
layout: 	post
title: 		"Pandas库入门"
date: 		2017-8-21 11:09:00
author: 	"玄天强"
header-img:	"img/mn-bg-xtq.jpg"
catalog: true
tags:
    - python
---

##1.简介

*	两种数据类型：Series, DataFrame
*	基于两个数据类型的各类操作
*	基本操作/运算操作/特征类操作/关联类操作 
*	基于Numpy扩展数据类型

##2.Series类型

*	Series类型由一组数据及与之相关的数据索引组成
*	运算是基于索引的
*	其实就是一维的带'标签'数组
###2.1 创建：

*	从列表创建，index与列表元素个数一致
*	从标量值创建，index表达Series类型的尺寸
*	从字典创建，键作索引，Index从字典中进行选择操作，也可自己指定
*	从ndarray类型创建，索引和数据都可以通过ndarray类型创建

###2.2 操作:

*	索引操作，自动索引和自定义索引并存，可通过任何一种方式索引到值
*	操作类似ndarray类型，Numpy的运算和操作均可用，也可以切片
*	通过自动索引切片时，若有自定义索引，也一同切片
*	也有类似字典的操作，可用通过自定义索引访问，以及保留字in的操作
*	对齐操作，两个Series类型在运算时会自动对齐不同索引的数据
*	.name属性可用来设置Series对象和其索引的名字

## 3.DataFrame类型

*	由共用相同索引的一组列组成
*	是二维带'标签'数组
*	是一个表格型数据类型，每列值的类型可用不同
*	常用于表达二维数据，但也可以表达多维数据 

### 3.1 索引

*	行索引称index, 列索引称column
*	行指定为aixs=0, 列指定为axis=1  

### 3.2 创建

*	由二维ndarray对象创建

		d = pd.DataFrame(np.arrange(10).reshape(2,5))
*	由一维ndarray、列表、字典、元组或Series构成的字典创建

		dl = {'one':[1,2,3,4], 'two':[9,8,7,6]}
		d = pd.DataFrame(dl, index=['a','b','c','d']) 		
		
*	由Series类型对象创建
*	由其他DataFrame类型创建

###  3.3 操作

*	重新索引reindex()

		.reindex(index=None,columns=None,...)
		index,columns	新的行列自定义索引
		fill_value		重新索引中，用于填充缺失位置的值
		method          填充方法，ffill当前值向前填充，bfill向后填充
		limit           最大填充量
		copy            默认为True,生成新的对象，False时，新旧相等的话不复制

*	index和columns返回索引类型
*	索引类型的方法

		.append(idx)
		.diff(idx)
		.intersection(idx)
		.union(idx)
		.delete(loc)
		.insert(loc, e)

*	.drop()删除指定的行或列索引 

###  3.4 运算

*	算数运算: 

		补齐索引后运算，默认产生浮点数，
		补齐时填充NaN, 
		高维到低维间是广播运算，默认在1轴
		运算符产生新对象
		采用方法方式可以指定参与运算的轴
*	比较运算:

		只能比较相同索引的元素，不进行补齐
		高维到低维间是广播运算，默认在1轴
		采用运算符进行运算，产生的是布尔对象

## 4.数据排序

### 4.1 .sort_index(axis=0, ascending=True)

*	按索引排序
*	默认在0轴，升序排列 

### 4.3 .sort_values()	

*	Series.sort_values(axis=0, asending=True)
*	DataFrame.sort_values(by, axis=0, asending=True)
*	二维中用by指定是按哪个索引来排序
*	NAN放到末尾 

##5.统计分析

###5.1 基本统计分析函数

*	适用于Series和DataFrame类型

		.sum()		//数据的总和
		.count()	//非NAN值的数量
		.mean() .median()
		.var() .std()
		.min() .max()

*	适用于Series类型

		.argmin()	.argmax()	//自动索引
		.idxmin()	.idxmax()	//自定义索引

*	describe()

		Series和DataFrame分别返回对应其的类型，
		包含各种信息

###5.1 累计统计分析函数

*	基本函数

		.cumsum()	前n个的和
		.cumprod()	前n个的积
		.cummax()	前n个的最大值
		.cummin()	前n个的最小值

*	窗口函数

		.rolling(w).sum()	相邻w个元素的和
		.rolling(w).mean()	相邻w个元素的算数平均值
		.rolling(w).var()	方差
		.rolling(w).std()	标准差
		.rolling(w).min().max()	最小值和最大值

## 6.相关分析

*	协方差矩阵

		s1.cov(s2)

*	相关系数矩阵

		s1.corr(s2)	



	
