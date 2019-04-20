
<!-- TOC -->autoauto- [连接github远程库的两种步骤](#连接github远程库的两种步骤)auto    - [一、clone的方式](#一clone的方式)auto    - [二、本地库git remote add origin http/ssh的方式](#二本地库git-remote-add-origin-httpssh的方式)auto- [vim编辑器](#vim编辑器)auto- [终端在复制终端外代码时,回因编码不同而导致命令错误](#终端在复制终端外代码时回因编码不同而导致命令错误)auto- [linux命令](#linux命令)auto- [git底层命令](#git底层命令)auto- [git高级命令](#git高级命令)auto    - [基本命令](#基本命令)auto    - [提交](#提交)auto    - [临时存储](#临时存储)auto    - [查看提交](#查看提交)auto    - [git 撤销](#git-撤销)auto    - [git 上传](#git-上传)auto    - [git 分支](#git-分支)auto    - [git 标签](#git-标签)auto    - [git 指针(回退版本)](#git-指针回退版本)auto    - [git 远程](#git-远程)auto- [git 储存](#git-储存)auto- [git 放弃本地修改](#git-放弃本地修改)auto- [删除 一些 没有 git add 的 文件；](#删除-一些-没有-git-add-的-文件)auto- [git忽略上传远程设置 .gitgnore文件](#git忽略上传远程设置-gitgnore文件)autoauto<!-- /TOC -->
## 连接github远程库的两种步骤
### 一、clone的方式

1 : 在某文件夹直接 git clone http/ssh
			仓库初始化,并且建立主分支跟踪
2 : 进人index层文件夹 cd xxx
				
3 : 将需要上传的文件复制进入(新文件)

4 :  全部上传  git add . (git add all)
			提交工作区的内容到暂存区
5 :  提交 git commit -m blog
			提交工作区的内容到本地库
6 :  提交到主分支 git pull origin master 
			提交主机远程库之前检查合并
7 : 提交到主分支 git push origin master  
			提交到对应主机分支
			
### 二、本地库git remote add origin http/ssh的方式

1 : 初始化本地库 git init 
				创建库隐藏文件夹(.git)
2 : git remote add origin http/ssh

2.1: git fetch origin dev:dev 创建跟踪分支(主分支clone时自动跟踪)
				远程有分支,本地没有
3 : 将需要上传的文件复制进入(工作区)
			
4 :  全部上传  git add . (git add all)
			提交工作区的内容到暂存区
5 :  提交 git commit -m blog
			提交工作区的内容到本地库
6 :  提交到主分支 git pull origin master (远程库没有(包括主)分支时,没有文件,可跳过) 
			提交主机远程库之前检查合并
7 : 提交到主分支 git push origin master  
			提交到对应主机,远程库没有对应分支会建立对应分支	

## vim编辑器
	:w filename  命令文件
	:wq 保存退出
	i 插入
## 终端在复制终端外代码时,回因编码不同而导致命令错误
## linux命令

  where  程序名称    可找到程序启动的位置(即程序所在位置)
	echo 控制台打印 (相当于console.log)
	find 文件夹    平铺查看文件夹下信息,能展示后代(比dir强大)
	find 文件夹 -type f 直线   平铺查看文件夹下信息,只展示文件
	ll: 列出对应目录下的所有子目录信息(比dir强大) 
	dir: 列出所有子目录名字
	cat 文件url 获取文件的内容
	mv newName oldName 重命名文件;
	stat 文件 查看文件创建时间  
## git底层命令
    echo "text content" | git hash object -w --stdin
	
	git 
	git hash object -w 文件路径  往git库储存数据(hash键值对的形式)
	git hash object 文件路径   读取文件的hash值
	git cat-file -t   显示对象的类型
	git cat-file -p hash值   格式化的查看,根据对象的类型，以优雅的方式显式对象内容。
## git高级命令

### 基本命令
	clear 清屏    (linux命令)
	git init  初始化本地仓库
	git diff  查看为暂存已跟踪文件当前操作更新与未更新的内容
	git	diff --staged  查看已缓存为提交的内容  (dit diff --cached);
	git rm filename 删除文件 (不会新增git对象,会生成tree,commit);
	git config -e 修改用户配置文件
	git rebase -i "hashcode" 编辑commit库,可能会程讯依赖错误导致报错

###	提交 
	git add . ：他会监控工作区的状态树，使用它会把工作时的所有变化提交到暂存区，包括文件内容修改(modified)以及新文件(new)，但不包括被删除的文件。	
	git add -u ：他仅监控已经被add的文件（即tracked file），他会将被修改的文件提交到暂存区。add -u 不会提交新文件（untracked file）。（git add --update的缩写）
	git add -A ：是上面两个功能的合集（git add --all的缩写）
	git commit -m ""  由暂存区提交至本地库,会生成tree,commit的hashcode;
	git commit -am ""  已跟踪过的文件直接提交
	git commit -a -m "" 已跟踪过的文件直接提交
### 临时存储
	git stash  临时提交虚拟库
	git stash list    查看临时库文件
	git stash apply		返回文件到本地
### 查看提交
	git show hashcode  查看blob对象的内容 (提交修改具体的内容) 
	git show hashcode --stat  提交修改简要的内容
	git log --oneline 查看几次提交(不显示撤销) ===git log --pretty=oneline
	git log --pretty   查看有效提交的 作者 日期 commit
	git reflog 查看所有提交(包括重置提交前(commit)
	git log --oneline --decorate 	查看当前分支所指对象
	git log --oneline --decorate --graph      --graph选项绘制一个ASCII图像来展示当前分支提交历史的分支结构
	git log --oneline --decorate --graph --all 	查看项目所有分叉历史
	git log --no-merges  查看未提交
	git log --merges 查看 合并
	git is-files -s 查看提交tree的内容(查看暂存区当前的样子)
	git reflog show --date=iso master 查看master分支每次提交时间
### git 撤销
	git checkout filename  工作目录放弃单个文件的修改,未加暂存区 (不可逆)
	git checkout . 放弃当前目录下的修改  (不可逆)
	
	git reset HEAD 如果后面什么都不跟的话 就是上一次add 里面的全部撤销了(将暂存区撤回工作区) 
	git reset HEAD XXX/XXX/XXX.java 就是对某个文件进行撤销了
	git checkout commit -- filename 可撤回暂存区和工作目录
	git commit --amend -m "xxx" 覆盖之前操作的m (会生成新的tree)
### git 上传
	git push origin  上面命令表示，将当前分支推送到origin主机的对应分支
	git push -u origin master  将本地的master分支推送到origin主机，同时指定origin为默认主机，后面就可以不加任何参数使用git push了
	git push origin 本地分支名/远程分支名 若远程分支没有该远程分支,则会在github中新建
### git 分支
	git pull mayu master --allow-unrelated-histories 第一次push前先pull合并
	git checkout 分支名 切换分支    
	git branch 分支名  创建分支(在当前head处创建分支)
	git branch -f newBr  新建分支并覆盖同名分支
	git checkout -b dev  hashcode //相当于以上两条命令：在hashcode创建 dev 分支并切换至hashcode处的dev分支
	git checkout -B newBr2    新建分支并覆盖同名分支,并切换分支
	git branch -d <name> 删除分支
	git merge <name> 合并某分支到当前分支
	git branch -a  查看所有分支,包括远程
	git fetch origin dev:dev 创建跟踪分支(主分支clone时自动跟踪)
	git branch -vv 查看跟踪分支
	git branch -r  查看远程版本库分支列表
	git branch -m oldName newName 给分支重命名
	git push origin --delete brh 删除远程分支

	git branch name hash值  在某个hash上创建分支 
	git branch --merged 查看已合并分支
### git 标签  
	git tag tagContent hashcode  给hashcode打上标签tagContent
	git tag annotatedTag e577355 -a -m "蚂蚁部落" 给某个commit打上有批注的标签
	git tag -d tagLearn 删除本地标签
	git push origin --delete tagLearn 删除远程分支标签
### git 指针(回退版本)
	git reset --hard eb9b70c  回退到指定版本,改变内容  
    git reset --soft HEAD~	分支和指针回到上一次提交(只回退指针,不改变内容)  但不重置已提交的
### git 远程
	git branch --set-upstream-to=origin/<branch>  当前分支跟踪origin主机的某分支
	git push -f origin 强行推送更新远程库
	git pull origin master --allow-unrelated-histories 强行拉取合并
	git remote add origin https/ssh 建立远程库连接
	git remote remove <name>  删除远程库连接
	git remote set-url origin <newurl> 重新设置远程库连接(也可以直接修改config文件)
	git remote show origin 查看remote地址，远程分支，还有本地分支与之相对应关系等信息
## git 储存
	git stash 
	git stash apply --index
	git stash list
	git stash branch testchanges
## git 放弃本地修改	
	git fetch --all 只是下载b远程仓库的内容,不做任何的合并
	git reset HEAD hash      指向刚刚下载的最新版本   

## 删除 一些 没有 git add 的 文件；
	git clean -n   显示 将要 删除的 文件 和  目录
	git clean -f   删除 文件，
	git clean -df  删除 文件 和 目录   

## git忽略上传远程设置 .gitgnore文件
	
	git config --global core.excludesfile ~/.gitignore
	
	※ 忽略文件必须在新加文件之前配置好,不然不生效
	※ 配置好忽略文件之后,将以前将要忽略的文件删掉重新添加
一、 .gitignore忽略规则的优先级:	

在 .gitingore 文件中，每一行指定一个忽略规则，Git检查忽略规则的时候有多个来源，它的优先级如下（由高到低）：  
1. 从命令行中读取可用的忽略规则   
2. 当前目录定义的规则   
3. 父级目录定义的规则，依次递推  
4. $GIT_DIR/info/exclude 文件中定义的规则   
5. core.excludesfile中定义的全局规则

二、 .gitignore忽略规则简单说明	

在 .gitingore 文件中，每一行指定一个忽略规则，Git检查忽略规则的时候有多个来源，它的优先级如下（由高到低）：  

```
#               表示此为注释,将被Git忽略
*.a             表示忽略所有 .a 结尾的文件
!lib.a          表示但lib.a除外
/TODO           表示仅仅忽略项目根目录下的 TODO 文件，不包括 subdir/TODO
build/          表示忽略 build/目录下的所有文件，过滤整个build文件夹；
doc/*.txt       表示会忽略doc/notes.txt但不包括 doc/server/arch.txt
 
bin/:           表示忽略当前路径下的bin文件夹，该文件夹下的所有内容都会被忽略，不忽略 bin 文件
/bin:           表示忽略根目录下的bin文件
/*.c:           表示忽略cat.c，不忽略 build/cat.c
debug/*.obj:    表示忽略debug/io.obj，不忽略 debug/common/io.obj和tools/debug/io.obj
**/foo:         表示忽略/foo,a/foo,a/b/foo等
a/**/b:         表示忽略a/b, a/x/b,a/x/y/b等
!/bin/run.sh    表示不忽略bin目录下的run.sh文件
*.log:          表示忽略所有 .log 文件
config.php:     表示忽略当前路径的 config.php 文件
 
/mtk/           表示过滤整个文件夹
*.zip           表示过滤所有.zip文件
/mtk/do.c       表示过滤某个具体文件
 
被过滤掉的文件就不会出现在git仓库中（gitlab或github）了，当然本地库中还有，只是push的时候不会上传。
 
需要注意的是，gitignore还可以指定要将哪些文件添加到版本管理中，如下：
!*.zip
!/mtk/one.txt
 
唯一的区别就是规则开头多了一个感叹号，Git会将满足这类规则的文件添加到版本管理中。为什么要有两种规则呢？
想象一个场景：假如我们只需要管理/mtk/目录中的one.txt文件，这个目录中的其他文件都不需要管理，那么.gitignore规则应写为：：
/mtk/*
!/mtk/one.txt
 
假设我们只有过滤规则，而没有添加规则，那么我们就需要把/mtk/目录下除了one.txt以外的所有文件都写出来！
注意上面的/mtk/*不能写为/mtk/，否则父目录被前面的规则排除掉了，one.txt文件虽然加了!过滤规则，也不会生效！
 
----------------------------------------------------------------------------------
还有一些规则如下：
fd1/*
说明：忽略目录 fd1 下的全部内容；注意，不管是根目录下的 /fd1/ 目录，还是某个子目录 /child/fd1/ 目录，都会被忽略；
 
/fd1/*
说明：忽略根目录下的 /fd1/ 目录的全部内容；
 
/*
!.gitignore
!/fw/ 
/fw/*
!/fw/bin/
!/fw/sf/
说明：忽略全部内容，但是不忽略 .gitignore 文件、根目录下的 /fw/bin/ 和 /fw/sf/ 目录；注意要先对bin/的父目录使用!规则，使其不被排除。
```
					