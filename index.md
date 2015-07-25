---
layout: page
title: Leisurely
tagline: 内心强大才能无懈可击！<div style="float:right"><p><SPAN style="color:blue;font-family:楷体" id="Clock"></SPAN></p></div>

---
{% include JB/setup %}
<style type="text/css">
*{padding:0; margin:0;}
#roll{ border:0px solid red;height:280px; margin:10px auto; width:600px; overflow:hidden;list-style:none;}
#roll li{height:40px; padding-left:10px;line-height:30px; border-bottom:0px solid #ddd;}
a{text-decoration:none;color:#0066CC;}
a:hover{ color:#FF0000; text-decoration: underline;} 
</style>
<script type="text/javascript">
function tick() {
var years,months,days,hours, minutes, seconds;
var intYears,intMonths,intDays,intHours, intMinutes, intSeconds;
var today;
today = new Date(); //系统当前时间
intYears = today.getFullYear(); //得到年份,getFullYear()比getYear()更普适
intMonths = today.getMonth() + 1; //得到月份，要加1
intDays = today.getDate(); //得到日期
intHours = today.getHours(); //得到小时 
intMinutes = today.getMinutes(); //得到分钟
intSeconds = today.getSeconds(); //得到秒钟
years = intYears + "年"; 

if(intMonths < 10 ){
months = "0" + intMonths +"月";
} else {
months = intMonths +"月";
}
if(intDays < 10 ){
days = "0" + intDays +"日 ";
} else {
days = intDays + "日 ";
}
if (intHours == 0) {
hours = "00:";
} else if (intHours < 10) {
hours = "0" + intHours+":";
} else {
hours = intHours + ":";
}
if (intMinutes < 10) {
minutes = "0"+intMinutes+":";
} else {
minutes = intMinutes+":";
}
if (intSeconds < 10) {
seconds = "0"+intSeconds+" ";
} else {
seconds = intSeconds+" ";
}
timeString = "北京时间："+years+months+days+hours+minutes+seconds;
Clock.innerHTML = timeString;
window.setTimeout("tick();", 1000);
}
tick();
</script>


<div>
<div style="float:left;width:50%">
<img src="myself.png" align="left"/></div>

<span style="align: right; margin-left:2em; text-align:center; font-family: KaiTi; font-weight: bold; line-height:1.5em;font-size:18pt;">
大家好，我是马新成，毕业于河北科技大学信息学院。现就读于北京理工大学信息与电子学院，攻读硕士学位。隶属于<a href="http://www.isclab.org">信息安全与对抗实验中心</a>。主研数据挖掘，机器学习方向。个人兴趣编程、运动。熟悉C,C++,JAVA等编程语言，PHP,MATLAB,R等脚本语言，熟练使用RStudio，eclipse，vs2010等编程工具，擅长数据可视化工具Echarts和Finereport。有两年多的项目经验。热衷于足球活动。</span>
</div>
<br/>

<table style="width:100%">
	<tr>
		<td style="width:50%">

<ol id="roll" style="float:right">
	{% for post in site.posts %}
    <li><a style="font-size:18pt" href="{{ BASE_PATH }}{{ post.url }}">{{ post.date | date_to_string }} &raquo; {{ post.title }}</a></li>
	{% endfor %}
</ol>
		</td>
		<td style="width:50%">
		<div style="width:50%">
			<video width="528" height="297" controls autoplay loop>
				<source src="myself.mp4" type="video/mp4"></source>
			</video>
			<audio autoplay="autoplay" height="100" width="100" loop>
				<source src="bg.mp3" type="audio/mp3" />
			</audio>
		</div>
		</td>
	</tr>
</table>

<script type="text/javascript">
(function(A){
   function _ROLL(obj){
      this.ele = document.getElementById(obj);
	  this.interval = false;
	  this.currentNode = 0;
	  this.passNode = 0;
	  this.speed = 100;
	  this.childs = _childs(this.ele);
	  this.childHeight = parseInt(_style(this.childs[0])['height']);
	      addEvent(this.ele,'mouseover',function(){
				                               window._loveYR.pause();
											});
		  addEvent(this.ele,'mouseout',function(){
				                               window._loveYR.start(_loveYR.speed);
											});
   }
   function _style(obj){
     return obj.currentStyle || document.defaultView.getComputedStyle(obj,null);
   }
   function _childs(obj){
	  var childs = [];
	  for(var i=0;i<obj.childNodes.length;i++){
		 var _this = obj.childNodes[i];
		 if(_this.nodeType===1){
			childs.push(_this);
		 }
	  }   
	  return childs;
   }
	function addEvent(elem,evt,func){
	   if(-[1,]){
		   elem.addEventListener(evt,func,false);   
	   }else{
		   elem.attachEvent('on'+evt,func);
	   };
	}
	function innerest(elem){
      var c = elem;
	  while(c.childNodes.item(0).nodeType==1){
	      c = c.childNodes.item(0);
	  }
	  return c;
	}
   _ROLL.prototype = {
      start:function(s){
	          var _this = this;
			  _this.speed = s || 100;
		      _this.interval = setInterval(function(){
						    _this.ele.scrollTop += 1;
							_this.passNode++;
							if(_this.passNode%_this.childHeight==0){
								  var o = _this.childs[_this.currentNode] || _this.childs[0];
								  _this.currentNode<(_this.childs.length-1)?_this.currentNode++:_this.currentNode=0;
								  _this.passNode = 0;
								  _this.ele.scrollTop = 0;
								  _this.ele.appendChild(o);
							}
						  },_this.speed);
	  },
	  pause:function(){
		 var _this = this;
	     clearInterval(_this.interval);
	  }
   }
    A.marqueen = function(obj){A._loveYR = new _ROLL(obj); return A._loveYR;}
})(window);
marqueen('roll').start(100/*速度默认100*/);
</script>