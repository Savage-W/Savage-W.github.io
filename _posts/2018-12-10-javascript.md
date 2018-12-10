---
layout: post
title:  "Canvas绘制雪花效果!"
date:   2018-12-10 22:14:54
categories: JavaScript
tags:  JavaScript
---

* content
{:toc}

`Canvas`时`html `中非常重要的特性在学习它的同时也做了一个 关于雪花的`demo`;

先在`html`中插入`canvas`元素
```
<canvas id="myCanvas" width="1200" height="600"></canvas>
```







且设置它的宽高，接下来我们在`body`结束标签之前添加`JavaScript`，代码如下：

```
var canvas = document.getElementById("myCanvas");//获取canvas元素
var context = canvas.getContext("2d");//返回一个对象，该对象提供了用于在画布上绘画的方法和属性
```
因为`Canvas`本身是没有绘图能力的，所以我们要通过`getContext()`方法返回可绘图对象，即上诉代码中的`context`，后续雪花都将在`context`中进行
接下来，创建一个数组保存所有雪花的信息：
```
var particles = [];//为雪花粒子创建一个数组
for( var i = 0; i<700;i++){//循环700次，生成700粒雪花
	particles.push({//设置雪花的初始位置，方向速度，大小，颜色
		x:Math.random()*window.innerWidth,
		y:Math.random()*window.innerHeight,
		vx:(Math.random()*1-.5),
		vy:(Math.random()*1-.5),
		size:1+Math.random()*10,
		color:"#FFF"
		
	});
}
```
上面代码是对雪花的一个虚拟描述，接下来就是进行绘制，使雪花在画布上显现出来：
```
function timeUpdate(e){
	context.clearRect(0,0,window.innerWidth,window.innerHeight);//清除画布区域
	var particle;
	for(var i = 0; i<700; i++){//循环遍历所有雪花
		particle = particles[i];
		particle.x += particle.vx;//更新雪花的新位置
		particle.y += particle.vy;
		if(particle.x < 0){
			particle.x = window.innerWidth;//当雪花移动到窗口左侧以外时，使其显示在窗口最右侧
		}
		if(particle.x > window.innerWidth){
			particle.x = 0;//当雪花移动到窗口右侧以外时，使其显示在窗口最左侧
		}
		if(particle.y >= window.innerHeight){
			particle.x = 0;//当雪花移动到窗口顶部以外时，使其重新显示在窗口最顶部
		}
		context.fillStyle = particle.color;//设置雪花颜色
	    context.beginPath();//开始绘制雪花
	    context.arc(particle.x,particle.y,particle.size,0,Math.PI*2);//绘制圆形
	    context.closePath();//闭合路径
	    context.fill();//填充颜色

	}
}
setInterval(timeUpdate,40);//每40毫秒执行一次timeUpdate函数
```
然后就成功了，
