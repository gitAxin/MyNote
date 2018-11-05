# git

## 一、配置

### 1.1 配置用户信息

- 初始使用时需配置用户信息

~~~bash
$ git config --global user.name 'name'
$ git config --global user.email 'email'
~~~

- git 配置文件.gitconfig

### 1.2 帮助

~~~
$ git help config
~~~

## 二、基本操作

### 2.1 初始化

~~~bash
$ mkdir mysite #创建一个名为mysite的目录
$ cd mysite #进入mysite的目录
$ git init #git 初始化
~~~

### 2.2 nano命令

~~~base
$ nano index.html #编辑或新建index.html
~~~

- Ctrl + O 保存
- Ctrl + X 退出

### 2.3 git add 跟踪

~~~base
$ git add *.html
~~~

### 2.4 git commit 把已经跟踪的文件提交到版本库中

~~~bash
$ git commit -m '注释'
$ git commit -am '注释' #跟踪并提交
~~~

### 2.6 git status 查看当前项目目前的状态

~~~bash
$ git status
~~~

- untracked 没有被跟踪
- unmodified 没有被修改过
- modified 被修改过
- staged 被暂存

## 三、创建分支

~~~bash
$ git branch testing #在当前commit对象上新建一个名称为'testing'的分支
$ git branch #查看显示有几个分支
$ git checkout testing #切换到testing分支出
~~~

- 注：$ git checkout -b testing 相当于执行了上面的第1行和第3行,即创建并切换了分支，如果工作区有正在工作中的内容，git会阻止切换(可储藏中间状态)

## 四、合并分支

~~~bash
$ git merge hotfix #hotfix是分支名字
                  #例如在master分支上合并hotfix分支
~~~

## 五、删除分支

~~~bash
$ git branch -d hotfix #删除hotfix分支
~~~

## 六、解决合并分支中产生的冲突

~~~bash
$ git add index.html #标记已经解决合并冲突
~~~

## 七、git stash 保存当前工作区的状态(中间状态)

~~~bash
$ git stash #保存工作区的状态
$ git stash list #查看状态列表
$ git stash apply stash@{0} #回到未完成工作的状态
~~~

- stash@{0} :可以使用$ git stash list 进行查看

## 八、克隆远程仓库

~~~bash
$ git clone 仓库url
~~~

> 自动创建了master分支,用于跟踪远程仓库的master分支,打开项目文件夹/.git/config文件可以看到master和远程master分支的关联

## 九、注册远程仓库

~~~bash
$ git remote add 远程仓库名(一般用origin) 仓库url
~~~

## 十、推送数据到远程仓库

~~~bash
$ git push -u [远程仓库名(origin)] [本地推送的分支名]
~~~

> -u :表示建立追踪，这样git status 会显示本地分支与远程分支的偏离情况,一般第一次提交数据时加此参数

## 十一、抓取数据

~~~bash
$ git fetch origin
~~~

> 从远程仓库抓取数据，但不会影响本地仓库

~~~bash
$ git pull 
#相当于 $ git fetch, $ git merge
~~~

> 此方式会改变本地仓库

## 十二、查看日志

~~~bash
$ git log --no-merges origin/master
~~~

> 查看在推送之前服务器发生了哪些变化

## 十三、远程仓库的分支合并

~~~bash
$ git merge 远程仓库名/分支名
~~~



