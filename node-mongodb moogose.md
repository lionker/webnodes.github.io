##node

###node指令
	node 	      --进入控制台		
	node -v 	  --查看版本
	node filename --运行文件	

基本概念：
	数据库服务器>>>数据库>>>集合>>>文档
	*可以有很多数据库>可以有多个集合>可以有多个文档(最小单位,操作储存的东西)
##1.mongo 连接mongodb,启动客户端

##2.mongod 用来启动服务器
1.安装MongoDB
	- 安装
	- 配置环境变量
		C:\Program Files\MongoDB\Server\3.2\bin
	- 在c盘根目录
		- 创建一个文件夹 data
		- 在data中创建一个文件夹db
		
	- 打开cmd命令行窗口
		- 输入 mongod 启动mongodb服务器
		- 32位注意：
			启动服务器时，需要输入如下内容
				mongod --storageEngine=mmapv1
				
				mongod --dbpath 数据库路径 --port 端口号


		
	- 在打开一个cmd窗口
		- 输入 mongo 连接mongodb ，出现 > 
		
	- 数据库（database）
		- 数据库的服务器
			- 服务器用来保存数据
			- mongod 用来启动服务器
			
		- 数据库的客户端
			- 客户端用来操作服务器，对数据进行增删改查的操作
			- mongo 用来启动客户端
			
			
	- 将MongoDB设置为系统服务，可以自动在后台启动，不需要每次都手动启动
		1.在c盘根目录创建data
			- 在data下创建db和log文件夹
		2.创建配置文件
			在目录 C:\Program Files\MongoDB\Server\3.2 下添加一个配置文件
			mongod.cfg
		3.以管理员的身份打开命令行窗口	
		
		4.执行如下的命令
			sc.exe create MongoDB binPath= "\"C:\Program Files\MongoDB\Server\3.2\bin\mongod.exe\" --service --config=\"C:\Program Files\MongoDB\Server\3.2\mongod.cfg\"" DisplayName= "MongoDB" start= "auto"
			
			sc.exe create MongoDB binPath= "\"mongod的bin目录\mongod.exe\" --service --config=\"mongo的安装目录\mongod.cfg\"" DisplayName= "MongoDB" start= "auto"
			
		5.启动mongodb服务

		6.如果启动失败，证明上边的操作有误，
			在控制台输入 sc delete MongoDB 删除之前配置的服务
			然后从第一步再来一次


	- 基本概念
		数据库（database）
		集合（collection）
		文档（document）
			- 在MongoDB中，数据库和集合都不需要手动创建，
				当我们创建文档时，如果文档所在的集合或数据库不存在会自动创建数据库和集合
		
	- 基本指令
		show dbs
		show databases
			- 显示当前的所有数据库
		use 数据库名
			- 进入到指定的数据库中
		db
			- db表示的是当前所处的数据库
		show collections
			- 显示数据库中所有的集合
			
	- 数据库的CRUD（增删改查）的操作
		- 向数据库中插入文档
			db.<collection>.insert(doc)
				- 向集合中插入一个文档
				- 例子：向test数据库中的，stus集合中插入一个新的学生对象
					{name:"孙悟空",age:18,gender:"男"}
					db.stus.insert({name:"孙悟空",age:18,gender:"男"})
			
			db.<collection>.find()
				- 查询当前集合中的所有的文档

- 向数据库中插入文档
			- db.collection.insert()
				- insert()可以向集合中插入一个或多个文档
			- db.collection.insertOne()
				- 向集合中插入一个文档
			- db.collection.insertMany()
				- 向集合中插入多个文档
				
		- 查询数据库中的文档
			- db.collection.find()
				- 可以根据指定条件从集合中查询所有符合条件的文档
				- 返回的是一个数组
			- db.collection.findOne()
				- 查询第一个符合条件的文档
				- 返回的是一个对象
			- db.collection.find().count()
				- 查询符合条件的文档的数量
				
		- 修改数据库中的文档
			- db.collection.update()
				- 可以修改、替换集合中的一个或多个文档
			- db.collection.updateOne()
				- 修改集合中的一个文档
			- db.collection.updateMany()
				- 修改集合中的多个文档
			- db.collection.replaceOne()
				- 替换集合中的一个文档
				
		- 删除集合中的文档
			- db.collection.remove()
				- 删除集合中的一个或多个文档（默认删除多个）
			- db.collection.deleteOne()
				- 删除集合中的一个文档
			- db.collection.deleteMany()
				- 删除集合中的多个文档
			- 清空一个集合
				db.collection.remove({})
			- 删除一个集合
				db.collection.drop()
			- 删除一个数据库
				db.dropDatabase()



db.<collection>.insert(doc) - 向数据库中插入文档

db.<collection>.find()      - 查询当前集合中的所有的文档

objectId()                  - 生成id,随着时间生成(id是确保信息唯一性)可以自己指定,但是也必须确保唯一性;

###mongodb--IDE(mongodbmanagerfree_inst)
F6 执行光标所在行的代表
F9 执行选中多行

##mongoose
	/*
  1. 引入mongoose模块
  2. 连接本地mongoDB数据库
  3. 创建Schema模式对象
  4. 创建Model模型对象
  5. 创建Document文档对象
  6. 保存数据
 */
 
 /*
      模型对象的CRUD
      C - create
        Model.create(文档对象, 回调函数)  返回值为undefined
        Model.create(文档对象)  返回值为promise
      R - read
        Model.find(查询条件[, 投影], 回调函数)
        Model.find(查询条件[, 投影])
        Model.findOne(查询条件[, 投影])
        
        操作符：
          1. < <= > >= !==  $lt $lte $gt $gte $ne
          2. 与或 $or $in 非 $nin
        
      U - update
        Model.updateOne(查询条件, 更新的内容[, 配置对象])
        Model.updateMany(查询条件, 更新的内容[, 配置对象])
      D - delete
        Model.deleteOne(查询条件)
        Model.deleteMany(查询条件)
     */
	 
	 由于CRUD的返回值是Promise封装函数
	 
	 所以利用async await函数  等到想要的返回值