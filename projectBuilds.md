## 1、Gulp介绍
* 中文主页: http://www.gulpjs.com.cn/
* gulp是与grunt功能类似的**前端项目构建**工具, 也是基于Nodejs的自动**任务运行器**
* 能自动化地完成 javascript/coffee/sass/less/html/image/css 等文件的
  合并、压缩、检查、监听文件变化、浏览器自动刷新、测试等任务
* gulp更高效(异步多任务), 更易于使用, 插件高质量

## 2、重要API介绍
* gulp.src(filePath/pathArr) 
  * 用于读取文件
* gulp.dest(dirPath/pathArr)
  * 用于向文件夹中输出文件
* gulp.task(name, [deps], fn) 
  * 定义一个任务
* gulp.watch() 
  * 监视文件的变化

## 3、创建一个简单的应用gulp_test
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

## 4、js文件语法检查 gulp-eslint
* 准备工作：创建js文件
  * src/js/module1.js
  * src/js/module2.js
  * src/js/module3.js
  * src/js/main.js
* 下载插件:
  * npm install gulp-eslint --save-dev
* 配置编码
  ```
  const gulp = require('gulp');
  const eslint = require('gulp-eslint');
  
  gulp.task('eslint',() => {
    return gulp.src(['./src/js/*.js'])
      .pipe(eslint())
      .pipe(eslint.format())
  })
  ```
* 在package.json中配置eslint的检查项
  ```
  "eslintConfig": {
    "parserOptions": {
      "ecmaVersion": 7,
      "sourceType": "module",
      "ecmaFeatures": {
        "module": true
      }
    }
  }
  ```
* 运行指令: `gulp eslint`

## 5、js语法转换 gulp-babel @babel/core @babel/preset-env
* 下载插件:
  * npm install --save-dev gulp-babel @babel/core @babel/preset-env
* 配置编码
  ```
  const babel = require('gulp-babel');
  
  gulp.task('babel', () => {
    return gulp.src('src/js/*.js')
      .pipe(babel({
        presets: ['@babel/env']
      }))
      .pipe(gulp.dest('build/js'))
  });
  ```
* 运行指令: `gulp babel`

## 6、将commonjs模块化转换浏览器能识别的语法 gulp-browserify
* 下载插件:
  * npm install --save-dev gulp-browserify
* 配置编码
  ```
  const browserify = require('gulp-browserify');
  
  gulp.task('browserify', () => {
    return gulp.src('build/js/main.js')
      .pipe(browserify())
      .pipe(rename('built.js'))
      .pipe(gulp.dest('build/js'))
  });
  ```
* 运行指令: `gulp browserify`

## 7、注册默认任务
* gulp.task('default', gulp.series('eslint', 'babel', 'browserify'));  //顺序执行
* gulp.task('default', gulp.parallel('eslint', 'babel', 'browserify'));  //并行执行
* 运行指令: `gulp`

## 8、处理less文件 gulp-less
* 准备工作：创建less文件
  * src/less/test1.less
  * src/less/test2.less
* 下载插件:
	* npm install gulp-less --save-dev 
* 配置编码
  ```
  const less = require('gulp-less');
  
  gulp.task('less', () => {
    return gulp.src('./src/less/*.less')
      .pipe(less())
      .pipe(gulp.dest('./build/css'));
  });
  
  gulp.task('js-dev', gulp.series('eslint', 'babel', 'browserify'));  //顺序执行
  gulp.task('build', gulp.parallel('js-dev', 'less'));  //并行执行
  ```
* 运行指令: `gulp build` 

## 9、自动编译代码 gulp-livereload
* 下载插件
  * npm install gulp-livereload --save-dev
* 配置编码:
  ```
  const livereload = require('gulp-livereload');
            
  //所有的任务最后加上
  .pipe(livereload());
  
  gulp.task('watch', function() {
    livereload.listen();
    
    gulp.watch('src/less/*.less', gulp.series('less'));
    gulp.watch('src/js/*.js', gulp.series('js'));
  });
  
  gulp.task('start', gulp.series('build', 'watch'));
  ```
* 运行指令: `gulp start`

## 10、自动打开/更新页面（热更新）gulp-connect open
* 下载插件
  * npm install gulp-connect open --save-dev
