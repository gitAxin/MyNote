视频网址：http://www.iqiyi.com/playlist276124702.html

# 一、linux分区：

## 1.硬盘接口
### 1.1:ide:133m/s    sha、 shb
### 1.2: scaii 200m/s sata 500m/s  sda、sdb
## 2:分区-格式化-分隔设备名称-挂载点
## 3：
## 4：挂载
```
必须分区 
 / 根分区 
 swap（交换分区） 2000
 推荐分区：/boot 启动分区 200
总结 ：
分区：把大硬盘分为小的逻辑分区
格式化 写入文件系统
分区设置文件名：给每个分区定义设备文件名
挂载：给每个分区分配挂载点

复杂性  大小写字母，数字 符号 三种以上
易记记性
时效性3个月 最长180天
```

## 5. root下的目录：

    /root/install.log:存储了安装在系统中的软件包及其版本信息
    /root/install.log.syslog:存储了安装过程中留下的事件记录
    /root/anaconda-ks.cfg 以Kickstart配置文件的格式记录安装中设置的选项信息


## 6. 远程登录管理

    虚拟机网络配置：
    桥接：使用真实的网卡  可以和局域网内同IP段内的其他计算机通信，但是会占用IP
    NAT:通过虚拟网卡vmnet8 只能和本机电脑通信 不会占用IP,如果本机可能访问网络，虚拟机也可以访问互联网
    host_only:通过虚拟网卡vmnet1 只能和本机电脑通信 不会占用IP，只能和本机通信


    ifconfig  查看网卡
    配置网卡：
    ifconfig eth0 192.168.118.2
    eth0:网卡名
    192.168.118.2：配置的网卡
    此配置，只是临时有效，重启后失效，如果想长期生效，则需要修改配置文件
    
    如果出现设置了桥接，并且在同一个IP地址段的地址后，还是无法连接，则可能针对于笔记本，如果有主机有两块网卡，一个有线网卡，一个无线网卡，
    在桥接时，虚拟机中编加-虚拟机网络配置中  手动设置一下桥 接哪个网卡




# 二、学习LINUX的注意事项
    注意：1.严格区分大小写
      2.linux中所有内容以文件形式保存，包括硬件
    	硬盘文件是/dev/sd[a-p]
    	光盘文件是/dev/sr0等
    	命令行只是临时保存
    	
    	ls /bin/  底下都是可执行命令
      3.Linux不靠扩展名区分文件类型
       压缩包：“*.gz” *.bz2  *.tar.bz2 *.tgz等
       二进制软件包：   *.rpm
       网页文件  *.html   *.php
       脚本文件  *.sh  (shell脚本)
       配置文件  *.conf
      4.Linux所有的存储设备都必须挂载之后用户才能使用，包括硬盘、U盘和光盘
      
       5.Windows下的程序不能直接在Linux中安装和运行

# 三、服务器管理和维护建议

## 1.各目录作用

| 目录&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | 说明&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| /bin/                                                        | 存放系统命令的目录，普通用户和超级用户都可以执行。不过放在/bin下的命令在单用户模式下也可以执行 |
| /sbin/                                                       | 保存和系统环境设置相关的命令，只有超级用户可以使用这些命令进行系统环境设置，但是有些命令可以允许普通用户查看 |
| /usr/bin/                                                    | 存放系统命令的目录，普通用户和超级用户都可以执行。这些命令和系统启动无关，在单用户模式下不能执行 |
| /usr/sbin/                                                   | 存放根文件系统不必要的系统管理命令，例如多数服务程序。只有超级用户可以使用。大家其实可以注意到linux的系统，在所有sbin目录中保存的命令只有超级用户可以使用，“bin”目录中保存的命令所有用户都可以使用 |
| /boot/                                                       | 系统启动目录 ，保存系统启动相关的文件，如内核文件和启动引导程序（grub）文件等 |
| /dev/                                                        | 设备文件保存位置。我们已经说过linux中所有内容以文件形式保存，包括硬件。那么这个目录就是用来保存所有硬件设备文件的 |
| /etc/                                                        | 配置文件保存位置。系统内所有采用默认安装方式（rpm安装）的服务的配置文件全部都保存在这个目录当中，如用户账户和密码，服务的启动脚本常用服务的配置文件等 |
| /home/                                                       | 普通用户的家目录。建立每个用户时，每个用户要有一个默认的登录位置，这个位置就是这个用户的家目录，所有普通用户的家目录就是在/home下建立一个和			用户名相同的目录。如用户user1的家目录就是/home/user1 |
| /lib/                                                        | 系统调用的函数库保存位置                                     |
| /lost+found/                                                 | （丢失的+找到的）当系统意外崩溃或机器意外关机，而产生一些文件碎片放在这里。当系统启动的过程 中fsck工具会检查这里，并修复已经损坏的文件系统。这个目录只在每个分区中出现，例如/lost+found就是根分区的备份恢复目录， /boot/lost+found就是/boot分区的备份恢复目录 |
| /media/                                                      | 挂载目录。系统建议是用来挂载体设备的，例如软盘和光盘         |
| /mnt/                                                        | 挂载目录。早期linux中只有这一个挂载目录，并没有细分，现在这个目录系统建议挂载额外设备，如u盘，移动硬盘和其他操作系统的分区 |
| /misc/                                                       | 挂载目录。系统建议用来挂载nfs服务的共享目录。我们在刚刚已经解释了挂载，我们应该知道只要是一个已经建立的空目录就可以作为挂载点。那么系统虽然准备了三个默认挂载目录/media /mnt  /misc，但是到底在哪个目录中挂载什么设备都可以由管理员自己决定 |
| /opt/                                                        | 第三方安装的软件保存位置。这个目录就是放置和安装其他软件的位置，我手工安装的源码包软件都可以安装到这个目录当中。不过我还是习惯把软件放置到/usr/local目录当中，也就是说/usr/local目录也可以用来安装软件 |
| /proc/                                                       | 虚拟文件系统，该目录中的数据并不保存到硬盘当中，而是保存到内存当中。主要保存系统的内核，进程，外部设备状态和网络状态灯。如/proc/cpuinfo是保存cpu信息的，/proc/devices是保存设备驱动的列表的，/proc/filesystems是保存文件系统列表的，/proc/net/是保存网络协议信息的 |
| /sys/                                                        | 虚拟文件系统。和/proc目录相似，都是保存在内存当中的，主要是保存于内核相关信息的 |
| /root/                                                       | 超级用户的家目录。普通用户家目录在/home/下，超级用户家目录直接在"/"下 |
| /srv/                                                        | 服务数据目录。一些系统服务启动之后，可以在这个目录中保存所需要的数据 |
| /tmp/                                                        | 临时目录。系统存放临时文件的目录，该目录下所有用户都可以访问和写入。我们建议此目录中不能保存重要数据最好每次开机都把该目录清空 |
| /usr/                                                        | 系统软件资源目录。注意usr不是user的缩写，而是" Unix Softwre Resource"的缩写，所以不是存放用户数据，而是存放系统软件资源的目录。系统中安装的软件大多数保存在这里，所以除了/usr/bin/ 和 /usr/sbin/这两个目录，我在介绍几个/usr/下的二级目录 |
| /var/                                                        | 动态数据保存位置。主要保存缓存、日志以及软件运行所产生的文件 |


## 2.远程服务器不允许关机，只能重启

	重启时应该关闭服务
	不要在服务器访问高峰运行高负载命令
	远程配置防火墙时不要把自己踢出服务器
	指定合理的密码规范并定期更新
	合理分配权限（系统启动服务越少越好，权限越小越好）
	定期备份重要数据和日志（etc  lib   var usr boot）


​	
# 四、 Linux常用命令
	命令格式
	命令  【-选项】 【参数】
	例：  ls -la /etc
	说明：个别命令使用不遵循此格式
			当有多个选项时，可以写在一起
			简化选项与完整选项

## 	4.1 文件处理命令
### 4.1.1 命令格式与目录处理命令ls

    命令名称: ls
    命令英文原意：list 
    命令所在路径: /bin/ls
    执行权限 ：所有用户
    功能描述：显示目录文件
    语法 : ls  选项[-ald] [文件或目录]
     -a 显示所有文件，包括隐藏文件    all
     -l 详细信息显示   lang  
        权限|计数|所有者|所属组|文件大小(字节)|最后一次修改时间|文件名	
         - rw- --- --- 1  root root 1205 3月  3 08:10 文件名
    		 分组分为3类  u所有者，g用户组，o其他人 
    		 - rw- r-- r--
    	 -文件类型（-二进制文件 d目录  l软链接文件）
    	 r 读   w写  x执行 
    -d 查看目录属性   
    -h 人性化选项
    -i i-node号


​			
​			
​			
### 4.1.2 目录处理命令

#### 4.1.2.1 创建目录 mkdir 


    命令英文原意：make directories 
    命令所在路径: /bin/mkdir
    执行权限 ：所有用户
    语法 : mkdir  -p  [目录名称]
     -p 递归创建
     范例：$ mkdir -p /tmp/Japan/boduo
           $ mkdir /tmp/Japan/longze/tmp/Japan/cangjing


​	 
#### 4.1.2.2 切换目录 cd

    命令英文原意：change directory
    命令所在路径: shell内置命令
    执行权限 ：所有用户
    语法 : cd [目录]
    范例：$ cd /tmp/Japan/boduo 切换到指定目录
          $ cd .. 回到上一级目录

#### 4.1.2.3 显示当前目录 pwd

    命令英文原意: pring working directory
    命令所在路径: /bin/pwd
    执行权限 ：所有用户
    语法 : pwd
    范例：$ pwd
          /tmp/Japan

#### 4.1.2.4 删除空目录 rmdir

    命令英文原意: remove empty directories
    命令所在路径: /bin/rmdir
    执行权限 ：所有用户
    语法 : rmdir[目录名]
    范例：$ rmdir /tmp/Japan/boduo


​	
#### 4.1.2.5 复制文件或目录 cp

    命令英文原意: copy
    命令所在路径: /bin/cp
    执行权限 ：所有用户
    语法 : cp -rp [原文件或目录] [目标目录]
        -r 复制目录
        -p 保留文件属性
        
     范例：$ cp /tmp/Japan /home/jia+ (复制的同时改名)
     不加 -r 则是复制文件

#### 4.1.2.6 剪切文件 、改名 mv

    命令英文原意: movie
    命令所在路径: /bin/mv
    执行权限 ：所有用户
    语法 : mv  [原文件或目录] [目标目录]
    mv可以剪切目录或文件    和cp不一样，不需要加-r
    范例：$ mv /tmp/Japan/cangjing /root
        $ mv /tmp/Japan /home/jia+ (前切的同时改名)

#### 4.1.2.7 删除文件（也可以删除目录） rm

    命令英文原意: remove
    命令所在路径: /bin/rm
    执行权限 ：所有用户
    语法 : rm -rf  [文件或目录]
    -r 删除目录
    -f 强制执行(删除之前不询问)
    范例：$ 

任何一个命令终止可按Ctrl+c


