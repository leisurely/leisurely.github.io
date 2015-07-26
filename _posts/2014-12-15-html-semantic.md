---
layout: post
title: "WEB基本概念"
description: "开始个人博客"
category: 
tags: [hello world]
---
{% include JB/setup %}

#HTML
##概念

根据内容的结构化（内容语义化），选择合适的标签（代码语义化）便于<strong>开发者阅读和写出更优雅的代码</strong>的同时让<strong>浏览器的爬虫和机器很好地解析</strong>。

##目的

1. 为了在没有CSS的情况下，页面也能呈现出很好地内容结构、代码结构:为了裸奔时好看；

2. 用户体验：例如title、alt用于解释名词或解释图片信息、label标签的活用；

3. 有利于SEO：和搜索引擎建立良好沟通，有助于爬虫抓取更多的有效信息：爬虫依赖于标签来确定上下文和各个关键字的权重；

4. 方便其他设备解析（如屏幕阅读器、盲人阅读器、移动设备）以意义的方式来渲染网页；

5. 便于团队开发和维护，语义化更具可读性，是下一步吧网页的重要动向，遵循W3C标准的团队都遵循这个标准，可以减少差异化。

##注意事项

1. 尽可能少的使用无语义的标签div和span；

2. 在语义不明显时，既可以使用div或者p时，尽量用p, 因为p在默认情况下有上下间距，对兼容特殊终端有利；

3. 不要使用纯样式标签，如：b、font、u等，改用css设置。

4. 需要强调的文本，可以包含在strong或者em标签中（浏览器预设样式，能用CSS指定就不用他们），strong默认样式是加粗（不要用b），em是斜体（不用i）；

5. 使用表格时，标题要用caption，表头用thead，主体部分用tbody包围，尾部用tfoot包围。表头和一般单元格要区分开，表头用th，单元格用td；

6. 表单域要用fieldset标签包起来，并用legend标签说明表单的用途；

7. 每个input标签对应的说明文本都需要使用label标签，并且通过为input设置id属性，在lable标签中设置for=someld来让说明文本和相对应的input关联起来

##HTML5新增

HTML5新增内容，详见<a href="http://www.html5jscss.com/html5-semantics-section.html">HTML 5的革新——语义化标签(一)</a>

#CSS
##样式优先级
多重样式（Multiple Styles）：如果外部样式、内部样式和内联样式同时应用于同一个元素，就是使多重样式的情况。一般情况下，优先级如下：

（外部样式） External style sheet < （内部样式）Internal style sheet < （内联样式）Inline style

有个例外的情况，就是如果外部样式放在内部样式的后面，则外部样式将覆盖内部样式。示例如下：

	<head>
		<style type="text/css">
		/*内部样式*/
		h3{color:green}
		</style>
		
		<!-- 外部样式 style.css -->
		<link rel="stylesheet" type="text/css" href="style.css"/>
		<!-- 设置：h3{color:blue;} -->
	</head>
	<body>
		<h3>测试！</h3>
	</body>
	
##选择器的优先权

<p><img src="/img/css选择器.png"/></p>

解释：

1. 内联样式表的权值最高 1000；

2. ID 选择器的权值为 100

3. Class 类选择器的权值为 10

4. HTML 标签选择器的权值为 1

利用选择器的权值进行计算比较，示例如下：


	<html>
	  <head>
		<style type="text/css">
			#redP p {
				 /* 权值 = 100+1=101 */
				 color:#F00;  /* 红色 */
			}
	 
			#redP .red em {
				 /* 权值 = 100+10+1=111 */
				 color:#00F; /* 蓝色 */
	 
			}
	 
			#redP p span em {
				 /* 权值 = 100+1+1+1=103 */
				 color:#FF0;/*黄色*/
			}
		</style>
	  </head>
	  <body>
		 <div id="redP">
			<p class="red">red
			   <span><em>em red</em></span>
			</p>
			<p>red</p>
		 </div>
	  </body>
	</html>
	
结果：<em> 标签内的数据显示为蓝色。

##css优先级法则：
1. 选择器都有一个权值，权值越大越优先；

2. 当权值相等时，后出现的样式表设置要优于先出现的样式表设置；

3. 创作者的规则高于浏览者：即网页编写者设置的CSS 样式的优先权高于浏览器所设置的样式；

4. 继承的CSS 样式不如后来指定的CSS 样式；

