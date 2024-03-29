##javascript-this指向问题

1. **箭头函数**
	* 作用: 定义匿名函数
	* 基本语法:
	  * 没有参数: () => console.log('xxxx')
	  * 一个参数: i => i+2
	  * 大于一个参数: (i,j) => i+j
	  * 函数体不用大括号: 默认返回结果
	  * 函数体如果有多个语句, 需要用{}包围，若有需要返回的内容，需要手动返回 
	  
	* 使用场景: 多用来定义回调函数
	
	* 箭头函数的特点：  
	    1、简洁  
	    2、箭头函数没有自己的this，箭头函数的this不是调用的时候决定的，而是在定义的时候处在的对象就是它的this  
	    3、扩展理解： 箭头函数的this看外层的是否有函数，
	        如果有，外层函数的this就是内部箭头函数的this，
	        如果没有，则this是window。

2. **this指向总结**
* 函数直接调用，this指向window（如果是严格模式，是undefined）
* 隐式调用，指向调用它的对象   (a.b.c.Func()的形式调用)
* 显示调用，[call/apply/bind[☚链接]](https://www.cnblogs.com/libin-1/p/5823025.html) 指向传入第一个参数    
* new 调用，指向新创建的实例对象
* 回调函数
  * 事件回调函数 this指向被绑定事件的DOM对象
  * 普通回调函数（定时器，map）：this指向window（如果是严格模式，是undefined）
* 箭头函数：指向离他最近的包裹它的函数的this，如果没有就是window
* 框架中的生命周期函数
  * 生命周期函数this指向组件的实例对象
  * 其他自定义函数this指向undefined  
* 基本class中方法，this指向实例对象