### 4.1.3 文件处理命令 

#### 4.1.3.1 创建空文件 touch

    命令英文原意: 
    命令所在路径: /bin/touch
    执行权限 ：所有用户
    语法 :touch [文件名]
    范例：$ touch Japanlovestory.list
           $ touch "Japanlovestory go"

#### 4.1.3.2 显示文件内容 cat （适合浏览内容较少的文件）

    命令英文原意: 
    命令所在路径: /bin/cat
    执行权限 ：所有用户
    语法 :cat [文件名]
       -n 显示行号
    范例：$ cat /etc/issue
           $ cat -n /etc/services

#### 4.1.3.3 显示文件内容(反向列示) tac 

    命令英文原意: 
    命令所在路径: /usr/bin/tac
    执行权限 ：所有用户
    语法 :tac [文件名]
        -n 显示行号
    范例：$ tac /etc/issue

#### 4.1.3.4 分页显示文件内容 more 

    命令英文原意: 
    命令所在路径: /bin/more
    执行权限 ：所有用户
    语法 :more [文件名]
        (空格)或f 一页一页翻
        （Enter） 一行一行翻
        q或Q      退出
    范例：$ more /etc/services

#### 4.1.3.5 分页显示文件内容（可向上翻页） less 

    命令英文原意: 
    命令所在路径: /usr/bin/less
    执行权限 ：所有用户
    语法 :less [文件名]
        (空格)或f 一页一页翻
        （Enter） 一行一行翻
        pageUP    向上翻页
        上箭头    向上翻一行
        按/ service   搜索关键词service
        按n      搜索下一处关键词
        q或Q      退出
    范例：$ less /etc/services

#### 4.1.3.6 显示文件前面几行 head 

    命令英文原意: 
    命令所在路径: /usr/bin/head
    执行权限 ：所有用户
    语法 :head [文件名]
        -n 指定行数
        (不指定行数，默认显示前10行)
    范例：$ head -n 20 /etc/services

#### 4.1.3.7 显示文件后面几行 tail

    命令英文原意: 
    命令所在路径: /usr/bin/tail
    执行权限 ：所有用户
    语法 :tail [文件名]
        -n 指定行数
        (不指定行数，默认显示后10行)
        -f 动态显示文件末尾内容
        （当文件（日志）内容更新后，会显示更新的内容）
    范例：$ tail -n 20 /etc/services	

### 4.1.4 链接命令

#### 4.1.4.1 生成链接文件 ln

    命令英文原意: link
    命令所在路径: /bin/ln
    执行权限 ：所有用户
    语法 :ln -s [原文件] [目标文件]
       -s 创建软链接
    范例：$ ln -s /etc/issue /tmp/issue.soft
            创建/etc/issue的软链接/tmp/issue.soft
          $ ln /etc/issue /tmp/issue.hard
            创建文件/etc/issue的硬链接/tmp/issue.hard
    软链接特点：1.权限三个rwx          2.文件大小很小，相当于windows快捷方式，
    3.ls查看时，箭头指向源文件
    硬链接特点：
        1.相同于copy，可同步更新，原文件删除，    硬链接文件还可打开。
        2.每个文件都有各自的i节点，硬链接文件的i节点和原文件相同。
        3.硬链接不可跨分区
        4.硬链接不可针对目录使用

## 4.2 权限管理命令  
### 4.2.1 改变文件或目录权限 chmod 

    命令英文原意: change the permissions mode of a file 
    命令所在路径: /bin/chmod
    执行权限 ：所有用户
    语法 : chmod [{ugoa}[+-=]{rwx}] [文件或目录]
               -R 递归修改
                u:所有者
                g：所属组
                o:其他
                a:所有all（所有者，所属组，其他）
                [mode=421] [文件或目录]
        权限的数字表示：


| 权限 | 数字 |
| ---- | ---- |
| r    | 4    |
| w    | 2    |
| x    | 1    |

| 权限 | 数字 |
| ---- | ---- |
| rwx  | 7    |
| rw-  | 6    |
| r--  | 4    |

- 文件目录权限总结

        代表字符 | 权限 | 对文件的含义 | 对目录的含义
        ---|---|---|---|
        r | 读权限 | 可以查看文件内容 | 可以列出目录中的内容
        w | 写权限 | 可以修改文件内容 | 可以在目录中创建、删除文件
        x | 执行权限 | 可以执行文件 | 可以进入目录 


    ​    
    ​        
    ​    
    范例： chmod u+x /tmp/filename
           chmod 421 /tmp/filename
           chmod -R 777 testdir
           修改目录testfile及其目录下文件为所有用户具有全部权限

>改变文件的权限 所有者和root都可以

### 4.2.2 改变文件或目录的所有者 chown

    命令英文原意: change file ownership
    命令所在路径: /bin/chown
    执行权限 ：所有用户
    语法 : chown [用户] [文件或目录]
    范例： $ chown haojiaxin testfile
        改变文件testfile的所有者为haojiaxin    

> 只有root可以改变文件的所有者
> 所有者是必须存在的

### 4.2.3 改变文件或目录的所属组 chgrp

    命令英文原意: change file group ownership
    命令所在路径: /bin/chgrp
    执行权限 ：所有用户
    语法 : chgrp [用户组] [文件或目录]
    范例： $ chgrp lampbrother fengjie
       改变文件fengjie的所属组为lampbrother   

> 文件或目录创建的默认的所有者为创建文件的人，默认的所属组为创建文件的用户的缺省组

### 4.2.4 显示、设置文件的缺省权限 umask

    命令英文原意: the user file-creation mask
    命令所在路径: Shell内置命令
    执行权限 ：所有用户
    语法 : umask [-S] 
            -S 以rwx形式显示新建文件缺省权限
    范例： $ umask -S 
            umask 023 设置创建目录或文件的权限为023

> 创建目录或文件时的默认权限为rwxr-xr-x=755

> 如要修改创建目录或文件时的默认权限为rwxr-xr--

> 则先写出rwxr-xr-- = 754

>        777 - 754 = 023

> 再执行 umask 023

> 即可修改创建目录或文件时的默认权限为rwxr-xr--

> 创建目录的默认权限为rwxr-xr-x

> 创建文件的默认权限为rw-r--r--

> 直接执行umask(老版本linux系统) 显示0022
> 新版本linux系统可以使用  -S 选项来看到rwx格式的权限


第一个码：0？？
第二个：第三个,第四个码:777-022=755=rwxr-xr-x

 


## 4.3 文件搜索命令

### 4.3.1 文件搜索命令 find(相当于windows中的搜索)
> windows中Everything搜索工具

    命令英文原意: 
    命令所在路径: /bin/find
    执行权限 ：所有用户
    语法 : find [搜索范围] [匹配条件] 
            
    范例： $ find /etc -name init
        在目录/etc中查找文件init（只能搜索文件名等于init的文件）
        
        $ find /etc -name *init* （通配符）
        在目录/etc中查找文件名包含init的文件
        -iname 不区分大小写

| 通配符 | 含义                      |
| ------ | ------------------------- |
| *      | 表示0个或0个以上 任意字符 |
| ？     | 表示1个任意字符           |

	   $ find / -size +204800 （单位是数据块：linux系统中存储文件的最小单位）
	   在根目录下查找大于100MB的文件
	   +n 大于  -n 小于  n 等于
	   
	   $ find /home -user haojiaxin
	    在根目录下查找所有者为haojiaxin的文件
	
	  $ find /home -group haojiaxin
	    -group 根据所属组查找
	    
	   $ find /etc -cmin -5
	    -n 分钟之内  +n 超过分钟
	   在/etc下查找5分钟内被修改过的属性的文件和目录
	   
	   -amin 访问时间 access
	   -cmin 文件属性 change
	   -mmin 文件内容 modify 
	   
	   $ find /etc -size +163840 -a -size -204800
	   在 /etc 下查找大于80MB小于100MB的文件
	   -a 两个条件同时满足
	   -o 两个条件满足任意一个即可
	   
	   $ find /etc -name init* -a -type f
	   在/etc目录下查找名为init开头的文件
	   
	   -type 根据文件类型查找  f 文件  d 目录   l 软链接文件
	   
	   $ find . -inum 31531 -exec rm {} \;
	   在当前目录中查找i 节点为31531 的文件 然后执行删除；
	   -inum 根据i节点查找 
	   （用i节点可以查找同一分区中（因为硬链接不可跨分区）硬链接的文件，或者删除文件名称比较复杂的文件）
	   
	   $ find  /etc -name inittal -exec ls -l {} \;
	   在/etc下查找inittab文件并显示其祥细信息
	   -exec/-ok 命令 {} \;对搜索结果执行操作

| 选项      | 含义                                               |
| --------- | -------------------------------------------------- |
| -exec/-ok | 命令连接符 ：对前面结果的执行 -ok:执行前会询问每个 |
| 命令      | 要执行的命令                                       |
| { }       | 查找到结果的集合，结果可能不是一个                 |
| \;        | ;结束，其中\为转义符                               |


> linux系统中 1个数据块=512字节=0.5K
> 1kB等于2个数据块

> 100M = 102400KB = 204800数据块




### 4.3.2 其他搜索命令

#### 4.3.2.1 在文件资料库中查找文件 locate 


    命令英文原意: 
    命令所在路径: /usr/bin/locate
    执行权限 ：所有用户
    语法 : locate 文件名
           -i 不区分大小写
            
    范例： $ locate inittab
     
     使用locate 搜索 locate
     其中有个/var/lib/mlocate/mlocate.db就是一个文件资料库，所有的文件系统会定期更新到mlocate.db,刚建立的文件使用locate可以查找不到，因为没有更新到mlocate.db中，可以使用 updatedb 命令手动更新 mlocate.db

注意：/tmp 中的文件不在文件资料库收录的范围，所以如果是在/tmp中的文件，使用locate不会搜索出来。

### 4.3.2.2 搜索命令所在目录及别名信息 which


    命令英文原意: 
    命令所在路径: /usr/bin/which
    执行权限 ：所有用户
    语法 :  which 命令


​	        
	范例： $ which rm
	    查看rm命令
	显示：alias rm = "rm -i" 
	       /bin/rm
	   alias:别名 

### 4.3.2.3 搜索命令所在目录及帮助文档路径 whereis


    命令英文原意: 
    命令所在路径: /usr/bin/whereis
    执行权限 ：所有用户
    语法 :  whereis [命令名称]


​	      
	范例： $ whereis ls
	    查看ls命令

### 4.3.2.4 在文件中搜寻字串匹配的行并输出 grep


    命令英文原意: 
    命令所在路径: /bin/grep
    执行权限 ：所有用户
    语法 :  grep -iv  [指定字串] [文件]
            -i 不区分大小写
            -v 排除指定字串
          
    范例： $ grep mysql /root/install.log
        
        $ grep -v ^# /etc/inittal
        查找/etc/initial文件中排除以#号开头的行


## 4.4 帮助命令

### 4.4.1 获得帮助信息 man