* 配置编码
  ```
  //在gulp.watch中配置服务器的选项
  connect.server({
      root : 'dist/', //提供服务的根路径
      livereload : true, //是否实时刷新
      port : 5000 //开启端口号
   });
  // 自动开启链接
  open('http://localhost:5000');
  ```
* 运行指令: `gulp start`  

> 以上就是gulp开发环境的配置，可以在内存中自动打包文件并有自动编译运行、热更新等功能。
  
## 11、压缩JS gulp-uglify
* 下载插件:
	* npm install --save-dev gulp-uglify
* 配置编码
	```
	const uglify = require('gulp-uglify');
	const rename = require('gulp-rename');
	
	gulp.task('uglify', function() {
	  return gulp.src('./build/js/built.js')
	    .pipe(uglify())
	    .pipe(rename('dist.min.js'))
	    .pipe(gulp.dest('./dist/js/'))
	});
	
	gulp.task('js-prod', gulp.series('js-dev', 'uglify'));  //顺序执行
	```
* 运行指令: `gulp js-prod`

## 12、压缩css gulp-clean-css less-plugin-autoprefix
* 下载插件
	* npm install gulp-clean-css less-plugin-autoprefix --save-dev 
* 配置编码
	```
	gulp.task('css', function () {
	  return gulp.src('./src/less/*.less')
	    .pipe(less({
	      plugins: [autoprefix] //自动扩展样式的兼容性前缀
	    }))  //将less文件转换成css文件
	    .pipe(concat('dist.min.css'))  //合并css文件
	    .pipe(cleanCSS({compatibility: 'ie8'}))  //压缩css文件
	    .pipe(gulp.dest('./dist/css'))
	});
	```
* 运行指令: `gulp css`	
	
## 13、压缩html gulp-htmlmin
* 下载插件:
  * npm install gulp-htmlmin --save-dev
* 配置编码
  ```
  var htmlmin = require('gulp-htmlmin');
  //压缩html任务
  gulp.task('html', function() {
    return gulp.src('index.html')
      .pipe(htmlmin({collapseWhitespace: true, removeComments: true}))
      .pipe(gulp.dest('dist'))
  });
  
  gulp.task('prod', gulp.parallel('js-prod', 'css', 'html')); //并行执行
  ```
* 修改页面引入
  ```
  <link rel="stylesheet" href="css/dist.min.css">
  <script type="text/javascript" src="js/dist.min.js"></script>
  ```
* 运行指令: `gulp prod`

> 以上就是gulp生产环境的配置，可以生成打包后的文件。

## webpack快速入门教程
### 1、了解Webpack相关
* 什么是webpack
  * Webpack是一个模块打包器(bundler)。
  * 在Webpack看来, 前端的所有资源文件(js/json/css/img/less/...)都会作为模块处理
  * 它将根据模块的依赖关系进行静态分析，生成对应的静态资源
* 五个核心概念
  * Entry：入口起点(entry point)指示 webpack 应该使用哪个模块，来作为构建其内部依赖图的开始。
  * Output：output 属性告诉 webpack 在哪里输出它所创建的 bundles，以及如何命名这些文件，默认值为 ./dist。
  * Loader：loader 让 webpack 能够去处理那些非 JavaScript 文件（webpack 自身只能解析 JavaScript）。
  * Plugins：插件则可以用于执行范围更广的任务。插件的范围包括，从打包优化和压缩，一直到重新定义环境中的变量等。
  * Mode：模式，有生产模式production和开发模式development
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
	
### 2、开启项目
* 初始化项目：
  * 生成package.json文件
      ```   
      {
        "name": "webpack_test",
        "version": "1.0.0"
      } 
      ```
* 安装webpack
  * npm install webpack webpack-cli -g  //全局安装
  * npm install webpack webpack-cli -D //本地安装
    
### 3、编译打包应用
* 创建js文件
  * src/js/app.js
  * src/js/module1.js
  * src/js/module2.js
  * src/js/module3.js
* 创建json文件
  * src/json/data.json  
* 创建主页面: 
  * src/index.html
* 运行指令
  * 开发配置指令：webpack src/js/app.js -o dist/js/app.js --mode=development
    * 功能: webpack能够编译打包js和json文件，并且能将es6的模块化语法转换成浏览器能识别的语法
  * 生产配置指令：webpack src/js/app.js -o dist/js/app.js --mode=production
    * 功能: 在开发配置功能上加上一个压缩代码
