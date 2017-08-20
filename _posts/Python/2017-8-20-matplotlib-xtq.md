---
layout: 	post
title: 		"Matplotlib库入门"
date: 		2017-8-20 18:43:00
author: 	"玄天强"
header-img:	"img/mn-bg-xtq.jpg"
catalog: true
tags:
    - python
---

##1.基本使用

*	import matlibplot.matpylot	as plt
*	画一幅图并显示及保存

		plt.plot([y1, y2,..., yn])
		plt.axis([x_bg, x_ed, y_bg, y_ed])
		plt.show()
		plt.savefig("test", dpi=600)

*	画多幅图

		plt.subplot(211)
		plt.plot(x1,y1)
		plt.subplot(212)
		plt.plot(x2,y2)
		plt.show()

##2.plot函数

*	plt.plot(x, y, format_string, **args)
*	format_string用来指定绘制线条颜色标记点
*	颜色：

&nbsp;&nbsp; ![](http://7xrc1w.com1.z0.glb.clouddn.com/17-8-20/79473793.jpg)

*	标记字符：
	
&nbsp;&nbsp; ![](http://7xrc1w.com1.z0.glb.clouddn.com/17-8-20/54547778.jpg)

*	**args是可以继续加多组
	
		color:  控制颜色  color="green"
		linestyle: 线条风格  linestyle="dashed"
		marker: 标记风格  marker="o"
		markerfacecolor: 标记颜色  markerfacecolor='blue'
		markersize: 标记尺寸  markersize=20
		
##3.中文显示

*	matplotlib的rcParams属性设置全局所有字体

		matplotlib.rcParams[font.family] = 'STSong'
		字体:	
			'SimHei'-- 黑体       'Kaiti' -- 楷体
			'LiSu'  -- 隶书       'FangSong' -- 仿宋
			'YouYuan' -- 幼圆     'STSong' -- 华文宋体
		font.style = 'normal'/'italic'
		font.size = 20

*	fontproperties设置文本属性
	
		plt.xlabel('横轴：时间', fontproperties='SimHei', fontsize=20)

##4.文本显示函数

		plot.xlabel()
		plot.ylabel()
		plot.title()
		plot.text(x,y,str)
		plot.annotate(s, xy=(x,y), xytext=(x1,y1), arrowprops=dict)
		//字典指明箭头的一些属性
##5.子图绘制

*	subplot2grid(GridSpec, CurSpec, colspan=1, rowspan=1)

		每块的编号从0开始
		plt.subplot2grid((3,3), (1,0), colspan=2)
		3*3方块中第一行第0个,纵向占两块,横向默认为1
*	gridspec + subplot

		import matplotlib.gridspec as gridspec
		
		gs = gridspec.GridSpec(3,3)
		tu1 = plt.subplot(gs[0,:])	//第0行所有列