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
大家好，我是马新成，毕业于河北科技大学信息学院。现就读于北京理工大学信息与电子学院，攻读硕士学位。隶属于信息安全与对抗实验中心<a href="http://www.isclab.org">官方网站</a>。个人主研数据挖掘，机器学习方向。个人兴趣编程、运动。熟悉C,C++,PHP,JAVA,MATLAB,R等多种编程语言，熟练使用eclipse,vs2010,RStudio等编程环境。有一年多的项目经验。本科有硬件开发背景，熟知keil3，WAVE6000，Quertuas等硬件开发平台。热衷于足球活动。关注中国足球发展。
</div>
<br/>

<div style="width:100%; margin: 10px 50px">
<div style="float:left; width:225px">
<span style="align: right; margin-left:2em; font-family: KaiTi; font-weight: bold; line-height:1em; font-size:18pt">
我的博客
</span>
<ul class="posts" style="float:left;font-family: KaiTi; font-weight: bold; font-size: 12pt">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>
</div>
<div style="float:right; width:575px">

<div style="float:right" id="content_slider"> <a href="http://www.adobe.com/go/getflashplayer"> <img src="http://www.adobe.com/images/shared/download_buttons/get_flash_player.gif" alt="" /> </a> </div>
</div>
