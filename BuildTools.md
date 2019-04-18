## BuildTools

### 一、 gulp (4)
1、Gulp介绍
* 中文主页: http://www.gulpjs.com.cn/
* gulp是与grunt功能类似的**前端项目构建**工具, 也是基于Nodejs的自动**任务运行器**
* 能自动化地完成 javascript/coffee/sass/less/html/image/css 等文件的
  合并、压缩、检查、监听文件变化、浏览器自动刷新、测试等任务
* gulp更高效(异步多任务), 更易于使用, 插件高质量

2、重要API介绍
* gulp.src(filePath/pathArr) 
  * 用于读取文件
* gulp.dest(dirPath/pathArr)
  * 用于向文件夹中输出文件
* gulp.task(name, [deps], fn) 
  * 定义一个任务
* gulp.watch() 
  * 监视文件的变化

3、创建一个简单的应用gulp_test
* 项目目录
  ```
  |- dist
  |- build
  |- src
    |- js
    |- less
  |- index.html
  |- gulpfile.js ----- gulp配置文件
  |- package.json
    {
      "name": "gulp_test",
      "version": "1.0.0"
    } 
  ```
* 安装gulp
  * npm install gulp-cli -g 全局安装
  * npm install gulp --save-dev 局部安装
* 配置编码: gulpfile.js
  ```
  //引入gulp模块
  var gulp = require('gulp');
  //定义任务
  gulp.task('任务名', function() {
    // 将你的任务的任务代码放在这
  });
  //定义默认任务
  gulp.task('default', '任务')
  ```
* 构建命令: `gulp`

### 二、 webpack (4)

1. **基本简介**:
* 什么是webpack
		* Webpack是一个模块打包器(bundler)。
		* 在Webpack看来, 前端的所有资源文件(js/json/css/img/less/...)都会作为模块处理
		* 它将根据模块的依赖关系进行静态分析，生成对应的静态资源
* 五个核心概念
  * Entry：入口起点(entrypoint)指示 webpack 应使用哪个模块，来作为构建内部依赖图的开始。
  * Output：output 属性诉 webpack 在哪里输出它创建的 bundles，以及如命名这些文件，默认值为./dist。
  * Loader：loader 让webpack 能够去处理那些非JavaScript 文（webpack 自身只能解析JavaScript）。
  * Plugins：插件则可以用执行范围更广的任务。插件范围包括，从打包优化和缩，一直到重新定义环境中变量等。
  * Mode：模式，有生产模production和开发模development
* 理解Loader
  * Webpack 本身只能加载JS/JSON模块，如果要加载其他类型的文件(模块)，就需要使用对应的loader 进行转换/加载
  * Loader 本身也是运行在 node.js 环境中的 JavaScript 模块
  * 它本身是一个函数，接受源文件作为参数，返回转换的结果
  * loader 一般以 xxx-loader 的方式命名，xxx 代表了这个 loader 要做的转换功能，比如 json-loader。
* 理解Plugins
  * 插件可以完成一些loader不能完成的功能。
  * 插件的使用一般是在 webpack 的配置信息 plugins 选项中指定。
* 配置文件(默认)
  * webpack.config.js : 是一个node模块，返回一个 json 格式的配置信息对象

### 常用插件

1. eslint    js文件语法错误检查
2. babel     js语法转换,将高级语法转向低级兼容性好的和编译JSX
3. marked     
4. md5
5. autoprefixer    自动扩展样式的兼容性前缀
6. imagemin
7. browserify  将commonjs模块化转换浏览器能识别的语法
8. livereload  自动编译代码
9. htmlmin
10. less    将less转译成css     
11. uglify  压缩js
12. open   打开浏览器
13. 