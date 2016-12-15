---
title: JavaScript高级程序设计(3)
tags: JavaScript
---

 
# Ajax
技术的核心是XMLHttpRequest对象
XHR的用法，首先要调用的第一个方法是open(),它接受3个参数，包括要发送的请求类型，请求URL，是否采用异步发送请求。

xhr.open(“get”，URL，false)；
调用open()方法不会真正发送请求，而只是启动了一个请求以备发送。

xhr.send() 该方法接收一个参数，即要发送的数据。如果不需要发送数据，则必须传入null，因为这个参数对浏览器是必须的。
由于是同步的，所以JavaScript代码会等到服务器响应后再执行。
响应数据会自动填充XHR对象的属性：

* responseText 返回的主体文本
* responseXML 响应数据的XML文档
* status HTTP状态

我们经常还是要发送异步请求，让JavaScript继续执行，而不必等待响应，可以通过检测XHR对象的readyState属性，表明请求/响应过程的活动阶段

* 0 还未调用open()
* 1 启动，调用open()还未调用send()方法
* 2 发送 已经调用send() 并未收到响应
* 3 接收 接收到部分响应数据
* 4 完成 已经接收到全部响应数据



readyState属性改变时会触发一次readystatechange事件
> 必须在调用open()前指定onreadystatechange事件处理程序，此时open方法里面的参数为true

## HTTP头部信息
* Accept：浏览器能处理的内容类型
* Connection:浏览器与服务器之间连接的类型
* Cookie：当前页面设置的任何cookie
* Host：发出请求的页面所在域
* Referer 发出请求页面的URL
可以设置请求包头的信息
xhr.setRequestHeader("MyHeader","MyValue");
以上代码必须在open()之后，send()之前；
GET从服务器获取数据
POST向服务器提交数据
> 与GET请求相比，POST请求消耗资源更多些，发送相同的数据，GET请求速度是POST请求的2倍

## CORS（Cross-Origin Resource Sharing)跨域资源共享
其基本思想为使用自定义的HTTP头部让浏览器与服务器进行沟通。决定请求响应成功或失败。

其他跨域技术
上述第一种跨域请求技术是使用\<img\>标签，一个网页可以从任何网页中加载图像，不用担心跨域，动态创建图像Ping只能发送GET请求，而且无法访问服务器的响应文本，图像Ping只能用于浏览器与服务器的单向通信。

## JSONP
是JSON with padding (填充式JSON 或参数式JSON）的简写，是包含在函数调用中的JSON
JSONP是由两部分组成：回调函数和数据
回调函数为响应到来时在页面调用的函数
数据是传入回调函数中的数据
http://xx.xx.xx/json/?callback=handleResponse
\<script\>元素与\<img\>元素类似，有能力不受限制地从其他域加载资源。
JSONP使用例子：
``` js
function handleResponse(response){
		alert("You are at IP address" +response.ip +",which is "+response.city +"," +response.region_name);
	var script =document.createElment("script")；
script.src="http://xx.xx.xx/json/?callback=handleResponse";
document.body.insertBefore(script ,document.body.firstChild);
```
优点在于直接访问响应文本，支持浏览器与服务器间双向通信

## Comet技术
一种服务器向页面推送数据的技术
适合处理体育比赛或者股票信息
两种实现Comet的方式：

* 长轮询
* HTTP流