* 结论：
  * webpack能够编译打包js和json文件
  * 能将es6的模块化语法转换成浏览器能识别的语法
  * 能压缩代码
* 缺点：
  * 不能编译打包css、img等文件
  * 不能将js的es6基本语法转化为es5以下语法
* 改善：使用webpack配置文件解决，自定义功能

### 4、使用webpack配置文件
* 目的：在项目根目录定义配置文件，通过自定义配置文件，还原以上功能
* 文件名称：webpack.config.js
* 文件内容：
    ```
    const {resolve} = require('path'); //node内置核心模块，用来设置路径。
    module.exports = {
      entry: './src/js/app.js',   // 入口文件
      output: {                     // 输出配置
        filename: './js/bundle.js',      // 输出文件名
        path: resolve(__dirname, 'dist')   //输出文件路径配置
      },
      mode: 'development'   //开发环境(二选一)
      mode: 'production'   //生产环境(二选一)
    };
    ```
* 运行指令： webpack

### 5、js语法检查 eslint-loader eslint
* 安装loader
  * npm install eslint-loader eslint --save-dev
* 配置loader
    ```
    module: {
      rules: [
        {
          test: /\.js$/,  //只检测js文件
          exclude: /node_modules/,  //排除node_modules文件夹
          enforce: "pre",  //提前加载使用
          use: { //使用eslint-loader解析
            loader: "eslint-loader" 
          }
        }        
      ]
    }
    ```
* 修改package.json（需要删除注释才能生效）
    ```
    "eslintConfig": {   //eslint配置
      "parserOptions": {  
        "ecmaVersion": 8,  // es8
        "sourceType": "module", //  ECMAScript 模块
      }
    }
    ```
* 运行指令：webpack

### 6、js语法转换 babel-loader @babel/core @babel/preset-env
* 安装loader
  * npm install babel-loader @babel/core @babel/preset-env --save-dev
* 配置loader
    ```
    module: {
      rules: [
        {
          oneOf: [  //数组中的配置只有一个能够生效, 后面的配置都会放在当前数组中
            {
              test: /\.js$/,
              exclude: /node_modules/,
              use: {
                loader: "babel-loader",
                options: {
                  presets: ['@babel/preset-env']
                }
              }
            }
          ]
        }
      ]
    }
    ```
* 运行指令：webpack

### 7、打包less资源  css-loader style-loader less-loader less
* 创建less文件
  * src/less/test1.less
  * src/less/test2.less
* 入口app.js文件
  * 引入less资源  
* 安装loader
  * npm install css-loader style-loader less-loader less --save-dev 
* 配置loader
    ```
    oneOf: [
      {
        test: /\.less$/,
        use: [{
          loader: "style-loader"
        }, {
          loader: "css-loader" 
        }, {
          loader: "less-loader" 
        }]
      }
    ]
    ```
* 运行指令：webpack
* 在index.html中引入打包生成的dist/js/bundle.js文件,观察效果

### 8、打包样式文件中的图片资源 file-loader url-loader --save-dev
* 添加2张图片:
   * 小图, 小于8kb: src/images/1.png
   * 大图, 大于8kb: src/images/2.jpg
* 在less文件中通过背景图的方式引入图片
* 安装loader
  * npm install file-loader url-loader --save-dev 
  * 补充：url-loader是对象file-loader的上层封装，使用时需配合file-loader使用。
* 配置loader
    ```
    {
      test: /\.(png|jpg|gif|svg)$/,
      use: [
        {
          loader: 'url-loader',
          options: {
            outputPath: 'images/',   //在output基础上，修改输出图片文件的位置
            publicPath: '../dist/images/',  //修改背景图引入url的路径
            limit: 8 * 1024,  // 8kb大小以下的图片文件都用base64处理
            name: '[hash:8].[ext]'  // hash值为7位，ext自动补全文件扩展名
          }
        }
      ]
    }
    ```

* 运行指令：webpack
* 在index.html中引入打包生成的dist/js/bundle.js文件,观察效果

### 9、打包html文件 clean-webpack-plugin
* 添加html文件
  * src/index.html
  * 注意不要在html中引入任何css和js文件
* 安装插件Plugins
	* npm install clean-webpack-plugin --save-dev 
* 在webpack.config.js中引入插件（插件都需要手动引入，而loader会自动加载）
	* const CleanWebpackPlugin = require('clean-webpack-plugin')
