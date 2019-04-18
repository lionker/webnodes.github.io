### 1. npm install express-generator -g [安装应用生成器](http://www.expressjs.com.cn/starter/generator.html),创建骨架
	
### 2. express --view=pug myapp 创建骨架

此命令创建了一个名称为 myapp 的 Express 应用。此应用将在当前目录下的 myapp 目录中创建，并且设置为使用 Pug 模板引擎（view engine）

```
  $ express --view=pug myapp

   create : myapp
   create : myapp/package.json
   create : myapp/app.js
   create : myapp/public
   create : myapp/public/javascripts
   create : myapp/public/images
   create : myapp/routes
   create : myapp/routes/index.js
   create : myapp/routes/users.js
   create : myapp/public/stylesheets
   create : myapp/public/stylesheets/style.css
   create : myapp/views
   create : myapp/views/index.pug
   create : myapp/views/layout.pug
   create : myapp/views/error.pug
   create : myapp/bin
   create : myapp/bin/www
```

### 3. 启动 bin/www文件 流浪器查看localhost:3000

### 4. 创建router. js   并在app.js中引入router.js

1. router中

```
// impor file

const router = require('express').Router();


// site monitor

router.get('/', (req, res, next) => {
    res.send('nihao aaron????')
})

//export file 

module.exports = router;

```

2. app中

```
const router = require('./routes/router')

// monitor route

app.use('/', router);

```	

### 5. 打开流浪求验证	
		
### 6. 静态文件,引入pulic文件夹
	
### 7. 安装socket-io ， 编辑服务器和客服端	