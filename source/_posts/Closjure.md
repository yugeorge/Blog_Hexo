---
title: JavaScript 高级程序设计(2)
---



# 闭包 Closjure 

> 在函数内部定义了其他函数时，就创建了闭包

> 闭包是为了让函数内部访问外部作用域

当函数返回一个闭包时，这个函数的作用域将会一直在内存中保存直到闭包不再存在。

闭包的例子:
``` js
function parent(){
   var m=50;
   function son(){
        alert(m);
   }
   return son;
}
var s=parent();//将结果保存在全局里
s();//50
```

## this对象与闭包的关系：
每个函数在被调用时，其活动对象就会自动获得两个特殊变量：this和arguments，内部函数永远无法直接访问外部函数中的这两个变量，所以建议用闭包的方式去访问这两个变量

闭包引起的内存泄露问题,回收闭包中的内存问题：


用作块级作用域（私有作用域）的匿名函数语法：
``` js
(function(){
		//模拟块级作用域
})();
```

前面圆括号里面是一个函数表达式，后面表示立即调用这个匿名函数。

javascript中的私有变量，函数中定义的变量，可以访问私有变量和私有函数的公共方法称为特权方法。
例子：
``` js
function myObject(){
		//私有变量和私有函数
		var privateVariable =10;
		function privateFunction(){
			return false;
		}
			//特权方法
		this.publicMethod=function(){
			privateVariable++;
			return privateFunction();
		};
}
```
特权方法作为闭包有权访问在构造函数中定义的所有变量和函数，利用私有成员和特权方法，可以隐藏那些不该被直接修改的数据。

在原型上定义特权方法：
Example：
``` js
(function(){
		var privateVariable =10;
	function privateFunction(){
		return false;
	}
    //构造函数
   MyObject = function(){
	 };
     //特权方法
	MyObject.prototype.publicMethod = function(){
			privateVariable++;
			return privateFunction();
		};
})();
```
上面代码中的私有变量和函数是由实例共享的。
即修改一个实例的变量会影响其他变量。



## 单例（Singleton)模式
只有一个实例的对象，单例一般作为全局对象存在。
以对象字面量的方式创建单例对象：
``` js
		var singelton={
			name:value;
			method:function(){
			     //方法的代码
			}
		}；
```
模块模式通过为单例添加私有变量和特权方法增强

``` js
var singleton=function(){
	var privateVariable=10;
	function privatFunction(){
		return false;
	function privateFunction(){
		return false;
   }
   return {
	//特权方法和属性
          publicProperty:true,
	  publicMethod : function(){
		privateVariable++;
		return privateFunction();
		}
         };
}();
```
  





> 可以使用构造函数模式、原型模式来实现自定义类型的特权方法，也可以使用模块模式、增强的模块模式来实现单例的特权方法