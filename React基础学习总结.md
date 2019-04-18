## React 基础学习总结
### 1、创建虚拟DOM对象的两种方式
* React.createElement(type, props, ...children)
* <h1></h1> jsx语法

### 2、React 的 jsx 语法
* 作用：用来创建虚拟DOM对象
* 语法：
	* 以<开头就会去解析，如果式html同名标签就解析html同名元素，如果不是就以其他方式解析
	* 以{开头就会去解析，将其中的代码当作js代码解析
		* if / for循环 不能用

### 3、定义组件两种方式
* 工厂函数 --> 简单组件
	```
	function MyComponent() {
		return <h1></h1>
	}
	```
* ES6类 --> 复杂组件
	```
	class MyComponent extends React.Component{
		render() {
			return <h1></h1>
		}
	}
	```
* 注意事项：
	* 组件首字母大写
	* 标签必须是闭合的
	* 有且只有一个根标签

### 4、React 组件的实例对象上 三大属性（what why how）
* state
	* 作用：	
		* 用来定义组件内部状态数据
		* 用来更新页面
	* 使用：
		* 初始化  在constructor中 this.state = {xxx: xxx}
		* 读取 this.state.xxx
		* 更新 this.setState({xxx: xxx})
* props
	* 作用：
		* 用来组件外向组件内传递数据
	* 使用：
		* 约束属性的类型和必要性 static propTypes = {xxx: PropTypes.func.isRequired}
		* 定义属性的默认值 static defaultProps = {xxx: xxx}
		* 读取 this.props.xxx
		* 设置 <List name={xxx}>
* refs
	* 作用：
		* 用来获取DOM元素
	* 使用：
		* 设置： 
			* 在constructor中 this.xxx = React.createRef()
			* 在虚拟DOM对象上 <input ref={this.xxx} />
		* 使用：this.xxx.current  
* 属性扩展:
    * static属性 不会传送给实例对象,永远在组件(类)上
    * 普通属性   会传给实例对象
### 5、组件化编码流程和套路
1. 拆分组件: 根据页面功能进行拆分
  App  
  AddTodo  
  TodoList  
2. 实现静态组件  
  先实现大的组件（最外层组件），再实现里面的组件。   
  有一个基本的显示效果
3. 实现动态组件  
  - 需不需要定义状态数据？ 
    看页面是否有变化，有变化就要定义状态数据  
  - 状态数据定义再哪里？   
    如果数据是单个组件需要，就定义再单个组件内  
    如果数据是多个组件需要，就定义再公共的父组件中
  - 状态数据定义成什么？  
    定义成对象、数组、基本数据类型。  
    方便插入数据和遍历展示，所以用数组
  - 子组件如何操作父组件的数据？  
    父组件定义操作数据的方法（数据再哪，操作数据的就在在哪）  
    父组件将操作数据的方法传给子组件，子组件调用就改父组件的数据
4. 组件特别注意事项:
	* 1)	组件内置的方法中的this为组件对象
	* 2)	在组件类中自定义的方法中this为null
			a.	强制绑定this: 通过函数对象的bind()
			b.	箭头函数(ES6模块化编码时才能使用)
 		
### 6、 收集表单数据(受控组件与非受控组件)
* 受控组件(官方推荐使用)
	* 定义组件状态,绑定触发事件,再通过事件目标信息更新组件状态
* 非受控组件
	* 通过ref操作DOM节点的方式操作form信息