```
命令英文原意: manual
命令所在路径: /usr/bin/man
执行权限 ：所有用户
语法 :  man [命令或配置文件]
           
	      
范例： $ man ls 
查看ls命令的帮助信息
查看命令：
看这个命令的name，选项; 再使用more进行查看
$ man services（不需要加绝对路径，否则会显示文件内容）
查看配置文件：
看这个配置文件的name，格式; 再使用more进行查看
查看配置文件services的帮助信息
q 退出
 /string 要查找的string
 空格：下一页c
回车：下一行
```

```
$ man passwd linux系统中有一个命令叫passwd 有一个配置文件也叫passwd 使用 man passwd 查询时，默认会显示命令，如果查询配置文件的帮助
执行 man 5 passwd
```
```        
whereis passwd  
帮助类型有很多种，其中
```
| 符号        | 含义         |
| ----------- | ------------ |
| passwd.1.gz | 命令的帮助   |
| passwd.5.gz | 配置文件帮助 |

### 4.4.2 查看命令的简短信息 whatis

```
命令英文原意: 
命令所在路径: 
执行权限 ：所有用户
语法 :  whatis [命令]

```

### 4.4.3 查看配置文件的简短信息 apropos

```
命令英文原意: 
命令所在路径: 
执行权限 ：所有用户
语法 :  apropos [命令]
```

### 4.4.4 查看命令的描述信息 --help

```
命令英文原意: 
命令所在路径: 
执行权限 ：所有用户
语法 :   [命令] --help

```

### 4.4.5 获得Shell内置命令的帮助信息 help

```
命令英文原意: 
命令所在路径: Shell内置命令
执行权限 ：所有用户
语法 :   help 命令
范例： $ help umask
    查看umask命令的帮助信息
```
```
所有 which/whereis  找不到所在路径的命令 都是Shell内置命令 不能使用man来查看帮助
```
```
修改日期：
查看日期格式  man date
date MMDDhhmm......
```


## 4.5 用户管理命令

### 4.5.1 添加新用户 useradd
```
命令英文原意: 
命令所在路径: /usr/sbin/useradd
执行权限 ：root
语法 :   useradd 用户名
范例： $ useradd yangmi
    
```

### 4.5.2 设置用户密码 passwd
```
命令英文原意: 
命令所在路径: /usr/bin/passwd
执行权限 ：所有用户
语法 :   passwd 用户名
范例： $ passwd yangmi
    
```

### 4.5.3 查看登录用户信息 who
```
命令英文原意: 
命令所在路径: /usr/bin/who
执行权限 ：所有用户
语法 :   who
范例： $ who
    
```
who返回信息格式
登录用户名 登录终端（ tty本地终端  pts远程终端 ) 登录时间（/登录IP地址）

### 4.5.4 查看登录用户祥细信息 w

```
命令英文原意:  
命令所在路径: /usr/bin/w
执行权限 ：所有用户
语法 : w
范例： $ w

```

## 4.6 压缩解压命令




### 4.6.1 压缩文件 gzip

.zip window和linux都不需要装软件就可以解压
```
命令英文原意:  GNUzip
命令所在路径: /bin/gzip
执行权限 ：所有用户
语法 : gzip[文件]
压缩后文件格式： .gz
范例： $ w

```

### 4.6.2 解压缩.gz的压缩文件 gunzip / gzip -d


```
命令英文原意:  GUN unzip 
命令所在路径: /bin/gunzip
执行权限 ：所有用户
语法 : gunzip [压缩文件]
压缩后文件格式： .gz
范例： $ gunzip boduo.gz

```
特点：只能压缩 文件，压缩 后不保留原文件


### 4.6.3 打包目录  tar


```
命令英文原意:  
命令所在路径: /bin/tar
执行权限 ：所有用户
语法 : tar 选项[-zcf] [压缩后文件名] [目录]
        -c 打包
        -v 显示祥细信息
        -f 指定文件名
        -z 打包同时压缩
压缩后文件格式： .tar.gz
范例： $ tar -zcf Japan.tar.gz Japan
    将目录Japan打包并压缩为.tar.gz文件

```
### 4.6.4 压缩解压命令  tar


```
命令英文原意:  
命令所在路径: /bin/tar
执行权限 ：所有用户
语法 : tar 选项[-zcf] [压缩的文件名]
        -x 解包
        -v 显示祥细信息
        -f 指定解压文件
        -z 解压缩 

范例： $ tar -zxvf Japan.tar.gz
```
### 4.6.4 压缩文件或目录 zip

>压缩比不高
```
命令英文原意:  
命令所在路径: /usr/bin/zip
执行权限 ：所有用户
语法 : zip 选项[-r] [压缩后文件名] [文件或目录]
        -r 压缩目录
压缩后文件格式： .zip
范例： $ zip japan.zip japan
```
### 4.6.5 解压.zip的压缩文件 unzip


```
命令英文原意:  
命令所在路径: /usr/bin/unzip
执行权限 ：所有用户
语法 : unzip [压缩文件]
范例： $ unzip test.zip
```
### 4.6.6 压缩文件 bzip2


```
命令英文原意:  
命令所在路径: /usr/bin/bzip2
执行权限 ：所有用户
语法 : bzip2 选项[-k][文件]
        -k 产生压缩文件后保留原文件
压缩后文件格式 .bz2
范例： $ bzip2 -k boduo
        压缩文件boduo
        $ tar -cjf Japan.tar.bz2 Japan
        压缩目录 Japan （先打包再压缩 为.bz2格式）
```
### 4.6.7 解压.bz2压缩格式的文件 bunzip2


```
命令英文原意:  
命令所在路径: /usr/bin/bunzip2
执行权限 ：所有用户
语法 : bunzip2 选项[-k][压缩文件]
        -k 解压缩后保留原文件
压缩后文件格式 .bz2
范例： $ bunzip2 -k boduo.bz2
        解压文件boduo.bz2
        $ tar -xjf Japan.tar.bz2
        解压目录 Japan.tar.bz2 （解压并解包）
```

解压缩命令总结
| 格式     | 压缩     | 解压缩          |
| -------- | -------- | --------------- |
| .gz      | gzip     | gunzip(gzip -d) |
| .tar     | tar -cf  | tar -xf         |
| .tar.gz  | tar -zcf | tar -zxf        |
| .zip     | zip -r   | unzip           |
| .bz2     | bzip2    | bunzip2         |
| .tar.bz2 | tar -cjf | tar -xjf        |



## 4.7 网络命令


### 4.7.1 给用户发信息， 以Ctrl+D保存结束 write
```
命令英文原意:  
命令所在路径: /usr/bin/write
执行权限 ：所有用户
语法 : write <用户名>
范例： # write linzhiling
```
### 4.7.2 给所有用户发广播消息 wall

```
命令英文原意:  
命令所在路径: /usr/bin/wall
执行权限 ：所有用户
语法 : wall [message]
范例： # wall ShenChao is a honest man!
```
### 4.7.3 测试网络连通性 ping

```
命令英文原意:  
命令所在路径: /bin/ping
执行权限 ：所有用户
语法 : ping 选项 ip地址
        -c 指定发送次数
        ctrl+c 取消
范例： # ping 192.168.118.156
       # ping -c 3 192.168.118.156
       ping 3次
```

### 4.7.4 查看和设置网卡息 ifconfig

```
命令英文原意:  interface configure
命令所在路径: /sbin/ifconfig
执行权限 ：root
语法 : ifconfig 网卡名称 ip地址
范例： # ifconfig eth0 192.168.118.2
```

**eth：代表本地的真实网卡，从eth0开始、以此类推,如果有第2块网卡则是eth1**

**lo：回环网卡**

### 4.7.5 查看发送电子邮件 mail

```
命令英文原意:  
命令所在路径: /bin/mail
执行权限 ：所有用户
语法 : mail [用户名]
范例：# mail root  [messge] Ctrl+D 发送
        mail 后面不跟用户名，则是查看
        输入1：查看邮件号为1的邮件
            h:返回邮件列表
            d 邮件号：删除邮件
            q： 退出。
        
    
```

### 4.7.6  检查某特定用户上次登录的时间 lastlog

```
命令英文原意:  
命令所在路径: /usr/bin/lastlog
执行权限 ：所有用户
语法 : lastlog
范例：$ lastlog
      $ lastlog -u 502
       查看指定用户uid(用户管理)的最后一次登录时间
```

### 4.7.7 列出目前与过去登入系统的用户信息 last

```
命令英文原意:  
命令所在路径: /usr/bin/last
执行权限 ：所有用户
语法 : last 
范例：$ last
```

### 4.7.8 显示数据包到主机间的路径 traceroute

```
命令英文原意:  
命令所在路径: /bin/traceroute
执行权限 ：所有用户
语法 : traceroute
范例：$ traceroute www.lampbrother.net
```

### 4.7.9 显示网络相关信息 netstat

```
命令英文原意:  
命令所在路径: /bin/netstat
执行权限 ：所有用户
语法 : netstat [选项]
范例：netstat -tlun 查看本机监听的端口
      netstat -an 查看本机所用的网络连接
      netstat -rn 查看本机路由表
```
**选项**

| 选项 | 说明                                                         |
| ---- | ------------------------------------------------------------ |
| -t   | TCP协议：三次握手 HTTP采用TCP ： 传输控制协议的简称          |
| -u   | UDP协议：快，不握手，连接可靠性差点事 ：像发短信，可能别人收不到　。 |
| -l   | 监听                                                         |
| -r   | 路由                                                         |
| -n   | 显示IP地址和端口号                                           |

### 4.7.10 配置网络 setup

```
命令英文原意:  
命令所在路径: /usr/bin/setup
执行权限 ：root
语法 : setup
范例：setup
```
**DHCP 自动分配**

配置完成IP后，需要重启网络服务
网络服务命令： service network restart

### 4.7.11 挂载命令 mount

```
命令英文原意:  
命令所在路径: /bin/mount
执行权限 ：所有用户
语法 : mount [-t 文件系统] 设备文件名 挂载点
范例：# mount -t iso9660 /dev/sr0 /mnt/cdrom
```
- /dev/sr0 是默认的 设备文件名
- 挂载之前首先要创建 /mnt/cdrom/ 目录
- -t iso9660  可以省略

- mount 不加选项查看已经挂载的设备
### 4.7.12 卸载挂载点 umount

```
命令英文原意:  
命令所在路径: /bin/umount
执行权限 ：所有用户
语法 : umount 挂载点
范例：# umount /mnt/cdrom
```
- 卸载时，当前目录不能在挂载点上，否则会提示正忙
- 卸载时，umount 后面可以跟随设备名，也可以跟随挂载点，只能跟随一个

## 4.8 关机重启命令

### 4.8.1 关机重启命令 shutdown

```
命令英文原意:  
命令所在路径: 
执行权限 ：所有用户
语法 : shutdown [选项] 时间
范例：# shutdown -h now 
      # shutdown -r now 
      # shutdown -h 20:30
选项：
    -c 取消前一个关机命令（针对指定关机时间时使用）
    -h 关机
    -r 重启
```

### 4.8.2 其他关机命令 halt poweroff init 0

