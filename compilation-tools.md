##babel 
将ES6 ==>ES5
###@babel/Plugins 插件
.babelrc文件配置方法：（插件是由前向后执行）
{
  "plugins": [
    "@babel/plugin-transform-object-assign",
    "@babel/plugin-transform-runtime"
  ]
}

###@babel/preset预设
@babel/preset-env  预设  处理ES6语法为ES5
####预设配置 
.babelrc文件的配置： （预设的执行由后向前，满足版本的兼容）
	one：
			{
                  "presets": ["@babel/preset-env"]
                } 
			---> package.json 这里配置到根目录json中方便其他工具调用
                "browserslist": [
                    "last 2 Chrome versions"
                 ] 
	two：
			{
			  "presets": [
				["@babel/preset-env", {
				  "targets": {
					"browsers": ["last 1 Chrome versions"]
				  }
				}]
			  ]
			}
###@babel-polyfill衬垫
处理兼容API	


####需要在预设处理后的代码中引入
	require（'@babel/polyfill'）
	
	
##browserify
	编译common.js语法的工具
###配置pakage.json执行脚本
	
##webpack 	
	编译common.js 的语法
###配置pakage.json执行脚本