* 配置插件Plugins
    ```
    plugins: [
      new HtmlWebpackPlugin({
        template: './src/index.html'
      }),
    ]
    ```
* 运行指令：webpack

### 10、打包html中图片资源 html-loader
* 添加图片
  * 在src/index.html添加两个img标签
* 安装loader
	* npm install html-loader --save-dev 
* 修改entry
  * entry: ['./src/js/app.js', './src/index.html']
* 配置loader
    ```
    {
      test: /\.(html)$/,
      use: {
        loader: 'html-loader'
      }
    }
    ```
* 运行指令：webpack

### 11、打包其他资源
* 添加字体文件
  * src/media/iconfont.eot
  * src/media/iconfont.svg
  * src/media/iconfont.ttf
  * src/media/iconfont.woff
  * src/media/iconfont.woff2
* 修改样式
    ```
    @font-face {
      font-family: 'iconfont';
      src: url('../media/iconfont.eot');
      src: url('../media/iconfont.eot?#iefix') format('embedded-opentype'),
      url('../media/iconfont.woff2') format('woff2'),
      url('../media/iconfont.woff') format('woff'),
      url('../media/iconfont.ttf') format('truetype'),
      url('../media/iconfont.svg#iconfont') format('svg');
    }
    
    .iconfont {
      font-family: "iconfont" !important;
      font-size: 16px;
      font-style: normal;
      -webkit-font-smoothing: antialiased;
      -moz-osx-font-smoothing: grayscale;
    }
    ```
* 修改html，添加字体
* 配置loader
    ```
    {
      loader: 'file-loader',
      exclude: [/\.js$/, /\.html$/, /\.json$/],
      options: {
        outputPath: 'media/',
        publicPath: '../dist/media/',
        name: '[hash:8].[ext]',
      },
    }
    ```
* 运行指令：webpack

### 12、自动编译打包运行 webpack-dev-serverwebpack-dev-server
* 安装loader
	* npm install webpack-dev-server --save-dev 
* 引入webpack
  * const webpack = require('webpack');
* 修改webpack配置对象（注意不是loader中）
    ```
    devtool: 'inline-source-map',  // 将编译后的代码映射回原始源代码，更容易地追踪错误和警告
    devServer: {
      contentBase: './dist',  //项目根路径
      hot: true,  //开启热模替换功能
      open: true  //自动打开浏览器
    },
    plugins: [
      new webpack.NamedModulesPlugin(),
      new webpack.HotModuleReplacementPlugin()
    ]
    ```
* 修改loader部分配置
  * 因为构建工具以dist为根目录，不用再找dist了
  * `publicPath: '../dist/images/'` --> `publicPath: 'images/'`
  * `publicPath: '../dist/media/'` --> `publicPath: 'media/'`
* 修改package.json中scripts指令
  * "start": "webpack-dev-server",
  * "dev": "webpack-dev-server"
* 运行指令：npm start / npm run dev

> 以上就是webpack开发环境的配置，可以在内存中自动打包所有类型文件并有自动编译运行、热更新等功能。

### 13、准备生产环境
* 创建文件夹config，将webpack.config.js复制两份
  * webpack.dev.js
  * webpack.prod.js
* 修改webpack.prod.js配置，删除webpack-dev-server配置
  ```
  module.exports = {
    output: {
      filename: 'js/[name].[hash:8].js',   //添加了hash值, 实现静态资源的长期缓存
      publicPath: '/'  //所有输出资源公共路径
    },
    module: {  //loader其他没有变化，只放了变化部分，只有需要修改路径部分改了
      rules: [
        {
          oneOf: [
            {
              test: /\.(png|jpg|gif|svg)$/,
              use: [
                {
                  loader: 'url-loader',
                  options: {
                    limit: 8 * 1024,  // 8kb大小以下的图片文件都用base64处理
                    name: 'images/[name].[hash:8].[ext]'
                  }
                }
              ]
            },
            {
              loader: 'file-loader',
              exclude: [/\.js$/, /\.html$/, /\.json$/],
              options: {
                name: 'media/[name].[hash:8].[ext]',
              },
            }
          ]
        }
      ]
    },
    mode: 'production',  //修改为生产环境
  }
  ```
* 修改package.json的指令
  * "start": "webpack-dev-server --config ./config/webpack.dev.js"
  * "dev": "webpack-dev-server --config ./config/webpack.dev.js"
  * "build": "webpack --config ./config/webpack.prod.js"
