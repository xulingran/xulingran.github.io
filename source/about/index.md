---
title: about
date: 2020-04-24 17:35:48
---
# 这是一个个人博客哒
我会在这个博客上更新些技术和学习方面的文章
**如果有什么写的不好的地方，**~~你来打我鸭~~    请多谅解
> emmm
<html lang="en">
<style type="text/css">
	*{margin:0;padding:0}
	.post-body{overflow-wrap:break-word;line-height:2;text-align:justify;font-size:1.125em}
	@media(min-width:992px){
		.post-body{text-align:justify}}
	@media(min-width:1200px){
		.post-body{font-size:1.125em}}
	div{display:block}
	.note{margin-bottom:20px;position:relative;border-radius:3px;padding:15px;border-width:1px;border-style:solid;border-image:initial}
	.success{color:#3c763d;background:#dff0d8;border-color:#d0e6be}
	.primary{background:#f3daff;border-color:#e1c2ff;color:#6f42c1}
	p{letter-spacing:normal;margin:0 0 20px}
	p:last-child{margin-bottom:0}
	p:first-child{margin-top:0}
</style>
<script language=javascript>
	function siteTime(){        
		window.setTimeout("siteTime()", 1000);
		var seconds = 1000;
		var minutes = seconds * 60;
		var hours = minutes * 60;
		var days = hours * 24;
		var years = days * 365;
		var today = new Date();
		var todayYear = today.getFullYear();
		var todayMonth = today.getMonth()+1;
		var todayDate = today.getDate();
		var todayHour = today.getHours();
		var todayMinute = today.getMinutes();
		var todaySecond = today.getSeconds();
		/* Date.UTC() -- 返回date对象距世界标准时间(UTC)1970年1月1日午夜之间的毫秒数(时间戳)
		year - 作为date对象的年份，为4位年份值
		month - 0-11之间的整数，做为date对象的月份
		day - 1-31之间的整数，做为date对象的天数
		hours - 0(午夜24点)-23之间的整数，做为date对象的小时数
		minutes - 0-59之间的整数，做为date对象的分钟数
		seconds - 0-59之间的整数，做为date对象的秒数
		microseconds - 0-999之间的整数，做为date对象的毫秒数 */
		var year = 2020//document.getElementById("year").innerHTML;
		var month = 04//document.getElementById("month").innerHTML;
		var day = 20//document.getElementById("day").innerHTML;
		var hour = 09//document.getElementById("hour").innerHTML;
		var minute = 00//document.getElementById("minute").innerHTML;
		var second = 00//document.getElementById("second").innerHTML;//北京时间2018-2-13 00:00:00
		var t1 = Date.UTC(year,month,day,hour,minute,second); 
		var t2 = Date.UTC(todayYear,todayMonth,todayDate,todayHour,todayMinute,todaySecond);
		var diff = t2-t1;
		var diffYears = Math.floor(diff/years);
		var diffDays = Math.floor((diff/days)-diffYears*365);
		var diffHours = Math.floor((diff-(diffYears*365+diffDays)*days)/hours);
		var diffMinutes = Math.floor((diff-(diffYears*365+diffDays)*days-diffHours*hours)/minutes);
		var diffSeconds = Math.floor((diff-(diffYears*365+diffDays)*days-diffHours*hours-diffMinutes*minutes)/seconds);
		if(diffYears==0){
		document.getElementById("sitetime").innerHTML=/*+diffYears+" year "*/+diffDays+" 日 "+diffHours+" 小时 "+diffMinutes+" 分 "+diffSeconds+" 秒";
		} else{
		document.getElementById("sitetime").innerHTML=diffYears+" 年 "+diffDays+" 日 "+diffHours+" 小时 "+diffMinutes+" 分 "+diffSeconds+" 秒";
		}
	}
	//siteTime(document.getElementById("year").innerHTML,document.getElementById("year").innerHTML,document.getElementById("year").innerHTML,document.getElementById("year").innerHTML,document.getElementById("year").innerHTML,0);
	siteTime();
	</script>
</head>

<body class="post-body">
	<div class="note primary">
		<p> 本站期待你的到来已经 <span id="sitetime">已经运行了一年多了</span></p>
	</div>
</body>

</html>