```
语法 : halt
语法 : poweroff
语法 : init 0
```

### 4.8.3 其他重启命令 
```
语法 : reboot
语法 : init 6
```

### 4.8.4 系统运行级别？

| 数字 | 含义                      |
| ---- | ------------------------- |
| 0    | 关机                      |
| 1    | 单用户                    |
| 2    | 不完全多用户，不含NFS服务 |
| 3    | 完全多用户                |
| 4    | 未分配                    |
| 5    | 图形界面                  |
| 6    | 重启                      |

```
使用以下命令可查看inittab配置文件中的配置
或修改系统默认运行级别
# cat /etc/inittab 
注：
默认不能改为0或6 

查询系统运行级别使用以下命令：
# runlevel
```

### 4.8.4 退出登录命令 logout
```
语法 : logout
```

# 五、 文本编辑器Vim

- Vim是一个功能强大的全屏幕文本编辑器，是Linux/UNIX上最常用的文本编辑器，它的作用是建立、编辑、显示文本文件。
- Vim没有菜单， 只有命令。

## 5.1 Vim常用操作
- 进入 vi filename
- 插入模式： i a o 

| 命令 | 作用                 |
| ---- | -------------------- |
| a    | 在光标所在字符后插入 |
| A    | 在光标所在行尾插入   |
| i    | 在光标所在字符前插入 |
| I    | 在光标所在行行首插入 |
| o    | 在光标下插入新行     |
| O    | 在光标上插入新行     |

- 定位命令

| 命令      | 作用                 |
| --------- | -------------------- |
| :set nu   | 在光标所在字符后插入 |
| :set nonu | 在光标所在行尾插入   |
| gg        | 到第一行             |
| G         | 到最后一行           |
| nG        | 到第n行              |
| :n        | 到第n行              |
| $         | 移至行尾             |
| 0         | 移至行首             |

- 删除命令

| 命令    | 作用                         |
| ------- | ---------------------------- |
| x       | 删除光标所在处字符           |
| nx      | 删除光标所在和n个字符        |
| dd      | 删除光标所在行，ndd删除n行   |
| dG      | 删除光标所在行到文件末尾内容 |
| D       | 删除光标所在处到行尾内容     |
| :n1,n2d | 删除指定范围的行             |

- 复制和剪切命令

| 命令 | 作用                         |
| ---- | ---------------------------- |
| yy   | 复制当前行                   |
| nyy  | 复制当前行以下n行            |
| dd   | 剪切当前行                   |
| ndd  | 剪切当前行以下n行            |
| p、P | 粘贴在当前光标所在行下或行上 |

- 替换和取消命令

| 命令 | 作用                                |
| ---- | ----------------------------------- |
| r    | 取代光标所在处字符                  |
| R    | 从光标所在处开始替换字符，按Esc结束 |
| u    | 取消上一步操作                      |


- 搜索和搜索替换命令

| 命令              | 作用                                     |
| ----------------- | ---------------------------------------- |
| /string           | 搜索指定字符串，搜索时忽略大小写 :set ic |
| n                 | 搜索指定字符串的下一个出现位置           |
| :%s/old/new/g     | 全文替换指定字符串                       |
| :n1,n2s/old/new/g | 在一定范围（行）内替换指定字符串         |



- 保存和退出命令

| 命令            | 作用                                                         |
| --------------- | ------------------------------------------------------------ |
| :w              | 保存修改（write）                                            |
| :w new_filename | 另存为指定文件                                               |
| :wq             | 保存修改并退出 (quit)                                        |
| ZZ              | 快捷键，保存修改并退出                                       |
| :q!             | 不保存修改退出                                               |
| :wq!            | 强行保存修改并退出没有写权限的文件 （文件所有者及root可使用） |


- 回到命令模式： Esc
- 退出： :wq
- 显示行号 :set number / set nu

 

## 5.2 Vim使用技巧
- 导入其他文件内容到光标位置： :r filename
- 查看命令所在路径： :!which 命令

```
范例： :!which ls
```
- 导入命令执行结果： :r !命令
```
导入date（时间）命令执行结果到当前光标所在位置，
范例： :r !date 
```
- 定义快捷键： :map 快捷键 触发命令


```
范例：　:map ^P I#<ESC> （在行首插入注释符#）
                ^:ctrl+v
                P:ctrl+p
                I:跳到行首
                #：插入#号
                <ESC>:回到命令格式
        :map ^B 0x （删除行首注释#）
        :map ^H isamlee@lampbrother.net （插入邮箱）
            
```

- 连续行注释： :n1,n2s/^/#/g （在行首加#号）
         :n1,n2s/^#//g （去掉行首#号）
         :n1,n2s/^/\/\//g （其他语言中的注释，\：转义符）
- 替换： :ab mymail samlee@lampbrother.net
            
-----
注：vim的这些编辑命令快捷键,在重新启动系统后就失效了，因此可以在宿主目录下添加配置文件.vimrc ，root用户在/root下 其他用户在/home/username下

```
set nu
map ^P I#<ESC>
ab mymail email@163.com
......
```

# 六、 软件包管理简介

## 6.1 软件包分类
- 源码包
    - 脚本安装包
- 二进制包（.RPM包、系统默认包）

当前市面上流行的Linux系统主要分为Readhat和Debian两大系列，而android底层直接用linux原版内核。

一、Redhat系列

Redhat：(yum需要收费)主要是服务器型Linux，商用收费；RHEL是Red Hat Enterprise Linux的缩写。

CentOS：Redhat的100%复制版本，不收版权费用。

二、Debian系列

Debian：主要是桌面型Linux，代表为Ubuntu。

### 6.1.1 源码包

- 源码包的优点是：
    - 开源，如果有足够的能力，可以修改源代码
    - 可以自由选择所需的功能
    - 软件是编译安装，所以更加适合自己的系统，更加稳定也效率更高
    - 卸载方便
- 源码包的缺点：
    - 安装过程步骤较多，尤其安装较大的软件集合时（如LAMP环境搭建），容易出现拼写错误
    - 编辑过程时间较长，安装比二进制安装时间长
    - 因为是编译安装，安装过程中一旦报错新手很难解决

### 6.1.2 RPM包

- 二进制包的优点：
    - 包管理系统简单，只通过几个命令就可以实现包的安装、升级、查询和卸载
    - 安装速度比源码包安装快的多

- 二进制包的缺点：
    - 经过编译，不再可以看到源代码
    - 功能选择不如源码包灵活
    - 依赖性（安装顺序）



## 6.2 rpm包管理-rpm命令管理
### 6.2.1 rpm命令管理-包命名与依赖性
- RPM包命名原则
    - httpd-2.2.15-15.el6.centos.1.i686.rpm

| 名称       | 含义            |
| ---------- | --------------- |
| httpd      | 软件包名        |
| 2.2.15     | 软件版本        |
| 15         | 软件发布的次数  |
| el6.centos | 适合的Linux平台 |
| i686       | 适合的硬件平台  |
| rpm        | rpm包扩展名     |


    -  包名：httpd
    -  包全名：httpd-2.2.15-15.el6.centos.1.i686.rpm

- RPM包依赖性
    - 树形依赖： a->b->c
    - 环形依赖： a->b->c->a
    - 模块依赖： 模块依赖查询网站：www.rpmfind.net
      .so.0是库文件 ，则需要上网查

### 6.2.2 rpm命令管理-安装、升级与卸载

- 包全名与包名
    -  包全名：操作的包是没有安装的软件包时，使用包全名。而且要注意路径（安装，升级）
    -  包名：操作已经安装的软件包时，使用包名。是搜索/var/lib/rpm/中的数据库 （查询，卸载）
- RPM 包安装
```
rpm -ivh 包全名
选项：
    -i (install) 安装
    -v (verbose) 显示详细信息
    -h （hash）显示进度
    --nodeps 不检测依赖性
```

- RPM 包升级
```
rpm -Uvh 包全名
选项：
    -U (upgrade) 升级
    
```
-  卸载
```
rpm -e 包名
选项：
    -e (erase) 卸载
    -- nodeps 不检查依赖性
```

### 6.2.3 rpm命令管理-查询

- 查询包是否安装
```
rpm -q 包名
选项：
    -q 查询（query）
```
- 查询所有已经安装的RPM包
```
rpm -qa 
选项：
    -a 所有（all）
```

```
rpm -qa | grep httpd

```

- 查询软件包详细信息
```
rpm -qi 包名
选项：
    -i 查询软件信息（information）
    -p 查询未安装包信息（package）需加全包名
```
- 查询包中文件安装位置
```
rpm -ql 包名
选项：
    -l 列表(list)
    -p 查询未安装包信息（package）需加全包名 （查询打算安装在哪，安装位置在包组建时就决定了的）
```

- 查询系统文件属于哪个RPM包
```
rpm -qf 系统文件名
选项：
    -f 查询系统文件 属于哪个软件包(file)
   
```

- 查询软件包的依赖性
```
rpm -qR 包名
选项：
    -R 查询软件包的依赖性(requires)
    -p 查询未安装包信息（package）
```

### 6.2.3 rpm包校验和文件提取

- RPM包校验
```
rpm -V 已安装的包名
选项：
    -V 校验指定RPM包中的文件 （verify）
如果未提示，则未修改过
```
验证内容中的8个信息的具体内容如下：
| 字符 | 含义                                              |
| ---- | ------------------------------------------------- |
| S    | 文件大小是否改变                                  |
| M    | 文件的类型或文件的权限(rwx)是否被改变             |
| 5    | 文件MD5校验和是否改变（可以看成文件内容是否改变） |
| D    | 设备的中，从代码是否改变                          |
| L    | 文件路径是否改变                                  |
| U    | 文件的属主（所有者）是否改变                      |
| G    | 文件的属组是否改变                                |
| T    | 文件的修改时间改变                                |

- RPM包中文件提取
```
rpm2cpio 包全名 | \
cpio -idv .文件绝对路径

\:换行符，一行输不下时使用

rpm2cpio
#将rpm包转换为cpio格式的命令

cpio
#是一个标准工具，它用于创建软件档案文件和从档案文件中提取文件
选项：
    -V 校验指定RPM包中的文件 （verify）
如果未提示，则未修改过
```

```
cpio 选项 < [文件 | 设备]
选项：
    -i: copy-in模式，还原
    -d: 还原时自动新建目录
    -v: 显示还原过程
```

例：
```
rpm -qf /bin/ls
#查询ls命令属于哪个软件包

mv /bin/ls /tmp/
#造成ls命令误删除假象

rmp2cpio /mnt/cdrom/Packages/coreutils-8.4-19.el6.i868.rpm | cpio -idv ./bin/ls
#提取RPM包中ls命令到当前目录的/bin/ls下

cp /root/bin/ls /bin/
#把ls命令复制到/bin/目录，修复文件丢失
```

## 6.3 rpm包管理-yum在线管理

#红帽子公司需要收费
### 6.3.1 IP地址配置和网络yum源

