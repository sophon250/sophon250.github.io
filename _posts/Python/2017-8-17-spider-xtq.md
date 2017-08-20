---
layout: 	post
title: 		"Python爬虫入门"
subtitle:	"Requests & Re & Scrapy"
date: 		2017-8-17 21:43:00
author: 	"玄天强"
header-img:	"img/mn-bg-xtq.jpg"
catalog: true
tags:
    - python
---

##一、Requests库

*	方法汇总
*	其他几个基于request()方法

![](http://7xrc1w.com1.z0.glb.clouddn.com/17-8-9/15465607.jpg)



*	requests.get(url, params=None, **kwargs)
*	返回Response对象

![](http://7xrc1w.com1.z0.glb.clouddn.com/17-8-9/67101570.jpg)

*	网页http header未设置编码charset时，默认为ISO-8859-1
*	r.apparent_encoding是解析网页内容获取编码方式，r.encoding是猜的
*	异常

![](http://7xrc1w.com1.z0.glb.clouddn.com/17-8-9/39218317.jpg)

*	r.raise_for_status()	非200时产生异常
*	爬取网页的框架：
	
		import requests
	
		def getHTMLText(url):
			try:
				r = requests.get(url,timeout=30)
				r.raise_for_status()
				r.encoding = r.apparent_encoding
				return r.text
			except:
				return "产生异常"

		if __name__ == "__main__":
			url = ""
			getHTMLText(url)	

*	Http的主要操作

![](http://7xrc1w.com1.z0.glb.clouddn.com/17-8-9/36533995.jpg)

*	Http跟request库的对应

![](http://7xrc1w.com1.z0.glb.clouddn.com/17-8-9/73579365.jpg)

*	req = requests.request(method, url, **kwargs)


		参数：
			url:
			method: Get/HEAD/POST/PUT/PATCH/delete/OPTIONS
			**kwargs:
				params: 字典或字节序列，作为参数加到url中
				data: 字典，字节序列或文件对象，作为Request对象的内容
				json: JSON数据，作为Request对象的内容
				headers: 字典，HTTP定制头
				cookies: 字典或CookieJar,Request中的cookie
				auth: 元组，支持HTTP认证功能
				files: 字典类型，传输文件
				timeout: 设置超时，单位是秒
				proxies: 字典类型，设定访问代理服务器，可以增加登录认证
				allow_redirects: True/False, 默认为True, 是否重定向
				stream: True/False, 默认为True，立即下载
				verify: True/False, 默认为True,	认证SSL开关
				cert: 本地SSL证书路径

*	其他方法

		requests.get(url, params=None, **kwargs)
		requests.head(url, **kwargs)
		requests.post(url, data=None, json=None, **kwargs)
		requests.put(url, data=None, **kwargs)
		requests.delete(url, **kwargs)


##二、Robots协议

*	Robots Exclusion Standard
	

##三、BeautifulSoup库

###1.解析器

![](http://7xrc1w.com1.z0.glb.clouddn.com/17-8-10/16382355.jpg)

###2.基本元素

![](http://7xrc1w.com1.z0.glb.clouddn.com/17-8-10/17068574.jpg)

###3.HTML遍历

*	下行遍历： 
	
		.contents: 	列表类型，包括换行 
		.children: 	迭代类型，for—in遍历
		.descendants：   迭代类型，for-in遍历 
*	上行遍历： 

		.parent：    当前标签的父标签
		.parents:    所有父辈标签
*	平行遍历:

		.next_sibling:    下一个	
		.previous_sibling:    上一个
		.next_siblings：    之后的
		.previous_siblings： 之前的
###4.格式化

*	soup.prettify()对标签和内容均可进行格式化
*	编码在python3中没得问题

###5.信息标记

*	三种形式: XML、JSON、 YMAL	

		XML:	Internet上的信息交互与传递
		JSON:	移动应用端和节点的信息通信，缺点是没注释
		YMAL:	用于各类系统的配置文件,有注释，易读

###6.信息提取方法

*	解析标记，再提取
*	直接提取
*	融合方法，先解析标记，再解析标记中的信息

###7.HTML内容查找

*	<>.find_all(name, attrs, recursive, string, **kwargs )
*	<>()		//缩写形式
*	其他方法:

![](http://7xrc1w.com1.z0.glb.clouddn.com/17-8-11/80415026.jpg)


##四、正则表达式库Re

###1.常用匹配

![](http://7xrc1w.com1.z0.glb.clouddn.com/17-8-14/89434438.jpg)

![](http://7xrc1w.com1.z0.glb.clouddn.com/17-8-14/10915423.jpg)

###2.经典匹配

![](http://7xrc1w.com1.z0.glb.clouddn.com/17-8-14/19849960.jpg)

###3.Re库两种使用方法
*	函数式：
	
		res = re.search(pattern, str, flags)

![](http://7xrc1w.com1.z0.glb.clouddn.com/17-8-14/45122851.jpg)

*	面向对象式：

		regex = re.compile(pattern, flags)
		res = regex.search(str)
![](http://7xrc1w.com1.z0.glb.clouddn.com/17-8-14/19679947.jpg )

###4.Match对象

*	四个属性： .string  .re	.po	 .endpos
*	四个方法： .group(0) .start() .end() .span()

###5.最小匹配

*	Re库默认是贪婪匹配
*	使用?来得到最小匹配
*	*?    +?   ??   {m,n}?


##五、Scrapy框架

###1.5+2架构

![](http://7xrc1w.com1.z0.glb.clouddn.com/17-8-15/40812332.jpg)

###2.各模块介绍

*	ENGINE

		控制所有模块间的数据流
		根据条件触发事件
*	DOWNLOADER
		
		根据请求下载网页
		不需要用户下载
*	ITEM PIPELINES
		
		对所有爬取请求进行调度管理
*	Spider

		解析Downloader返回的响应(response)
		产生爬取项(scraped item)
		产生额外的爬取请求(request)
*	Item Pipelines
	
		以流水线方式处理Spider产生的爬取项
		由一组操作顺序组成，类似流水线，每个操作类型是一个Item Pipeline类型
		可能操作包括：清理、检验和查重爬取项中的HTML数据，将数据存储到数据库
*	Downloader MiddleWare				
	
		实施Engine, Scheduler和Downloader之间进行用户可配置的控制
		修改、丢弃、新增请求或响应
*	Spider MiddleWare

		对请求和爬取项再处理
		修改、丢弃和新增请求或爬取项

###3.Scrapy命令

*	>scrapy <command> [options] [args]
*	Scrapy更多的是一个后台框架，因此采用命令行的形式

![](http://7xrc1w.com1.z0.glb.clouddn.com/17-8-15/72653252.jpg)

###4.Scrapy基本使用

*	创建工程: >scrapy startproject hellospider

		目录结构:
			hellospider/
				scrapy.cfg          --部署Scrapy爬虫的配置文件
				hellospider/        --scrapy框架的用户自定义Python目录
					__init__.py
					items.py        --Items代码模板
					middlewares.py  --Middlewares代码模板
					pipelines.py    --Piplines代码模板
					settings.py     --爬虫配置文件
					spiders/		--Spider代码模板目录

*	创建一个Spider爬虫: >scrapy genspider demo hellospide.io

		Spider目录:
			spiders/
				__init__.py        --初始化文件
				__pycache__        --缓存
				demo.py            --自己的文件
*	配置自己的Spider

###5.类

*	Request类: class scrapy.http.Request()

		Request对象表示Http请求，Spider生成，Downloader执行
		属性:
			.url .method .headers .body .meta .copy()

*	Response类: class scrapy.http.Response()

		Response对象表示Hrttp响应，Downloader生成，Spider处理
		属性:
			.url .status .headers .body .flags .request .copy()

*	Item类: class scrapy.item.Item()

		Item对象表示从HTML中提取到的信息内容
		Spider生成，Item Pipeline处理
		类似字典，可按字典类型处理


		

		

	 