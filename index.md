---
layout: page
title: Leisurely
tagline: 内心强大才能无懈可击！
---
{% include JB/setup %}

<script type="text/javascript" src="js/jquery.pngFix.js"></script>
<script type="text/javascript">$(document).ready(function(){ $(document).pngFix(); });</script>
<script type="text/javascript" src="js/swfobject.js"></script>

<script type="text/javascript">
var flashvars = {};
flashvars.xml = "config.xml";
flashvars.font = "font.swf";
var attributes = {};
attributes.wmode = "transparent";
attributes.id = "slider";
swfobject.embedSWF("design3edge.swf", "content_slider", "575", "265", "9", "expressInstall.swf", flashvars, attributes);
</script>


<div>
<div style="float:left;width:50%">
<img src="myself.png" align="left"/></div>

<span style="align: right; margin-left:2em; text-align:center; font-family: KaiTi; font-weight: bold; line-height:1.5em;font-size:20pt;">
大家好，我是马新成，毕业于河北科技大学信息学院。现就读于北京理工大学信息与电子学院，攻读硕士学位。隶属于信息安全与对抗实验中心<a href="http://www.isclab.org">官方网站</a>。个人主研数据挖掘，机器学习方向。个人兴趣编程、运动。熟悉C,C++,PHP,JAVA,MATLAB,R等多种编程语言，熟练使用eclipse,vs2010,RStudio等编程环境。有一年多的项目经验。热衷于足球活动。关注中国足球发展。</span>
</div>
<br/>

<table style="width:100%">
	<tr>
		<td style="width:50%">
<span style="float:left;font-family:KaiTi;font-size:18pt">
我的近期博客					
</span>
<table style="width:100%;height:275px;font-family:KaiTi;font-size:16pt">
  {% for post in site.posts %}
	<tr>
		<td style="width:5%" align="left"><li></li></td>
		<td style="width:25%" align="left"><span>{{ post.date | date_to_string }}</span></td>
		<td style="width:5%" align="left">&raquo;</td>
		<td style="width:65%" align="left"><a style="align: left;" href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></td>
	</tr>
  {% endfor %}
</table>
		</td>
		<td style="width:50%">

<div style="float:right" id="content_slider"> <a href="http://www.adobe.com/go/getflashplayer"> <img src="http://www.adobe.com/images/shared/download_buttons/get_flash_player.gif" alt="" /> </a> </div>
		</td>
	</tr>
</table>