* 开发环境指令
  * npm start
  * npm run dev
* 生产环境指令
  * npm run build
  * 注意: 生产环境代码需要部署到服务器上才能运行
    * npm i serve -g  
    * serve -s dist
  
### 14、清除打包文件目录 clean-webpack-plugin
* 安装插件
	* npm install clean-webpack-plugin --save-dev
* 引入插件
  * const CleanWebpackPlugin = require('clean-webpack-plugin');
* 配置插件
  ```
  new CleanWebpackPlugin()
  ```
* 运行指令：npm run build

### 15、提取css成单独文件 mini-css-extract-plugin
* 安装插件
	* npm install mini-css-extract-plugin --save-dev 
* 引入插件
  * const MiniCssExtractPlugin = require("mini-css-extract-plugin");	
* 配置loader
  ```
  {
    test: /\.less$/,
    use: [
      MiniCssExtractPlugin.loader,
      'css-loader',
      'less-loader',
    ]
  }
  ```
* 配置插件
  ```
  new MiniCssExtractPlugin({
    filename: "css/[name].[hash:8].css",
    chunkFilename: "css/[id].[hash:8].css"
  })
  ```    
* 运行指令
  * npm run build
  * serve -s dist

### 16、添加css兼容  postcss-loader autoprefixer
* 安装loader
	* npm install postcss-loader autoprefixer --save-dev 
* 配置loader
  ```
  {
    test: /\.less$/,
    use: [
      MiniCssExtractPlugin.loader,
      'css-loader',
      'postcss-loader',
      'less-loader',
    ]
  }
  ```
* 在项目根目录添加postcss配置文件：postcss.config.js
  ```
  module.exports = {
    "plugins": {
      "autoprefixer": {
        "browsers": [
          "ie >= 8",
          "ff >= 30",
          "chrome >= 34",
          "safari >= 8",
          "opera >= 23"
        ]
      }
    }
  }
  ```
* 运行指令：
  * npm run build
  * serve -s dist

### 17、压缩css optimize-css-assets-webpack-plugin
* 安装插件
	* npm install optimize-css-assets-webpack-plugin --save-dev 
* 引入插件
  * const OptimizeCssAssetsPlugin = require('optimize-css-assets-webpack-plugin');	
* 配置插件
  ```
  new OptimizeCssAssetsPlugin({
    cssProcessorPluginOptions: {
      preset: ['default', { discardComments: { removeAll: true } }],
    },
  })
  ```
* 运行指令：
  * npm run build
  * serve -s dist
 
### 18、图片压缩  img-loader imagemin-gifsicle imagemin-mozjpeg imagemin-pngquant imagemin-svgo imagemin
* 安装loader
	* npm install img-loader imagemin-gifsicle imagemin-mozjpeg imagemin-pngquant imagemin-svgo imagemin --save-dev 
* 配置loader
  ```
  {
    test: /\.(png|jpg|gif|svg)$/,
    use: [
      {
        loader: 'url-loader',
        options: {
          limit: 8 * 1024,  // 8kb大小以下的图片文件都用base64处理
          name: 'images/[name].[hash:8].[ext]'
        }
      },
      {
        loader: 'img-loader',
        options: {
          plugins: [
            require('imagemin-gifsicle')({
              interlaced: false
            }),
            require('imagemin-mozjpeg')({
              progressive: true,
              arithmetic: false
            }),
            require('imagemin-pngquant')({
              floyd: 0.5,
              speed: 2
            }),
            require('imagemin-svgo')({
              plugins: [
                { removeTitle: true },
                { convertPathData: false }
              ]
            })
          ]
        }
      }
    ]
  }
  ```
* 运行指令：
  * npm run build
  * serve -s dist  
  
### 19、压缩html
* 修改插件配置
  ```
  new HtmlWebpackPlugin({
    template: './src/index.html',
    minify: {
      removeComments: true,
      collapseWhitespace: true,
      removeRedundantAttributes: true,
      useShortDoctype: true,
      removeEmptyAttributes: true,
      removeStyleLinkTypeAttributes: true,
      keepClosingSlash: true,
      minifyJS: true,
      minifyCSS: true,
      minifyURLs: true,
    }
  })
  ```
* 运行指令：
  * npm run build
  * serve -s dist 
    
> 以上就是webpack生产环境的配置，可以生成打包后的文件。




