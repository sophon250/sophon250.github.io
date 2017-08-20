---
layout: 	post
title: 		"Numpy库基础"
subtitle:	"Python没有数组 那就造个数组！"
date: 		2017-8-18 20:17:00
author: 	"玄天强"
header-img:	"img/mn-bg-xtq.jpg"
catalog: true
tags:
    - python
---

##1.ndarray数组对象

*	python原始数据类型没有数组，只有list、set和dictionary
*	Numpy中提供ndarray作为多维数组对象
*	ndarray一般要求元素类型相同，但也可以有非同质元素
*	ndarray数据类型更丰富
*	ndarray对象的属性：

		.ndim      -- 轴或维度的数量(轴就是维度)
		.shape     -- n行m列
		.size      -- 大小n*m
		.dtype     -- 元素类型
		.itemsize  -- 元素大小

##2.ndarray数组的创建及变换操作

*	创建: 

		（1）列表，元组创建
			x = np.array([1,2,3,4])
			x = np.array((1,2,3,4))
			x = np.array([1,2],[3,4],(5,6))
		（2）函数创建
			np.arange(x)
			np.ones(shape)
			np.zeros(shape)
			np.full(shape,val)
			np.eye(n)
		（3）另一个数组
			np.ones_like(a)
			np.zeros_like(a)
			np.full_like(a,val)
		 (4) 其他方法
			np.linspace(1,10,4)
			np.concatenate((a,b))
*	变换操作:

		arr.reshape(shape)
		arr.resize(shape)  --跟reshape功能一致，但修改原数组
		arr.swapaxes(ax1, ax2)
		arr.flatten()      --降维，返回折叠后的一维数组，原数组不变
		arr.astype(new_type)  --改变类型，返回新数组，可用来拷贝数组
		arr.tolist()       --转为列表
			 
*	dtype = *** 创建数组时须指定类型
*	数组索引跟切片

		(1)索引是一样的，取下标即可，下标从0向右递增，从-1向左递减， arr[i], arr[i,j]
		(2)切片： a[start : end : stride]

##3.ndarray运算

*	一元运算

		np.abs(x) / np.fabs(x)
		np.sqrt(x)
		np.square(x)
		np.log(x) / np.log10(x) / np.log2(x)
		np.ceil(x) / np.floor(x)	
		np.rint(x)
		np.modf(x)
        np.cos(x)/np.sin(x)/np.tan(x)/np.cosh(x)/np.sinh(x)/np.tanh(x)
		np.exp(x)
		np.sign(x)

*	二元运算

		+ - * / **
		np.maximum(x,y)    np.fmax()
		np.minimum(x,y)    np.fmin()
		np.mod(x,y)
		np.copysign(x,y)
	    > < >= <= == !=

##4.numpy读写CSV文件

*	写入文件

		np.savetxt(frame, array, fmt='%.18e', delimiter=None)
		args:
			frame -- 文件
			array -- 要保存的数组
			fmt   -- 写入文件的格式
			delimiter  --分割符，默认为空格
*    读入文件

		np.loadtxt(frame, dtype=np.float, delimiter=None, unpack=False)
		args:
			frame  --文件
			dtype  --数据类型，可选，默认为float
			delimiter --分割符，默认为空格
			unpack --若为True,读入属性将分别写入不同的变量

*	CSV只能存取一维或二维的数组
	
##5.多维数据的读写

*	tofile和fromfile

		1.写入:
			a.tofile(frame, sep='',format="%s")
			args:
				frame --文件名
				sep   --分割符，空串时以二进制写入
				format --写入格式
		2.读出：
			a = np.fromfile(frame, dtype=float, count=-1, sep='')
			args:
				frame  -- 文件名
				dtype  -- 读入的数据类型
				count  -- -1表示整个读入
				sep    -- 分割符，空串时以二进制方式读入
		3.由于没有数组行列信息，可以将其写入元数据文件，先查找，然后再读入

*	NumPy便捷存取

		1.写入:
			np.save(fname, array) / np.savez(fname, array)
		2.读出：
			np.load(fname)	
		3.该方法是以二进制读写，扩展名为.npz

*	save和load

##6.随机函数

*	rand系列

		np.random().rand(d0, d1, ..., dn)		--[0, 1]间的均匀分布
		np.random().randn(d0, d1, ..., dn)		--正态分布
		np.random().randint(low, high, (row, col)) --row*col的随机数组，范围[low, high]
		np.random().seed(s)                     --设置随机数种子
*	随机排列

		np.random.shuffle(a)         --数组最外层作随机排列,原数组改变
		np.random.permutation(a)     --同上，但原数组不变
		np.random.choice(a, (row, col), replace, p) 
                                       --a中选择row*col个数组成新数组，replace表示是否重复取，p是抽取概率

*	分布
	
		np.random.uniform(low, high, (row, col)) --均匀分布,[low, high]为范围
		np.random.normal(loc, scale, (row, col)) --正态分布，loc为均值，scale为标准差，然后是形状
		np.random.poisson(lam, (row, col))             --泊松分布，lam为随机事件发生的概率
##7.统计函数

		np.sum(a, axis=None)         --求和
		np.mean(a, axis=None)        --期望
		np.average(a,axis=None,weights=None)  --加权平均
		np.std(a, axis=None)         --标准差
		np.var(a, axis=None)         --方差
		
		np.min(a) np.max(a)          --最大最小值
		np.argmin(a)  np.argmax(a)      --最大最小值降一维后的下标
		np.unravel_index(index, shape)  --按shape将一维下标index转为多维下标
		np.ptp(a)                       --最大最小值的差
		np.median()                       --中值  

##8.梯度函数

*    np.gradient(f)
	
		[a0, a1, a2, ..., an]   
		g(a1) = (a2-a0) / 2
		g(a[n]) = (a[n]-a[n-1])) / 1
		g(a[0]) = (a[1]-a[0]) / 1
*	梯度反应元素的变化率
*	高维数组对应生成多个梯度数组


		

		