* [组件间的数据传输(重点)--------->](https://blog.csdn.net/yusirxiaer/article/details/82924454)
  1. 父组件传送给子组件	--利用props属性传值
  2. 子组件对父组件传值 简单来说就是利用回调来完成
  3. 兄弟之间传值      传值者先将值传给父组件,再由父组件传送给需要收值者
### 7、 组件的生命周期(Component-lifecycle)
* 概念:
	*
	*
* 初始化加载,生命周期函数执行顺序	
	1. construtor (只会执行一次)
		* 初始化状态数据
		* 初始话Rreat.createRef()
		* 绑定自定义函数this指向
	2. componetWillMount (18将废弃) (只会执行一次)
	3. Render 渲染DOM (每当组件状态有变化就执行)
	4. componetDidMout (只会执行一次)
		* 发送请求
		* 设置异步任务 ---> 绑定事件或者设置定时器
* 组件接收数据,生命周期函数执行顺序
	0. componentWillRevivceProps  (将废弃)
	1. shouldComponentUpdate (this.setState)
		* 专门用来做React性能优化的：将之前的状态/属性和当前的状态/属性进行对比，如果一样，就不更新，如果不一样就更新
    * 返回值为true就更新
    * 返回值为false就不更新 
	2. componentDidUpdate
		* 可以获取更新后DOM元素,进而进行操作
	3. render()
* 组件强制更新,执行顺序 
  1. componentWillUpdate  (this.forceUpdate)   将废弃
	2. render()
	3. componentDidUpate() 
* 组件将移出
	1. componentWillUnmout  (unmountComponentAtNode  1秒执行) 
		* 做一些首尾工作,清除定时器,局部变量,取消ajax请求	
### [Diff算法------->](https://zhuanlan.zhihu.com/p/20346379)  
1. 总结:
	* React 通过制定大胆的 diff 策略，将 O(n3) 复杂度的问题转换成 O(n) 复杂度的问题；

	* React 通过分层求异的策略，对 tree diff 进行算法优化；

  * React 通过相同类生成相似树形结构，不同类生成不同树形结构的策略，对 component diff 进行算法优化；

	* React 通过设置唯一 key的策略，对 element diff 进行算法优化；

  * 建议，在开发组件时，保持稳定的 DOM 结构会有助于性能的提升；

	* 建议，在开发过程中，尽量减少类似将最后一个节点移动到列表首部的操作，当节点数量过大或更新操作过于频繁时，在一定程度上会影响 React 的渲染性能。
2. 	作用:
 	* 最小化页面重绘、减少重排重绘的次数
	
### key 与 index 对比
1. 为什么列表的key尽量不要用index
  * 简单来说: 当数组中的数据发生变化时: React 比较更新前后的元素 key 值，
  * 如果相同则更新，如果不同则销毁之前的，重新创建一个元素

2. 结论：
  * 如果今后需要往数组最前面插入数据，必须用id作为key的值，
  * 如果不是，而是往最后追加，可以用index作为key的值，（如果数据中有id属性，就用id）

### react-scaff 脚手架
1.简述:
	* 1)	xxx脚手架: 用来帮助程序员快速创建一个基于xxx库的模板项目
		* a.	包含了所有需要的配置
		* b.	指定好了所有的依赖
		* c.	可以直接安装/编译/运行一个简单效果
	* 2)	react提供了一个用于创建react项目的脚手架库: create-react-app
	* 3)	项目的整体技术架构为:  react + webpack + es6 + eslint + babel
	* 4)	使用脚手架开发的项目的特点: 模块化, 组件化, 工程化
2. 安装启动:
```
npm install -g create-react-app
create-react-app hello-react
cd hello-react
npm start

```
3. json配置含义:
```
"scripts": {
    "start": "react-scripts start",  //启动服务器端口监听
    "build": "react-scripts build", //生产环境指令
    "test": "react-scripts test",   // 测试文件是否有问题
    "eject": "react-scripts eject"  //会webpack配置打包,在要大量修改时使用(一般不用)
  },
```
### PubSubJS 利用第三方库组件进行交互

### antD-UI构建库项目
1. 创建项目,引入adtd
   * create-react-app react-admin
	 * npm i antd 
2. 在根目录配置按需打包文件  config-overrides.js
   * 安装: yarn add react-app-rewired customize-cra babel-plugin-import -D
	 * 配置: config-overrides.js
	 ```
	 const { override, fixBabelImports} = require('customize-cra');

		module.exports = override(
			fixBabelImports('import', {
				libraryName: 'antd',
				libraryDirectory: 'es',
				style: true,
			}),
		);

	 ```
3. 在应用中使用antd组件
4. 自定义antd主题
	 * 安装: yarn add less less-loader -D
	 * 功能: 编译less,和主题颜色配置
5. 引入路由
   * 安装: yarn add react-router-dom 
	 * 配置路由:  项目应该首先设置路由	 

6. 静态组件引入
	 * 按需引入 	
	 ```
	 import {Form, Icon, Input, Button} from 'antd'    //按需引入
	 const Item = Form.Item;   //替换成Item

	 ```
7. 表单验证
	 * 利用高阶函数 给Form创建form属性 
	 ```
	@Form.create()
	class Login extends Component {...}
	export default Login	 
	 ```
	 * 引入验证函数	
	 ``` 
	 		 // 引入	
	 		 render() {
        const { getFieldDecorator } = this.props.form;
				...
			 // 验证语法
			 
			 	
	 ```
	 
#### antd-UI项目包管理
0. antd-UI下载
	yarn add antd
1. 路由管理
	react-router-dom  
2. 组件按需打包
	react-app-rewired -D 
	customize-cra -D
	babel-plugin-import -D   
3. 修改主题颜色,编译文件
	less less-loader -D
4. mongodb数据库
5. postman接口测试
6. ajax请求
	axios
7.	本地存储
		store
8. 文件路径配置	
	node原生模块 path
9. 轻量的处理时间和日期库
	apm i dayjs --save
10. 跨域处理...
	npm i jsonp
### redux状态管理	
1. React Component 组件
  * react-redux的Provider时store的抽象实例对象
  * 使用react-redux 的connect方法连接redux的store
2. actions creator 事件行为定义,创造新的store行为
3. reducers 新状态生成,并不更新
  * redux的combineReducers方法将处理后多状态同时返回给store 	
4. store   存储比较新旧状态	
  * redux的createStore方法将reducers的新状态创建为新的store
  * redux的applyMiddleware方法应用中间件
  * redux-thunk是一个redux-store日志记录的中间件
  * redux-devtools-extension的composeWithDevTools是一个调试扩展工具的方法