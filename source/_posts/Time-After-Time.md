---
title: Javascript 高级程序设计
tags: JavaScript
---
# Javascript 高级程序设计（一）

&lt;script&gt;中内嵌部分代码中不能用&lt;/script&gt;，因为解释器遇到script后就会解释为script脚本停止。
&lt;script type=text/javascript src=“a.js”&gt;这个时候会忽略后面的内嵌javascript转而变成引用外部的“a.js”

通常外部引用都要放到head中，例如CSS，但是为了加速页面的加载，javascript的外部引用一般放在&lt;body&gt;的最末尾

也可以用defer属性 延迟加载脚本 
async属性 （HTML5）新增 但是不保证会按照async的属性来加载
写法如下：
``` html
<script type=“text/javascript” async src=“1.js”>
```

不要在异步脚本加载期间修改DOM

异步脚本一定会在页面load后执行，但可能在DOMContentLoaded之前或之后发生。

标识符指的是变量，函数和属性的名字，或者函数的参数。

严格模式 “use strict” 某些不确定行为将得到处理，不安全操作也会抛出异常。

Javascript中的变量为松散类型的，即可以保留任何类型的数据。
给未经声明的变量赋值会在严格模式下抛出ReferenceError错误
严格模式下不能定义名为eval或arguments的变量，否则会导致语法错误