- 访问内网只需 配ip和子网掩码 访问公同需配置网关和dns、IP、子网掩码缺一不可
- 使用setup命令
```
# setup 
```
- 启动网卡
```
# vi /etc/sysconfig/network-scripts/ifcfg-eth0
把ONBOOT="no"改为
ONBOOT="yes"
```
- 重启网络服务
```
# service network restart
```
- 网络yum源

```
# vi /etc/yum.repos.d/CentOS-Base.repo

```

| 配     置  | 说明                                                         |
| ---------- | ------------------------------------------------------------ |
| [base]     | 容器名称，一定要放在[]中                                     |
| name       | 容器说明，可以自己随便写                                     |
| mirrorlist | 镜像站点，这个可以注释掉（mirrorlist和baseurl都一样，mirrorlist是镜像，baseurl是真正的地址，建议注释掉mirrorlist，打开baseurl，但是都可以用） |
| baseurl    | 我们的yum源服务器的地址。默认是CentOS官方的yum源服务器，是可以使用的，服务器在国外，如果觉得慢，可以改成你喜欢的yum源地址 |
| enabled    | 此容器是否生效，如果不写或写成enable=1都是生效，写成enable=0 就是不生效 |
| gpgcheck   | 如果是1是指RPM的数字证书生效，如果是0则不生效                |
| gpgkey     | 数字证书的公钥文件保存位置。不用修改                         |


- 查看yum源地址

```
ls /etc/yum.repos.d/
默认为：CentOS-Base.repo
如果不能上网，可以让CentOS-Media.repo生效，让本机光驱设备作为yum源
```




### 6.3.2 yum命令
- 查询 

```
# yum list
 查询所有可用软件包列表
```

```
# yum search 关键字
搜索服务器上所有和关键字相关的包
```
- 安装

```
# yum -y install 包名
选项：
    install 安装
    -y 自动回答yes
例：yum -y install gcc
```
- 升级

```
# yum -y update 包名
选项：
    update 升级
    -y 自动回答yes
    如果不添加包名，则默认更新所有软件包，包括linux内核，更新linux内核后有的需要配置一下才能生效，如果远程的话，会导致linux系统崩溃,无法启动，慎重。
```

- 卸载

```
# yum -y remove 包名
选项：
    remove 卸载
    -y 自动回答yes
    yum卸载时，所依赖的包都会卸载，有可能被linux内核所依赖的包也会卸载，这样会导致系统崩溃。所以建议，安装软件包时，最小安装，尽量不卸载 。
```
- yum软件组管理命令

```
# yum grouplist
列出所有可用的软件组列表
```


```
# yum groupinstall 软件组名
安装指定软件组，组名可以由grouplist查询出来
```


```
yum groupremove 软件组名
卸载指定软件组
```



### 6.3.3 光盘yum源搭建

- 1. 挂载光盘

```
mount /dev/cdrom /mnt/cdrom/
```
- 2. 让网络yum源文件失效

```
cd /etc/yum.repos.d/
mv CentOS-Base.repo CentOS-Base.repo.bak
mv CentOS-Debuginfo.repo CentOS-Debuginfo.repo.bak
mv CentOS-Vault.repo  CentOS-Vault.repo.bak
```
- 3. 修改光盘yum源文件

```
vim CentOS-Media.repo

[c6-media]
#容器
name=CentOS-$releasever - Media
#容器说明
baseurl=file:///mnt/cdrom/
#        file:///media/cdrom/
#        file:///media/cdrecorder/
#地址，不再用网络作为源，所以协议为file，第三个/开始为光盘挂载点的绝对路径，注释掉两个多余地址
gpgcheck=1
enabled=1
# 修改为enabled=1 为让光盘yum源生效
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6

```


## 6.4 源码包管理

### 6.4.1 源码包和RPM包的区别
- 区别
    - 安装之前的区别：概念上的区别
    - 安装之后的区别：安装位置不同

- RPM包安装位置
    -  是安装在默认位置中

RPM包默认安装路径
| 目录            | 说明                       |
| --------------- | -------------------------- |
| /etc/           | 配置文件安装目录           |
| /usr/bin/       | 可执行的命令安装目录       |
| /usr/lib/       | 程序所使用的函数库保存位置 |
| /usr/share/doc/ | 基本的软件使用手册保存位置 |
| /usr/share/man  | 帮助文件保存位置           |

- 源码包安装位置
    - 安装在指定位置当中，一般是 
      /usr/local/软件名/
- 安装位置不同带来的影响
    - RPM包安装的服务可以使用系统服务管理命令（service）来管理，例如RPM包安装的apache的启动方法有两种：
        - /etc/rc.d/init.d/httpd start (RPM包的服务一般都会安装在此目录下)
        - service httpd start (service：redhat专有命令,此命令会搜索以上目录，找到执行，找不到报错，所以源码包安装的不能在以上目录中找到)
    - httpd的网址安装在 /var/www/html/

    - 而源码包安装的服务则不能被服务管理命令管理，因为没用安装到默认路径中。所以只能用绝对路径进行服务的管理，如：
        - /usr/local/apache2/bin/apachect1 start
### 6.4.2 源码包安装过程

- 1. 安装准备
    - 安装C语言编译器  gcc  (执行 rpm -q gcc 查看是否安装gcc)
    - 下载源码包 http://mirror.bit.edu.cn/apache/httpd/

- 2. 安装注意事项
    - 源代码保存位置 ：/usr/local/src/
        - usr:unix系统资源目录
        - local:本地
        - src:源代码缩写
    - 软件安装位置: /usr/local/
    - 如何确定安装过程报错：
        -  安装过程停止
        -  并出现error、warning或no的提示
- 3. 源码包安装过程
    -  下载源码包
    -  解压缩下载的源码包( tar -zxvf httpd-2.4.29)
    -  进入解压缩目录
        -  INSTALL：安装说明(可查看其中的安装步骤说明来进行安装)
        -  README:使用说明
    -  ./configure 软件配置与检查  ./configure -- prefix=/usr/local/软件名称（例如：apache2）
        -  定义需要的功能选项
        -  检测系统环境是否符合安装要求
        -  把定义好的功能选项和检测系统环境的信息都写入Makefile文件 ，用于后续的编辑( 执行完命令后，会自动写入)
    -  make 编译
        - make 报错后，执行make clean清空一下，重新执行
    -  make install 编译安装
- 4. 启动apache ，启动方法在INSTALL文件中有提示
    - /usr/local/apache2/bin/apachectl start
      启动成功后，在网页中输入IP地址显示it works! 则成功。
- 5. 源码包的卸载
    -  不需要卸载命令，直接删除安装目录即可。不会遗留任何垃圾文件。

```
 - rm -rf /usr/local/apache2/
```


## 6.5 脚本安装包与软件包选择

- 脚本安装包
    - 脚本安装包并不是独立的软件包类型，常见安装的是源码包。
    - 是人为把安装过程写成了自动安装的脚本，只要执行脚本，定义简单的参数，就可以完成安装。
    - 非常类似于windows下软件的安装方式。
- Webmin的作用
    -  Webmin是一个基于Web的Linux系统管理界面。您就可以通过图形化的方式设置用户帐号、Apache、DNS、文件共享等服务。
- Webmin安装过程
    -  下载软件
        -  http://sourceforge.net/projects/webadmin/files/webmin/
        -  解压缩，并进入解压缩目录
            -  du -sh webmin-1.881 查看文件大小
        -  执行安装脚本
            -   ./setup.sh
- 软件包选择
    - 用于网络用户访问的，如apache 建议使用源码包
    - 用于本机使用的，使用二进制包即可。


# 七、 用户和用户组管理
## 7.1 用户配置文件 
### 7.1.1 用户配置文件-用户信息文件/etc/passwd
- 用户管理简介
    - 所以越是对服务器安全性要求高的服务器，越需要建立合理的用户权限等级制度和服务器操作规范
    - 在Linux中主要是通过用户配置文件来查看和修改用户信息
- /etc/passwd
    - 第1字段：用户名称
    - 第2字段：密码标志:存放在影子文件中,只有root可以查看
    - 第3字段：UID（用户ID）
        - 0: 超级用户
        - 1-499：系统用户（伪用户），不能删除，否则会崩溃
        - 500-65535：普通用户
    - 第4字段：GID(用户初始组ID)
    - 第5字段: 用户说明
    - 第6字段：家目录
        - 普通用户：/home/用户名/
        - 超组长户: /root/
    - 第7字段：登录之后的Shell
- 初始组和附加组
    - 初始组：就是指用户一登录就立刻拥有这个用户组的相关权限，每个用户的初始组只能有一个，一般就是和这个用户的用户名相同的组名作为这个用户的初始组。
    - 附加组：指用户可以加入多个其他的用户组，并拥有这些组的权限，附加组可以有多个。
- Shell是什么
    - Shell就是Linux的命令解释器。
    - 在/etc/passwd当中，除了标准Shell是/bin/bash之外，还可以写如/sbin/nologin。


### 7.1.2 用户配置文件-影子文件/etc/shadow

- ll 命令可以查看文件信息

```
# ll /etc/shadow
```
- 影子文件 /etc/shadow
    - 第1字段：用户名
    - 第2字段：加密密码
        - 加密算法升级为SHA512散列加密算法
        - 如果密码位是“！！”或“*”代表没有密码，不能登录，（需要时可以在前面加个！禁用密码）
    - 第3字段：密码最后一次修改日期
        - 使用1970年1月1日作为标准时间，每过一天时间戳加1
    - 第4字段：两次密码的修改间隔时间（和第3字段相比）
    - 第5字段：密码有效期（和第3字段相比）
    - 第6字段：密码修改到期前的警告天数（和第5字段相比）
    - 第7字段： 密码过期后的宽限天数（和第5字段相比）
        - 0：代表密码过期后立即失效
        - -1：则代表密码永远不会失效。
    - 第8字段：账号失效时间
        - 要用时间戳表示
    - 第9字段：保留
- 时间戳换算
    - 把时间戳换算为日期
        - date -d "1970-01-01 16066 days"
    - 把日期换算为时间戳
        - echo $(($(datecv '' --date="2014/01/06"+%s)/86400+1))


### 7.1.3 用户配置文件-组信息文件/etc/group和组密码文件/etc/gshadow

- 组信息文件 /etc/group
    - 第1字段：组名
    - 第2字段：组密码标志
    - 第3字段：GID
    - 第4字段：组中附加用户

- 组密码文件/etc/gshadow
    - 第1字段：组名
    - 第2字段：组密码
    - 第3字段：组管理员用户名
    - 第4字段：组中附加用户

## 7.2 用户管理相关文件
- 用户的家目录
    - 普通用户：/home/用户名/，所有者和所属组都是此用户名，权限是700
    - 超级用户：/roo/，所有者和所属组都是root用户，权限是550
- 用户的邮箱
    - /var/spool/mail/用户名/
- 用户模板目录
    - /etc/skel/ :添加用户时会自动从此目录中copy信息到用户的家目录中


## 7.3 用户管理命令
### 7.3.1 用户添加命令useradd

