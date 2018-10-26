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



