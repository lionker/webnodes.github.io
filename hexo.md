### 第一步安装hexo

$ npm install -g hexo-cli   


### 第二步克隆hexo_github的库

$ hexo init hexo_text

注: hexo_text是自命名clone库根文件夹

### 第三部生成静态文件

$ hexo Generate	

### 第三步启动hexo本地服务器
	
$ hexo s 

通过localhost可查看

### 第四步生成新文章及标题(markdown格式)

$ hexo new "post title";

### 运行生成静态文件(网页) 

$ hexo g(Generate)

### 生成草稿(不会被渲染,和生成静态文章)

$ hexo new draf "draf title";

### 发布草稿

$ hexo public draf "draf title";

### 生成纯页面

$ hexo new page "page title";

### 配置deploy(上传库)

$ hexo deploy

#### 安装deploy(git的插件)

$ npm hexo-deployer-git --save

#### 改变config.yml配置文件

type : git
repo : github仓库SSH值


#### 提交部署

$hexo d($ hexo deploy)

#### 错误处理
```
#### windows若报错,重新设置github配置文件

$ git config --global credential.helper wincred

### _config.yml重要配置

	###修改_config配置文件,修改url路径,和root路径(修复线上的引用路径的错误,js无法加载,css无法加载,图片无法加载)
	# URL
	## If your site is put in a subdirectory, set url as 'http://yoursite.com/child' and root as '/child/'
	url: https://huang56.github.io/hexo_text/ (your_https)
	root: /hexo_text (repo_name)

```


### 迁移其他网站内容

$ hexo migrate


###部署
hexo clean：清除public，当 source文件夹中的部分资源更改过之后，特别是对文件进行了删除或者路径的改变之后，需要执行这个命令，然后重新编译。
hexo generate (hexo g)： 编译，一般部署上去的时候都需要编译一下，编译后，会出现一个 public 文件夹，将所有的md文件编译成html文件 开启本地服务，
hexo server (hexo s) 启动本地web服务，用于博客的预览
hexo deploy (hexo d) 部署播客到远端（比如github, heroku等平台）：部署博客到github上，如果一切顺利，你就通过访问usename.github.io访问你的博客了！
--------------------- 
装饰你的个人博客
至此，已经完成了github pages+hexo搭建博客的步骤，现在需要装饰你的博客 

###切换主题
1. Hexo 主题配置 
就和当时我们用的qq空间一样，我们可以直接用写好的主题，然后我们就只需要写文章就好 
这里以主题NexT为例进行说明。 

2. 安装主题 $ hexo clean (在theme文件夹下Git bash)
$ git clone https://github.com/iissnan/hexo-theme-next

3. 启用主题

修改Hexo目录下的_config.yml配置文件中的theme属性，将其设置为next。 
4. 更新主题 
$ cd themes/next 
$ git pull 
$ hexo g # 生成 
$ hexo s # 启动本地web服务器 



# [hexo个性化配置](https://blog.csdn.net/kunkun5love/article/details/79130956)

# [5分钟带你读懂Hexo源码设计模式](https://www.jianshu.com/p/ef88b5bbb914)

# [bat批处理可定时提交hexo](https://www.jianshu.com/p/b19173aae49a)