- useradd命令格式
```
# useradd [选项] 用户名
选项：
    -u UID: 手工指定用户的UID号
    -d 家目录：手工指定用户的家目录
    -c （comment）用户说明：手工指定用户的说明
    -g 组名：手工指定用户的初始组
    -G 组名：指定用户的附加组
    -s shell：手工指定用户的登录shell. 默认是/bin/bash
```

- 添加默认用户
```
# useradd sc
    执行命令后查看以下文件 ，其是是在以下文件 中添加了相关的信息
    - # grep sc /etc/passwd
    - # grep sc /etc/shadow
    - # grep sc /etc/group
    - # grep sc /etc/gshadow
    - # ll -d /home/lamp/
    - # ll /var/spool/mail/lamp
```
- 指定选项添加用户

```
useradd -u 666 -G root,bin -d /home/lamp1 -c "test user" -s /bin/bash sc

-g ：不建议指定初始组，不好管理
-G： 可以使用此选项添加附加组，附加组必须是系统中已存在的组
```
- 用户默认值文件

    -  /etc/default/useradd
```

GROUP=100 #用户默认组
HOME=/home #用户家目录
INACTIVE=-1 #密码过期宽限天数 （shadow文件7字段）
EXPIRE=     #密码失效时间（8）
SHELL=/bin/bash #默认shell
SKEL=/etc/skel  #模板目录
CREATE_MAIL_SPOOL=yes #是否建立邮箱
```

    - /etc/login.defs

```
PASS_MAX_DAYS   99999 #密码有效期（5）
PASS_MIN_DAYS   0     #密码修改间隔（4）
PASS_MIN_LEN    5     #密码最小5位（PAM）
PASS_WARN_AGE   7     #密码到期警告（6）
UID_MIN         500   #最小和最大UID范围
UID_MAX         60000
ENCRYPT_METHOD  SHA512 #加密模式

```


### 7.3.2 修改用户密码passwd

- passwd命令格式

```
# passwd [选项] 用户名
选项：
    -S 查询用户密码的密码状态。仅root用户可用。
    -l 暂时锁定用户。仅root用户可用
    -u 解锁用户。仅root用户可用
    --stdin 可以通过管道符输出的数据作为用户的密码。
```
- 查看密码状态

```
# passwd -S xiaoming
xiaoming PS 2013-01-06 0 99999 7 -1
- 用户名密码设定时间（2013-01-06）
- 密码修改间隔时间（0）
- 密码有效期（99999）
- 警告时间 （7）
- 密码不失效（-1）

```
- 锁定用户和解锁用户

```
# passwd -l xiaoming
# passwd -u xiaoming
```
- 使用字符串作为用户的密码

```
# echo '123' | passwd --stdin xiaoming
```


### 7.3.3 修改用户信息usermod及修改用户密码状态chage
- 修改用户信息usermod
```
# usermod [选项] 用户名
选项：
    -u UID: 修改用户的UID号
    -c 用户说明：修改用户的说明信息
    -G 组名：修改用户的附加组
    -L: 临时锁定用户（Lock）
    -U： 解锁用户锁定(Unlock)
```
- 例：

```
# usermod -c "test user" lamp
#修改用户的说明
# usermod -G root lamp 
#把lamp用户加入root组
# usermod -L lamp 
#锁定用户
# usermod -U lamp
#解锁用户
```
- 修改用户密码状态chage

```
# chage [选项] 用户名
选项：
    -l: 列出用户的祥细密码状态
    -d 日期:  修改密码最后一次更改日期（shadow3字段）
    -m 天数： 两次密码修改间隔（4字段）
    -M 天数： 密码有效期（5字段）
    -W 天数:  密码过期前警告天数（6字段）
    -I 天数： 密码过期后宽限天数（7字段）
    -E 日期： 账号失效时间(8字段)
```
可使用VIM直接修改shadow文件
```
# chage -d 0 lamp
#这个命令其实是把密码修改日期归0了（shadow第3字段）
#这样用户一登陆就要修改密码
```




### 7.3.4 删除用户userdel及用户切换命令su

- 删除用户userdel

```
# userdel [-r] 用户名
选项： 
    -r 删除用户的同时删除用户家目录
```
- 手工删除用户

```
# vi /etc/passwd
# vi /etc/shadow
# vi /etc/group
# vi /etc/gshadow
# rm -rf /var/spool/mail/lamp
# rm -rf /home/lamp/
外加skel模板文件？
```
- 查看用户ID

```
# id 用户名
```
- 切换用户身份su

```
# su [选项] 用户名
选项：
    -: 选项使用“-”代表连带用户的环境变量一起切换 ，必填，否则报错
    -c 命令： 仅执行一次命令，而不切换用户身份
```

```
$ su - root
#切换成root
```

```
$ su - root -c "useradd user3"
#不切换成root,但是执行useradd命令添加user3用户
#只是借root身份执行一下useradd命令，useradd命令只能管理员使用
```

```
# env 查看当前环境变量
```
如果从超级用户切换为普通用户不需要输入密码。

## 7.4 用户组管理命令

- 添加用户组

```
# groupadd [选项] 组名
选项：
    -g GID: 指定组ID
```
- 修改用户组

```
# groupmod [选项] 组名
选项：
    -g GID: 修改组ID
    -n 新组名：修改组名
# groupmod -n testgrp group1
#把组名group1修改为testgrp
```
- 删除用户组

```
# groupdel 组名
```
如果组内有初始用户，不能删除，如果都是附加用户，可以删除
添加用户时如果指定用户组 使用-g 指定用户组的话，不会生成与用户相同的用户组
如果使用-G指定附加组的话，还是会生成与用户相同名的用户组

- 把用户添加入组或从组中删除

```
# gpasswd 选项 组名
选项：
    -a 用户名： 把用户加入组
    -d 用户名： 把用户从组中删除
# gpasswd 命令是将用户以附加用户的形式加入到组中，可查看/etc/group文件 ，可以看到的都是附加用户。
```
# 八、 权限管理
## 8.1 ACL权限
access control list 访问控制表
### 8.1.1 ACL权限简介与开启
-  ACL权限简介
-  查看分区 ACL权限是否开启

```
[root@localhost~]# dumpe2fs -h /dev/sda3
#dumpe2fs命令是查询指定分区详细文件系统信息的命令
选项：
    -h 仅显示超级块中信息，而不显示磁盘块组的详细信息 
```


```
[root@localhost~]# df -h 
#查看系统有哪些分区？
```

- 临时开户分区ACL权限 

```
[root@localhost~]# mount -o remount,acl /
#重新挂载根分区，并挂载加入acl权限 
```
- 永久开户分区ACL权限

```
[root@localhost~]# vi /etc/fstab
UUID=c2ca6f57-b15c-43ea-bca0-f239083d8bd2 / ext4 defaults,acl 1 1 
#加入“acl”
# 此文件系统每次启动时会执行此文件，挂载分区

[root@localhost~]# mount -o remount /
#重新挂载文件系统或重启动系统，使修改生效

```

### 8.1.2 查看与设定ACL权限
- 查看ACL命令

```
[root@localhost~]# getfacl 文件名
#查看acl权限
```
- 设定ACL权限的命令

```
[root@localhost~]# setfacl 选项 文件名
选项：
    -m : 设定ACL权限
    -x : 删除指定的ACL权限 
    -b : 删除所有的ACL权限 
    -d ：设定默认的ACL权限 
    -k ：删除默认ACL权限 
    -R : 递归设定ACL权限 
```

- 给用户设定ACL权限 


```
[root@bogon ~]# mkdir /project
#添加目录project
[root@bogon ~]# useradd bimm
#添加用户bimm
[root@bogon ~]# useradd cangls
#添加用户cangls
[root@bogon ~]# groupadd tgroup
#添加用户组tgroup
[root@bogon ~]# gpasswd -a bimm tgroup
Adding user bimm to group tgroup
#将用户bimm添加到用户组tgroup
[root@bogon ~]# gpasswd -a cangls tgroup
Adding user cangls to group tgroup
#将用户cangls添加到用户组tgroup
[root@bogon ~]# cat /etc/group
......
......
bimm:x:502:
cangls:x:503:
tgroup:x:504:bimm,cangls
#要看group文件 ，可看到bimm,cangls已经添加到group用户组了
[root@bogon ~]# chown root:tgroup /project/
#修改/project/文件 所有者和所属组
[root@bogon ~]# chmod 770 /project/
#修改/project/目录的访问权限
[root@bogon ~]# ll -d /project/
drwxrwx--- 2 root tgroup 4096 5月  14 08:16 /project/
#查看/project/目录的权限


```

```
[root@bogon ~]# useradd st
#添加一个特殊用户
[root@bogon ~]# setfacl -m u:st:rx /project/
#给用户st赋予r-x权限 ，使用"u:用户名:权限"格式

```
- 给用户组设定ACL权限


```
[root@bogon ~]# groupadd tgroup2
#添加一个用户组
[root@bogon ~]# setfacl -m g:tgroup2:rwx /project/
#给用户组tgroup2赋予ACL权限 ，使用"g:组名:权限"格式
```



### 8.1.3 最大有效权限与删除ACL权限

- 最大有效权限mask
    - mask是用来指定最大有效权限的。如果我给用户赋予了ACL权限，是需要和mask的权限“相与”才能得到用户的真正权限。

| A    | B    | and  |
| ---- | ---- | ---- |
| r    | r    | r    |
| r    | -    | -    |
| -    | r    | -    |
| -    | -    | -    |

用户和mask“相与” 得到最大有效权限

- 修改最大有效权限

```
[root@bogon ~]# setfacl -m m:rx 文件名
#设定mask权限为r-x. 使用“m:权限”格式
```


```
[root@bogon ~]# setfacl -m m:rx /project/
```



```
[root@bogon ~]# setfacl -m m:rx /project/
[root@bogon ~]# getfacl /project/
getfacl: Removing leading '/' from absolute path names
# file: project/
# owner: root
# group: tgroup
user::rwx
user:st:r-x
group::rwx			#effective:r-x
mask::r-x
other::---
# 从以上例子中可以看出，mask最大权限为rx：
假如给了用户rwx或组rwx，但其实最大权限还是rx
```

- 删除ACL权限


```
[root@localhost~]# setfacl -x u:用户名 文件名
#删除指定用户的ACL权限
```


```
[root@localhost~]# setfacl -x g:组名 文件名
#删除指定用户组的ACL权限
```
```
[root@localhost~]# setfacl -b 文件名
#删除文件的所有的ACL权限
```

### 8.1.4 默认ACL权限和递归ACL权限

- 递归ACL权限（对现有文件）
    - 递归是父目录在设定ACL权限时，所有的子文件和子目录也会拥有相同的ACL权限。


```
[root@localhost~]# setfacl -m u:用户名:权限 -R 目录名（必须是目录，不能是文件 ，否则会报错）
```

- 默认ACL权限（对未来文件）
    - 默认ACL权限的作用是如果给父目录设定了默认ACL权限，那么父目录中所有新建的子文件都会继承父目录的ACL权限。


```
setfacl -m d:u:用户名:权限 目录名
```