5. 在同一组属性设置中标有<strong>!important</strong>规则的优先级最大；示例如下：

	<html>
	  <head>
		<style type="text/css">
		 #redP p{
			/*两个color属性在同一组*/
			color:#00f !important; /* 优先级最大 */
			color:#f00;
		 }
		</style>
	  </head>
	  <body>
		 <div id="redP">
		   <p>color</p>
		   <p>color</p>
		 </div>
	  </body>
	</html>

结果：在Firefox 下显示为蓝色；在IE  6 下显示为红色；

##使用脚本添加样式

当在连接外部样式后，再在其后面使用JavaScript 脚本插入内部样式时（即内部样式使用脚本创建），IE 浏览器就表现出它的另类了。代码如下：

	<html>
	<head>
	  <title> demo </title>
	  <meta name="Author" content="xugang" />
	 
	  <!-- 添加外部CSS 样式 -->
	  <link rel="stylesheet" href="styles.css" type="text/css" />
	  <!-- 在外部的styles.css文件中，代码如下：
		   h3 {color:blue;}
	  -->
	 
	  <!-- 使用javascript 创建内部CSS 样式 -->
	  <script type="text/javascript">
	  <!--
		(function(){
			var agent = window.navigator.userAgent.toLowerCase();
			var is_op = (agent.indexOf("opera") != -1);
			var is_ie = (agent.indexOf("msie") != -1) && document.all && !is_op;
			var is_ch = (agent.indexOf("chrome") != -1);
	 
			var cssStr="h3 {color:green;}";
			var s=document.createElement("style");
			var head=document.getElementsByTagName("head").item(0);
			var link=document.getElementsByTagName("link");
			link=link.item(0);
	 
			if(is_ie)
			{
				if(link)
					head.insertBefore(s,link);
				else
					head.appendChild(s);
				document.styleSheets.item(document.styleSheets.length-1).cssText=cssStr;
			}
			else if(is_ch)
			{
				var t=document.createTextNode();
				t.nodeValue=cssStr;
				s.appendChild(t);
				head.insertBefore(s,link);
			}
			else
			{
				s.innerHTML=cssStr;
				head.insertBefore(s,link);
			}
		})();
	  //-->
	  </script>
	</head>
	<body>
	  <h3>在IE中我是绿色，非IE浏览器下我是蓝色！</h3>
	</body>
	</html>

结果：在Firefox / Chrome / Safari / Opera 中，文字都是蓝色的。而在IE 浏览器中，文字却是绿色的。

##附加
在IE 中添加样式内容的JavaScript 代码：
	var s=document.createElement("style");
	var head=document.getElementsByTagName("head").item(0);
	var link=document.getElementsByTagName("link").item(0);
	 
	head.insertBefore(s,link);
	/* 注意：在IE 中，
	   虽然代码是将<style>插入在<link>之前，
	   但实际内存中，<style>却在<link>之后。
	   这也是“IE中奇怪的应用CSS的BUG”之所在！
	*/
	 
	var oStyleSheet = document.styleSheets[0];
	//这实际是在<link>的外部样式中追加
	oStyleSheet.addRule("h3","color:green;");
	alert(oStyleSheet.rules[0].style.cssText);
	alert(document.styleSheets[0].rules[0].style.cssText);
	 
	//方式2
	var cssStr="h3 {color:green;}";
	document.styleSheets.item(document.styleSheets.length-1).cssText=cssStr;

##IE浏览器下载或者渲染的顺序可能如下：

●   IE 下载的顺序是从上到下；

●   JavaScript 函数的执行会阻塞IE 的下载；

●   IE 渲染的顺序也是从上到下；

●   IE 的下载和渲染是同时进行的；

●   在渲染到页面的某一部分时，其上面的所有部分都已经下载完成（但并不是说所有相关联的元素都已经下载完。）

●   在下载过程中，如果遇到某一标签是嵌入文件，并且文件是具有语义解释性的（例如：JS脚本，CSS样式），那么此时IE的下载过程会启用单独连接进行下载。并且在下载后进行解析，如果JS、CSS中如有重定义，后面定义的函数将覆盖前面定义的函数。

●   解析过程中，停止页面所有往下元素的下载。样式表文件比较特殊，在其下载完成后，将和以前下载的所有样式表一起进行解析，解析完成后，将对此前所有元素（含以前已经渲染的）重新进行样式渲染。并以此方式一直渲染下去，直到整个页面渲染完成。

●   Firefox 处理下载和渲染的顺序大体相同，只是在细微之处有些差别，例如：iframe 的渲染。

