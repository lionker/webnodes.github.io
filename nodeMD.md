## 一、 node 常用模块
### 1. fs 文件管理
### 2. path 路径管理
### 3. http 协议请求管理

## 二、 mongoDB数据库

### 1). mongoose数据操作基础本逻辑:
	a. 使用mongose模块连接mongoDB相应数据库,没有对应则创建
	b. 创建Schema模式对象,约束创建doc
	c. 创建model实例对象	,即在连接的数据库中创建相应集合
	d. 利用model实例对象(即数据库集合)操作 document.
		
## 三、 express 服务器框架
###	1). middleware中间件
  1. 内置中间件  
		a. express.static(资源文件目录)向外暴露静态资源  
    b. express.urlencoded()  解析post请求的请求体参数，就能通过req.body获取
	2. 第三方中间件
		a. cookie-parser  解析cookie数据
	3. 错误处理中间件
		a. 	(err, req, res, next) => {} 一旦中间件或者路由出问题，就触发错误中间件处理404页面

### 2). Router 中间件模块  (当模块化时可使用)
		
	//创建路由器对象: 相当于一个小型的app应用对象(功能更少)
	
### 3). 基本逻辑步骤:

1. 安装引入express模块,并调用express生成实例对象app;
2. 设置监听端口app.listen
3. 设置请求方式,和监听地址或者路由(route) app.get
4. 使用中间件  app.use  
	  	* 正常中间件使用(内置与第三方)  
		  * 错误处理中间件使用
## 四、 koa2    简化版express框架
	
## 五、 wechart 需求插件

1. request    request-promise-native  (请求处理)

## 六、 Ajax

### 1). 原生ajax请求 

#### 客服端:
  1. 绑定触发事件 
	2. 创建 xhr事件监听 new XMLHttpRequest
	3. 接收响应的的内容 xhr.onreadystatechange
	5. 发送请求				xhr.open	
	4. 设置请求信息		xhr.setRequestHeader
	5. 	发送请求      xhr.send()  
#### 服务端:  处理请求

### 2). JQuery集成ajax请求