## 8.2 文件特殊权限
### 8.2.1 SetUID
- SetUID的功能
    - 只有可以执行的二进制程序才能设定SUID权限
    - 命令执行者要对该程序拥有x(执行)权限 
    - 命令执行者在执行该程序时获得该程序文件属主的身份（在执行程序的过程中灵魂附体为文件的属主）
    - SetUID权限只在该程序执行过程中有效，也就是说身份改变只在程序执行过程中有效
    - passwd命令拥有SetUID权限，所以普通用户可以修改自己的命令

```
[root@localhost~]# ll /usr/bin/passwd
-rwsr-xr-x. 1 root root 25980 2月 22 2012 /usr/bin/passwd
```



- 
    - cat命令没有SetUID权限，所以普通用户不能查看/etc/shadow文件内容


```
[root@localhost~]# ll /bin/cat
-rwxr-xr-x 1 root root 47976 6月 22 2012 /bin/cat
```
- 设定SetUID的方法
    -  4代表 SUID
        - chmod 4755 文件名
        - chmod u+s 文件名

```
[root@bogon ~]# ll abc
-rw-r--r-- 1 root root 0 5月  22 06:35 abc
[root@bogon ~]# chmod 4755 abc
[root@bogon ~]# ll abc
-rwsr-xr-x 1 root root 0 5月  22 06:35 abc

```

- 取消SetUID的方法
    - chmod 755 文件名
    - chmod u-s 文件名

- 危险的SetUID
    - 关键目录应严格控制写权限。比如“/”、 “/usr” “/etc”、 “/lib” 等
    - 用户的密码设置要严格遵守密码三原则
    - 对系统中默认应该具有SetUID权限的文件作一列表，定时检查有没有这之外的文件被设置了SetUID权限 

注意：如果是大S则不能使用的。

### 8.2.2 SetGID

- SetGID针对文件的作用
    - 只有可执行的二进制程序才能设置SGID权限
    - 命令执行者要对该程序拥有x(执行)权限
    - 命令执行者在执行程序的时候，组身份升级为该程序文件的属组
    - SetGID权限同样只在该程序执行过程中有效，也就是说组身份改变只在程序执行过程中有效


```
例：
[root@localhost~]# ll /usr/bin/locate
-rwx--s--x 1 root slocate 35612 8月 24 2010 /usr/bin/locate

[root@localhost~]# ll /var/lib/mlocate/mlocate.db
-rw-r----- 1 root slocate 1838850 1月 20 04:29 /var/lib/mlocate/mlocate.db
```

```
- /usr/bin/locate是可执行二进制程序， 可以赋予SGID
- 执行用户lamp对/usr/bin/locate命令拥有执行权限
- 执行/usr/bin/locate命令时，组身份会升级为slocate组，而slocate组对/var/lib/mlocate/mlocate.db数据库拥有r权限，所以普通用户可以使用locate命令查询mlocate.db数据库
- 命令结束，lamp用户的组身份返回为lamp组
```
- SetGID针对目录的作用
    - 普通用户必须对此目录拥有r和x权限，才能进入此目录
    - 普通用户在此目录中的有效组会变成此目录的属组
    - 若普通用户对此目录拥有w权限时，新建的文件的默认属组是这个目录的属组

- 设定SetGID
    - 2代表SGID
        - chmod 2755 文件名
        - chmod g+s  文件名


```
[root@localhost~]# cd /tmp/
[root@localhost tmp]# mkdir test
[root@localhost tmp]# chmod g+s test
[root@localhost tmp]# ll -d test/
[root@localhost tmp]# chmod 777 test/
[root@localhost tmp]# su - lamp
[lamp@localhost~]$ cd /tmp/test/
[lamp@localhost test]$ touch abc
[lamp@localhost test]$ ll
```


- 取消SetGID
    - chmod 755 文件名
    - chmod g-s 文件名

        

### 8.2.3 Sticky BIT

- SBIT粘着位作用
    - 粘着位目前只对目录有效
    - 普通用户对该目录拥有w和x权限，即普通用户可以在此目录拥有写入权限
    - 如果没有粘着位，因为普通用户拥有w权限，所以可以删除此目录下所有文件，包括其他用户建立的文件。一但赋予了粘着位，除了root可以删除所有文件 ，普通用户就算拥有w权限 ，也只能删除自己建立的文件，但是不能删除其他用户建立的文件


```
[root@localhost~]# ll -d /tmp/
drwxrwxrwt. 3 root root 4096 12月 13 11:22 /tmp/
```
- 设置与取消粘着位
    - 设置粘着位
        - chmod 1755 目录名
        - chmod o+t 目录名
    - 取消粘着位
        - chmod 777 目录名
        - chmod o-t 目录名

## 8.3 文件系统属性chattr权限

- chattr命令格式

```
[root@localhost~]# chattr [+-=] [选项] 文件或目录名
+： 增加权限
-： 删除权限
=:  等于某权限
选项：
    - i: 如果对文件设置i属性，那么不允许对文件进行删除、改名，也不能添加和修改数据；如果对目录设置i属性，那么只能修改目录下文件的数据，但不允许建立和删除文件。
    - a: 如果对文件设置a属性, 那么只能在文件中增加数据，但是不能删除也不能修改数据；如果对目录设置a属性，那么只允许在目录中建立和修改文件，但是不允许删除。
```
- 查看文件系统属性


```
[root@localhost~]# lsattr 选项 文件名
选项：
    -a : 显示所有文件和目录
    -d : 若目标是目录，仅列出目录本身的属性，而不是子文件的
```





## 8.4 系统命令sudo权限

- sudo权限
    - root把本来只能超级用户执行的命令赋予普通用户执行。
    - suto的操作对象是系统命令

- sudo使用


```
[root@localhost~]# visudo
#实际修改的是/etc/sudoers文件

root      ALL=(ALL)  ALL
#用户名   被管理主机的地址=（可使用的身份） 授权命令（绝对路径）

# %wheel    ALL=(ALL)  ALL
#%组名      被管理主机的地址=（可使用的身份） 授权命令（绝对路径）
```

- 授权sc用户可以重启服务器


```
[root@localhost~]# visudo

sc ALL=/sbin/shutdown -r now

ALL： 代表本机，或者填写本机IP地址
```
- 普通用户执行sudo赋予的命令


```
[root@localhost~]# su - sc
[sc@localhost~]$ sudo -l
# 查看可用的sudo命令

[sc@localhost~]$ sudo /sbin/shutdown -r now
#普通用户执行sudo赋予的命令
```

# 九、文件系统管理

## 9.1 回顾分区和文件系统
- 分区类型
    - 主分区：总共最多只能分四个
    - 扩展分区：只能有一个，也算作主分区的一种，也就是说主分区加扩展分区最多有四个。但是扩展分区不能存储数据和格式化，必须再划分成逻辑分区才能使用。
    - 逻辑分区：逻辑分区是在扩展分区中划分的，如果是IDE硬盘，Linux最多支持59个逻辑分区，如果是SCSI硬盘Linux最多支持11个逻辑分区
- 分区表示方法

sda：代表SCSI硬盘接口
hda: 代表IDE硬盘接口
分区的设备文件名
| 分区      | 表示方法  |
| --------- | --------- |
| 主分区1   | /dev/sda1 |
| 主分区2   | /dev/sda2 |
| 主分区3   | /dev/sda3 |
| 扩展分区  | /dev/sda4 |
| 逻辑分区1 | /dev/sda5 |
| 逻辑分区2 | /dev/sda6 |
| 逻辑分区3 | /dev/sda7 |

| 分区      | 表示方法  |
| --------- | --------- |
| 主分区1   | /dev/sda1 |
| 扩展分区  | /dev/sda2 |
| 逻辑分区1 | /dev/sda5 |
| 逻辑分区2 | /dev/sda6 |
| 逻辑分区3 | /dev/sda7 |

/sda1 /sda2 /sda3 /sda4 只能由主分区使用


- 文件系统
    - ext2:是ext文件系统的升级版本，RedHat Linux7.2版本以前的系统默认都是ext2文件系统。1993年发布，最大支持16TB的分区和最大2TB的文件（1TB=1024GB=1024*1024kb）
    - ext3: ext3文件系统是ext2文件系统的升级版本，最大的区别就是带日志功能，以在系统突然停止时提高文件系统的可靠性。支持最大16TB的分区和最大2TB的文
      件。
    - ext4: 它是ext3文件系统的升级版。ext4在性能、伸缩性和可靠性方面进行了大量改进。EXT4的变化可以说是翻天覆地的，比如向下兼容EXT3、最大1EB文件系统和16TB文件、多块分配、延迟分配、持久预分配、快速FSCK、日志校验、无日志模式、在线碎片整理、inode增强、默认启用barrier等。是CentOS6.3的默认文件系统（1EB=1024PB=1024*1024TB）


## 9.2 文件系统常用命令

### 9.2.1 df命令、du命令、fack命令和dump2fs命令

- 文件系统查看命令df

```
[root@localhost~]# df [选项] [挂载点]
选项：
    -a 显示所有的文件系统信息，包括特殊文件系统，如/proc、/sysfs
    -h 使用习惯单位显示容量，如KB, MB或GB等
    -T 显示文件系统类型
    -m 以MB为单位显示容量
    -k 以KB为单位显示容量。默认就是以KB为单位
```
- 统计目录或文件大小du

```
[root@localhost~]# du [选项] [目录或文件名]
选项：
    -a 显示每个子文件的磁盘占用量。默认只统计子目录的磁盘占用量
    -h 使用习惯单位显示磁盘占用量，如KB, MB或GB等
    -s 统计总占用量，而不列出子目录和子文件的占用量
```
- du命令和df命令的区别
    - df命令是从文件系统考虑的，不光要考虑文件占用的空间，还要统计被命令或程序占用的空间（最常见的就是文件已经删除，但是程序并没有释放空间）
    - du命令是面向文件的，只会计算文件或目录占用的空间

- 文件系统修复命令fsck (知道就行，一般不用，有时反而会造成系统异常)
```
[root@localhost~]# fsck [选项] 分区设备文件名
选项：
    -a: 不用显示用户提示，自动修复文件系统
    -y: 自动修复。 和-a作用一致，不过有些文件系统只支持-y
```

- 显示磁盘状态命令dumpe2fs
```
[root@localhost~]# dumpe2fs 分区设备文件名
```


### 9.2.2 挂载命令

- 查询与自动挂载
```
[root@localhost~]# mount [-l]
#查询系统中已经挂载的设备 -l会显示卷标名称

[root@localhost~]# mount -a
#依据配置文件 /etc/fstab的内容，自动挂载
#硬盘其实就是每次开机时依据这个文件进行自动挂载的，
#移动硬盘，光盘，U盘，最好不要进行自动挂载 ，因为每次开机的时候，不能保证都插入了光盘，U盘等，这样系统一开机就会崩溃。


[root@bogon etc]# mount 
#直接回车
/dev/sda5 on / type ext4 (rw)
proc on /proc type proc (rw)
#内存
sysfs on /sys type sysfs (rw)
#内存
devpts on /dev/pts type devpts (rw,gid=5,mode=620)
tmpfs on /dev/shm type tmpfs (rw)
/dev/sda1 on /boot type ext4 (rw)
/dev/sda2 on /home type ext4 (rw)
none on /proc/sys/fs/binfmt_misc type binfmt_misc (rw)
```

