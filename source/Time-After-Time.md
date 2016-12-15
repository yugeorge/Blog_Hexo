
# Javascript 高级程序设计

\<script\>中内嵌部分代码中不能用\</script\>，因为解释器遇到script后就会解释为script脚本停止。
\<script type=text/javascript src=“a.js”\>这个时候会忽略后面的内嵌javascript转而变成引用外部的“a.js”

通常外部引用都要放到head中，例如CSS，但是为了加速页面的加载，javascript的外部引用一般放在\<body\>的最末尾

也可以用defer属性 延迟加载脚本 
async属性 （HTML5）新增 但是不保证会按照async的属性来加载
写法如下：
```javascript
`<script type=“text/javascript” async src=“1.js”>
不要在异步脚本加载期间修改DOM
异步脚本一定会在页面load后执行，但可能在DOMContentLoaded之前或之后发生。

标识符 指的是变量，函数和属性的名字，或者函数的参数。

严格模式 “use strict” 某些不确定行为将得到处理，不安全操作也会抛出异常。

Javascript中的变量为松散类型的，即可以保留任何类型的数据。
给未经声明的变量赋值会在严格模式下抛出ReferenceError错误
严格模式下不能定义名为eval或arguments的变量，否则会导致语法错误

ECMAScript基本数据类型 Boolean Number String Undefined Null
复杂数据类型 Object
对没有声明的变量可以使用typeof函数，结果返回的是undefined
Null值表示一个空的对象指针，所以typeof(null)返回值为object
null==u  defined 返回值为真
保存对象的变量还没有真正地保存变量，就应该赋给null值
空字符串”“的Boolean值返回为false
0和NaN的Boolean返回值为false，其余number为true
null的Boolean返回值为false
数值表示 0x 表示十六进制，0开头表示8⃣️进制
NaN除以任何数均为NaN，NaN与任何值都不相等，包括NaN
isNaN()是否为数值 是数值或能转换为数值（”10“ boolean类型true等）返回为true 
三个转换非数值为数值的函数：Number() parseInt() parseFloat()
其中第一个函数适用任何类型
另外两个函数专门用于String类型
Number()函数的返回值 
字符串中只包含数字转换为对应的十进制数字。忽略前面的0
”011“转换为11
字符串为空转换为0
字符串包含其他字符，输出为NaN

parseInt()函数 忽略前面的空格 直到遇见第一个数字，并忽略数字后面的非数字字符，包括小数点，空字符返回NaN
也可以使用第二个参数作为转换时的基数 表示几进制
parseFloat()与parseInt()相似，只是遇到第二个小数点后才认为结束，只解析十进制的值

Sting类型的toString()方法 每个类型都有，除了null与undefined 没有
对于这两个，可以用String()来返回undefined 和null
```javascript
````alert(String(undefined));    //undefined
````alert(String(null)); //null
`对非数值使用一元+/-操作符会将得到的值通过Number方法转换为数字

逻辑与 && 逻辑或 
for in 语句用来枚举对象的类型
例子：
	' for (var propName in window) {
	'	document.write(propName);
	'}

函数定义时，不必一定声明是否需要返回值
函数return后面的语句并不会执行。
JavaScript函数没有重载
JavaScript函数的参数与其他语言并不是那么相似，并不关心参数的数量与类型，因为它们都是被传递到一个数组中，在函数体中可以通过arguments数组来访问这些参数。
例如：
	 function sayHi(a,b){
		alert("Hello"+a+b);
	}
	function sayHi(){
	  alert("Hello " + arguments[0]+arguments[1]);
	}
	//以上两个函数实现相同功能 

不能给基本类型值添加属性，虽然不会报错，但是会输出undefined

typeof 检测数据类型 Instanceof 检测引用类型
基本类型的instance始终会返回false

没有块级作用域
	if（true）{
		 var color ="blue";
	}
		alert(color); //     "blue"

看到4.2 72


访问变量有按值和按引用两种方式，而参数只能按值传递