- 挂载命令的格式

```
[root@localhost~]# mount [-t 文件系统] [-L 卷标名] [-o 特殊选项] 设备文件名 挂载点
选项：
    -t 文件系统： 加入文件系统类型来指定挂载的类型，可以ext3、ext4、iso9660等文件系统：如果挂载的是硬盘、是分区默认的文件系统是ext4，如果挂载的是光盘默认文件系统是iso9660
    -L 卷标名：挂载指定卷标的分区,而不是安装设备文件名挂载
    -o 特殊选项：可以指定挂载的额外选项
```

特殊选项
| 参数          | 说明                                                         |
| ------------- | ------------------------------------------------------------ |
| atime/noatime | 更新访问时间/不更新访问时间。访问分区文件时，是否更新文件的访问时间，默认为更新 |
| async/sync    | 异步/同步，默认为异步                                        |
| auto/noauto   | 自动/手动，mount -a命令执行时，是否会自动按照/etc/fstab文件内容挂载，默认为自动 |
| defaults      | 定义默认值，相当于rw,suid,dev,exec,auto,nouser,async这七个选项 |
| exec/noexec   | 执行/不执行，设定是否允许在文件系统中执行可执行文件，默认exec允许 |
| remount       | 重新挂载已经挂载的文件系统，一般用于指定修改特殊权限         |
| rw/ro         | 读写/只读 , 文件系统挂载时，是否具有读写权限 ，默认是rw      |
| suid/nosuid   | 具有/不具有SUID权限，设定文件系统是否具有SUID和SGID的权限，默认是具有 |
| user/nouser   | 允许/不允许普通用户挂载，设定文件系统是否允许普通用户挂载，默认是不允许，只有root可以挂载分区 |
| usrquota      | 写入代表文件系统支持用户磁盘配额，默认不支持                 |
| grpquota      | 写入代表文件系统支持组磁盘配额，默认不支持                   |


```
[root@localhost~]# mount -o remount,noexec /home
#重新挂载/boot分区，并使用noexec权限
[root@localhost~]# cd /home
[root@localhost home]# vi hello.sh
#编写一个简单的hello.sh文件
[root@localhost home]# chmod 755 hello.sh
[root@localhost home]# ./hello.sh
[root@localhost home]# mount -o remount,exec /home
#记得改回来啊，要不会影响系统启动的


```


### 9.2.3 挂载光盘与U盘

1. 挂载光盘

```
[root@localhost~]# mkdir /mnt/cdrom/
#建立挂载点

[root@localhost~]# mount -t iso9660 /dev/cdrom /mnt/cdrom/
#挂载光盘

[root@localhost~]# mount /dev/sr0 /mnt/cdrom
```
> cdrom是 sr0的软链接
> 如果有多个光盘则是cdrom1 或sr1

2. 卸载光盘


```
[root@localhost~]# umount 设备文件名或挂载点

[root@localhost~]# umount /mnt/cdrom
```

3. 挂载U盘


```
[root@localhost~]# fdisk -l
#查看U盘设备文件名

[root@localhost~]# mount -t vfat /dev/sdb1 /mnt/usb/
```
> **注意：Linux默认是不支持NTFS文件系统的**
> 系统将fat16识别为fat 将fat32识别为vfat

### 9.2.4 支持NTFS文件系统

1. 下载NTFS-3Gc插件

http://www.tuxera.com/community/ntfs-3g-download/

2. 安装NTFS-3G

```
[root@localhost~]# tar -zxvf ntfs-3g_ntfsprogs-2013.1.13.tgz
#解压
[root@localhost~]# cd ntfs-3g_ntfsprogs-2013.1.13
#进入解压目录
[root@localhost ntfs-3g_ntfsprogs-2013.1.13]# ./configure
#编译器准备。没有指定安装目录，安装到默认位置中
[root@localhost~]# make
#编译
[root@localhost~]# make install
#编译安装
```
3. 使用
```
[root@localhost~]# mount -t ntfs-3g 分区设备文件名 挂载点
```



## 9.3 fdisk分区

### 9.3.1 fdisk命令分区过程

1. 添加硬盘
2. 查看新硬盘


```
[root@localhost~]# fdisk -l
```
3. 使用fdisk命令分区

```
[root@localhost~]# fdisk /dev/sdb
```
> fdisk/sdb 后面不带任何数字

**fdisk交互指令说明**
| 命令 | 说明                                                        |
| ---- | ----------------------------------------------------------- |
| a    | 设置可引导标记                                              |
| b    | 编辑bsd磁盘标签                                             |
| c    | 设置DOS操作系统兼容标记                                     |
| d    | 删除一个分区                                                |
| l    | 显示已知的文件系统类型。82为Linux swap分区，83为Linux分区 m |
| n    | 新建分区                                                    |
| o    | 建立空白DOS分区表                                           |
| p    | 显示分区列表                                                |
| q    | 不保存退出                                                  |
| s    | 新建空白SUN磁盘标签                                         |
| t    | 改变一个分区的系统ID                                        |
| u    | 改变显示记录单位                                            |
| v    | 验证分区表                                                  |
| w    | 保存退出                                                    |
| x    | 附加功能（仅专家）                                          |

4. 重新读取分区表信息


```
[root@localhost~]# partprobe
```
5. 格式化分区


```
[root@localhost~]# mkfs -t ext4 /dev/sdb1
```

```
[root@bogon ~]# fdisk -l

Disk /dev/sda: 21.5 GB, 21474836480 bytes
255 heads, 63 sectors/track, 2610 cylinders
Units = cylinders of 16065 * 512 = 8225280 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk identifier: 0x000e01dc

   Device Boot      Start         End      Blocks   Id  System
/dev/sda1   *           1          26      204800   83  Linux
Partition 1 does not end on cylinder boundary.
/dev/sda2              26         281     2048000   83  Linux
Partition 2 does not end on cylinder boundary.
/dev/sda3             281         409     1024000   82  Linux swap / Solaris
Partition 3 does not end on cylinder boundary.
/dev/sda4             409        2611    17693696    5  Extended
/dev/sda5             409        2611    17692672   83  Linux

Disk /dev/sdb: 10.7 GB, 10737418240 bytes
255 heads, 63 sectors/track, 1305 cylinders
Units = cylinders of 16065 * 512 = 8225280 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk identifier: 0xbf9e4b6c

   Device Boot      Start         End      Blocks   Id  System
/dev/sdb1               1         262     2104483+  83  Linux
/dev/sdb2             263        1305     8377897+   5  Extended
#注意：扩展分区不能格式化和写入数据
/dev/sdb5             263         524     2104483+  83  Linux

```
6. 创建目录并挂载分区
```
[root@bogon ~]# mkdir /disk1
[root@bogon ~]# mkdir /disk5
[root@bogon ~]# mount /dev/sdb1 /disk1/
[root@bogon ~]# mount /dev/sdb5 /disk5/

```
7. 查看已挂载分区
```
[root@bogon ~]# df 
或
[root@bogon ~]# mount 
```

### 9.3.2 分区自动挂载与fstab文件修复

1. /etc/fstab文件
- 第一字段：分区设备文件名或UUID（硬盘通用唯一识别码）

```
[root@localhost~]# dumpe2fs -h /dev/sdb1
#查看UUID
```

- 第二字段：挂载点
- 第三字段：文件系统名称
- 第四字段：挂载参数（挂载权限：可参考前面的mount）
- 第五字段：指定分区是否被dump备份，0代表不备份，1代表每天备份，2代表不定期备份

```
[root@localhost~]# cd /
[root@localhost~]# ls
bin     demo   disk5  lib         media  net   project  selinux  temp  usr
boot    dev    etc    lib64       misc   opt   root     srv      test  var
cgroup  disk1  home   lost+found  mnt    proc  sbin     sys      tmp
#其中的 lost+found 就是备份的信息（只有分区才有一份）
```

- 第六字段：指定分区是否被fsck检测，0代表不检测，其他数字代表检测的优先级，那么当然1的优先经比2高

2. 分区自动挂载

```
[root@localhost~]# vi /etc/fstab
...省略部分输出...
/dev/sdb1 /disk1   ext4 defaults 1  2
```

```
[root@localhost~]# mount -a
#设置完自动挂载 并在系统重启之前先执行此命令
#依据配置文件/etc/fstab的内容，自动挂载
```
3. /etc/fstab文件修复

此修复方式不是万能的，因为此方式只能修复/etc/fstab文件错误导致的原因
```
[root@localhost~]# mount -o remount,rw /
#当/etc/fstab文件写错，重启后报错，虽然经过输入root密码进入了系统，但是修改不了/etc/fstab文件，因为报错，挂载分区时挂载为了只读权限
#重新将分区挂载为读写权限可修复报错
```


## 9.4 分配swap分区

1. free命令


```
[root@localhost~]# free [选项]
选项：
    -m : 以单位兆（M）显示
#查看内存与swap分区使用状态

```
- cached(缓存)：是指把读取出来的数据保存在内存当中，当再次读取时，不用读取硬盘而而直接从内存当中读取，加速了数据了读取过程
- buffer(缓冲)：是指在写入数据时，先把分散的写入操作保存到内存当中，当达到一定程度再集中写入硬盘，减少了磁盘碎片和硬盘的反复寻道，加速了数据的写入过程

2. 新建swap分区

```
[root@localhost~]# fdisk /dev/sdb

#别忘记把分区ID改为82



```

格式化之前别忘记重新读取分区表信息，如果不行则需重启系统

```
[root@localhost~]# partprobe
```


3. 格式化


```
[root@localhost~]# mkswap /dev/sdb6
#/dev/sdb6是刚分出来的区
```
4. 加入swap分区



```
[root@localhost~]# swapon  /dev/sdb6
#加入swap分区
```
```
[root@localhost~]# swapoff  /dev/sdb6
#取消swap分区
```
5. swap分区开机自动挂载


```
[root@localhost~]# vi /etc/fstab
/dev/sdb6   swap    swap    defaults    0  0
```


```
[root@localhost~]# mount -a
#执行重新挂载所有分区
#如果不报错，则说明配置正确
```

# 十、Shell基础

## 10.1 Shell概述

1.  Shell是什么

- Shell是一个命令行解释器，它为用户提供了一个向Linux内核发送请求以便运行程序的界面系统级程序，用户可以用Shell来启动、挂起、停止甚至是编写一些程序。



## 10.2 Shell脚本的执行方式
## 10.3 Bash的基本功能
## 10.4 Bash的变量
## 10.5 Bash的运算符
## 10.6 环境变量配置文件
```

[root@localhost~]#
[root@localhost~]#
[root@localhost~]#
[root@localhost~]#
[root@localhost~]#


```