## Linux

#### yum

```shell
#1.安装操作
yum install PACKAGE			#安装某个包
#例：yum install httpd

yum groupinstall GROUP		 #安装某个软件组
#例：yum groupinstall "KDE"	# 安装KDE桌面

#2.升级操作
yum update				#更新系统中所有需要更新的包
yum update PACKAGE  	#更新某个包
#例：yum update httpd

yum groupupdate GROUP	#更新某个软件组
#例：yum groupupdate "KDE" #升级KDE桌面

yum check-update 		#检查当前系统中需要更新的包

#3.查找操作
yum list 			#显示软件源中所有可用的包（一般不用）
yum list installed 	#显示系统中已经安装过的包
yum info PACKAGE	#显示某个包的信息
#例：yum info httpd

yum groupinfo GROUP			#显示某个软件组的信息
#例：yum groupinfo "KDE"		#显示KED桌面软件信息
yum grouplist				#显示软件源宏所有的可用软件组

#4.删除操作
yum remove PACKAGE			#删除某个包
#例：yum remove httpd
yum groupremove GROUP		#删除某个软件组
#例：yum groupremove "KDE"   #删除KDE桌面

#5.清除操作
yum clean					#清楚使用yum所生成的缓存文件


# 例:
yum install -y lrzsz
sz index.html		# 发送文件到本地
rz					# 上传本地文件到服务器
```



#### 日期与日历

```shell
date			# 显示当前日期
cal				# 
```

#### 系统信息

```shell
locale				# 查看linux编码格式
locale -a 			# 查看当前系统支持的字符集
lsb_release -a		# 显示系统信息
```





**提示：执行以下命令的用户必须在** **/etc/sudoers** **中**

\# sudo -i			//可以频繁执行某些只有root用户才能执行的命令，而不用每次输入密码,				   无时间限制，exit退出

\# sudo  ls 	//暂时切换到root模式以执行ls命令（暂时拥有root权限）

\# sudo passwd 		 // 更改或设置root密码（刚安装的Linux系统没有设置root用户密码）

\# sudo passwd user1 	//更改user1的密码





#### 管理用户

1. 创建用户

    > Linux用户按照使用方式分为三种：根用户、系统用户、普通用户。普通用户是没有添加用户的权限的，只有root用户才能创建用户

    ```shell
    useradd liqiju			# 创建用户（仅限root用户）
    
     -c	<备注> 　				# 设置用户说明
    
     -d	<登入目录> 　			# 指定用户家目录
    
     -e	<有效期限> 　		# 指定帐号的有效期限
    
     -f	<缓冲天数> 　		# 指定在密码过期后多少天即关闭该帐号
    
     -g	<群组> 　				# 指定用户所属的群组
    
     -G	<群组> 　				# 指定用户所属的附加群组
    
     -s	<shell>　 　			# 指定用户登入后所使用的shell
    
     -u	<uid> 　				# 指定用户UID
     
     # 例：
     useradd  -u	1000  user1
     
    # 
    whoami		    //显示自身用户名称
    su					//切换到root用户
    su user1		//切换到user1用户
    su -			//切换到root用户并到进入家目录
    ```

    > 系统创建用户的过程：

    1. 系统需要将用户信息记录在/etc/passwd中，一般会在/etc/passwd和/etc/shadow末尾追加一条记录，同时会分配给该用户一个UID
    2. 为该用户在home文件夹自动创建家目录
    3. 复制/etc/skel下所有的文件至/home/john
    4. 新建一个与该用户名一样的用户组，也就是说当创建用户john的时候，也同时创建了一个叫john的用户组，而用户john默认属于john用户组

2. 删除用户

    > userdel不允许你移除正在线上的使用者帐号。你必须kill此帐号现在在系统上执行的程序才能进行帐号删除

    ```shell
    userdel -r liqiju	# 彻底删除用户
    ```

    > 彻底删除过程：

    1. 删除/etc/passwd ，/etc/shadow  中的内容
    2. 删除 /etc/group  ，/etc/gshadow  中的内容
    3. 删除家目录，/var/spool/mail/用户名 中的内容
    4. 删除该用户创建的文件（find查找后删除）

3. 修改密码

    ```shell
    passwd liqiju		# 设置或更改用户密码（仅限root用户）
    passwd				# 设置或更改密码（普通用户）
    ```

4. 修改用户

    > fwef

    ```shell
    # usermod 					//修改用户
    
     -c	<备注> 　		//修改用户帐号的备注文字
    
     -d	<家目录> 　		//修改用户登入时的目录
    
     -e	<有效期限> 　		//修改帐号的有效期限
    
     -f	<缓冲天数> 　		//修改在密码过期后多少天即关闭该帐号
    
     -g	<群组> 　		//修改用户所属的群组
    
     -G	<群组> 　		//修改用户所属的附加群组
    
     -l	<账号名> 　		//修改用户帐号名称
    
     -L 　	<账号名>			//锁定用户密码，使密码无效（root用户例外）
    
     -s	<shell> 　		//修改用户登入后所使用的shell
    
     -u	<uid> 　			//修改用户UID
    
     -U 　<账号名>			//解除密码锁定
    ```

5. 新增和删除用户组

    > fwef

    ```shell
    groupadd [-g 1001]  liqiju			# 创建组[制定GID]
    groupdel  liqiju					# 删除组
    groupmod
    ```

    



#### 进程管理

\# top			//实时显示 process 的动态



\# ps aux  	//显示目前系统运行的进程

\# who 		    //查看目前登录在系统中的所有用户

\# kill  -l  		//查看具体的信号代码

\# kill  -1  PID 		//重启进程(原地重启或者说“软重启”，不会改变主进程的PID)

\# kill  -9  PID 		//强行杀掉进程

\# kill  -15  PID   //正常结束进程

\# killall  进程名	//简单而且安全



***\*Linux netstat命令用于显示网络状态\****

\# netstat  -ntlp 	//

***\*进程优先级调整\****

 优先级默认为0 ，数值越低优先级越高

 nice命令仅限于在启动一个进程的时候同时赋予其nice优先级

 对于已经启动的进程，可以用renice命令进行修改，不过，这需要先查询出该进程的PID



***\*将进程转到后台运行but xshell断开连接后失效：\****

\# jobs 		//查看任务，返回任务编号n和进程号PID

\# bg %n 	//将编号为n的任务转后台运行

\# fg %n 	//将编号为n的任务转前台运行

\# ctrl+z 	//挂起当前任务

\# ctrl+c   //结束当前任务

***\*将进程转到后台运行但xshell断开连接后无影响：\****

\# nohup python app.py &		// no hung up

***\*python\****

\# nohup gunicorn -w 4 -b 127.0.0.1:5001 运行文件名称:Flask程序实例名 &

\# pstree -ap | grep gunicorn      //查询gunicorn的进程树以关闭gunicorn相关服务



### 文件操作

#### 1. 目录的权限解析

> rwx

- r

    具有读取目录结构列表的权限，可以查看目录下有那些文件

- w

    1. 可以在该目录下**新建**文件或目录
    2. **删除**文件或目录
    3. **重命名**文件或目录
    4. **移动**该目录内文件或目录的位置

- x

    是否可以进入该目录



#### 2. 查看文件内容

- cat

    ```shell
    \# cat  -b 文件名（不显示空行）
    
    \# cat  -n 文件名（显示行号）
    ```

    

- more

    ```shell
    \# more  文件名        //分页显示
    空格       //向下翻一页
    Enter      //向下翻一行
    /字符串    //搜索
    :f         //立刻显示文件名和行数
    b 			//向上翻一页
    q			//退出
    ```

    



***\*压缩与解压\****

***文件查找***

\# find  PATH-name  FILENAME

\# find  /etc  -name  httpd.conf			//从etc目录查找httpd.conf文件

\# find  /  -name  *.conf				//找出系统中所有以.conf结尾的文件

\# find  /  -name  httpd*				//以httpd开头的文件：



#### 文件类型

> drwxrwxr--
>
> -rwxrwxxr--

- d			目录
- l              链接文件
- b             块文件
- c             字符文件
- s              socket文件
- \-              普通文件

 -		p             管道文件

#### 文件操作

```shell
touch index.html		# 创建index.html文件
rm index.html			# 删除index.html文件
rm -f index.html		# 强制删除index.html文件
du -h 文件/目录			 # 查看文件大小
rm -fr /*				# 强制删除根目录所有文件

#
mkdir www				# 创建www目录
rm -r www				# 删除www目录

```



\# du -h 文件/目录 		//查看大小

\# mkdir stu			//创建目录stu

\# rm -r  directory		//删除目录

\# rm -fr directory        //强制删除目录

\# cd ~       		//进入家目录

\# cd ..				//回到上级目录

\# cd - 				//回到之前的目录

\# cd ../..				//跳到目前目录的上上层

\# cd  /				//回到根目录

\# cd /etc/profile.d       //跳到 etc/profile.d目录

\# pwd 				//显示当前所在路径

\# ll 					//显示目录文件详细信息

\# cp -ar test1 test2  	 //-r 复制文件和目录 -a保留属性

\# cp  hello.sh  file.sh	//复制并重命名文件

\# mv				//移动或重命名

\#stat  world.txt			//显示文件或文档的详细信息

***\*改变文件所属组：\****

\# chgrp  liqiju  hello.txt		//将文件hello.txt修改用户组为liqiju

\# chgrp  -R  liqiju  hello.dir	//

***\*改变文件拥有者：\****

\# chown  liqiju  hello.txt			//将文件hello.txt拥有者更改为 liqiju

\# chown  :liqiju  hello.txt 		//将文件hello.txt的所属组更改为 liqiju

\# chown  liqiju:liqiju  hello.txt 		//同时更改

\# chown  -R  liqiju:liqiju  hello      //

***\*使用grep搜索文本：\****

\# grep  [-ivnc]  '需要匹配的字符'  文件名

 -i			//不区分大小写

 -v			//反向匹配

 -n			//输出行号

 -c			//统计包含匹配的行数

***\*文件的隐藏属性：\****

Linux下的文件还有一些隐藏属性，必须使用lsattr来显示，默认情况下，文件的隐藏属性都是没有设置的。

拥有a属性的文件只能在尾部增加数据而不能被删除(即使是root也不行)

还有一种比较常用的属性是i属性。设置了这种属性的文件将无法写入、改名、删除，即便是root用户也不行。这种属性常用于设置在系统或者关键服务中的配置文件，这对提升系统安全性有较大的帮助。

\# lsattr  [hello.txt]		//查看当前目录中文件的隐藏属性

\# chattr  +a  hello.txt	//只能在尾部增加数据而不能被删除

\# chattr  -a  hello.txt	//

\# chattr +i filename 	//

\# chattr -i filename 		//解除chattr限制

***\*更改文件权限：\****

\# chmod	 u+x  hello.txt		//为hello.txt文件的所有者添加x权限

\# chmod  744  hello.txt		//同上

![img](file:///C:\Users\hollow\AppData\Local\Temp\ksohtml7220\wps7.jpg) 

***\*文件特殊属性：SUID／SGID/Sticky\****

![img](file:///C:\Users\hollow\AppData\Local\Temp\ksohtml7220\wps8.jpg) 

/usr/bin/passwd的权限，发现有个特别的s权限在用户权限上，这就是奥秘所在—该命令是设置了SUID权限的，这意味着普通用户可以使用root的身份来执行这个命令。那么以上的疑问就很容易解释了。但是必须注意的是，SUID权限只能用于二进制文件。

\# chmod  u+s  filename			//给一个二进制文件添加SUID权限的方法

如果某个二进制文件的用户组权限被设置了s权限，则该文件的用户组中所有的用户将都能以该文件的用户身份去运行这个命令。

\# chmod  g+s  filename 			//

Sticky权限只能用于设置在目录上，设置了这种权限的目录，任何用户都可以在该目录中创建或修改文件，但是只有该文件的创建者和root可以删除自己的文件。

\# chmod  o+t  dirname			//给dirname目录添加一个t权限

***\*默认权限和umask：\****

![img](file:///C:\Users\hollow\AppData\Local\Temp\ksohtml7220\wps9.jpg) 

**注：创建的文件和目录，文件会拿走x权限，目录会拿走w权限**

对于root用户，文件的默认权限是644(-rw-r--r--)，目录的默认权限是755(drwxr-xr-x)

对于普通用户，文件的默认权限是664(-rw-rw-r--)，目录的默认权限是775(drwxrwxr-x)

\# umask 				//查看当前用户的umask权限

\# umask 	-S			//人性化显示

\# umask  0000		//临时修改umask

\# umask  /etc/bashrc	//永久性修改（不建议）

\# file  name			//查看文件或目录的类型

![img](file:///C:\Users\hollow\AppData\Local\Temp\ksohtml7220\wps10.jpg) 

***\*软连接：\****

\# ln  -s  file  file_slink 	//目标文件 链接文件

***\*硬链接：\****

两个限制：

 不允许给目录创建硬链接

 只有在同一文件系统中的文件之间才能创建链接，即不同分区上的两个文件之间不能够建立硬链接。

\# ln  file  file_hlink			//为file创建硬链接文件file_hlink

***\*域名：\****

\# hostname  				//查看本及域名

\# hostname liqiju.com  		//临时修改域名为liqiju.com

\# hostnamectl set-hostname liqiju.com	  //永久修改(/etc/hostname)

***\*管道：\****

\# ls  -l  /etc/init.d | more				   //分页显示

 

***\*网络配置\****

/etc/sysconfig/network-scripts/ifcfg-eth0     //配置IP、Gatewau、子网掩码

 ONBOOT=yes

 BOOTPROTO=static

 IPADDR=192.168.40.22

 NATMAXS=255.255.255.0

 GATEWAY=192.168.40.2

 service  network  restart           	//重启网络服务

/etc/resolv.conf

包含nameserver、search、domain这3个关键字

 nameserver关键字后面紧跟着一个DNS主机的IP地址，可以设置2~3个nameserver

 search关键字后紧跟的是一个域名。每个主机严格来说都应该有一个FQDN（全限定域名），所以往往域名就很长，如果这里写成search google.com，那么www就代表www.google. com了，这个关键字后可以跟多个域名

 domain关键字和search类似，不同的是domain后面只能跟一个域名                 

 nameserver  8.8.8.8        //配置DNS

 search  google.com

 domain  google.com

/etc/sysconfig/network					//更改主机名

\# init  6							 //重启主机

\# hostname                        //显示主机名

/etc/hosts                   //ping主机名可以ping通

192.168.40.22  master

192.168.40.23  Slave1

192.168.40.24  Slave2

/etc/hostname

//修改主机名

***\*SSH免密登录：\****

\# ssh-keygen -t  rsa -P ''

***\*Linux软件安装\****



> wef

```shell

```

 

\------------------------------------------------------------------------------------------------------

//通配符--用于匹配Linux中的文件或目录

*

?

[]

[!]

ls p*      //以p开头的所有

ls p?      //pa或p8

ls pass[abcd]d 	 //

ls pas[!abg]d 		 //

 

//正则表达式--用于匹配文件中的内容

cat test.txt | grep [[:upper:]] //匹配所有的大写字母

...         [[:digit:]] 

...         [[:alnum:]] //任何字母和数字

...         [[:lower:]]

^    //锚定行首

$    //锚定行尾

 

//sed查找||替换||插入

sed -a  添加(下一行)  	//sed '2a hello word' filename 在文件的第2行添加hello world 这一行

​	-d 	删除   	//sed '2,5d' filename  删除filename文件内容的2-5行

​	-i  插入(上一行)   //sed '$i hello world' 最后一行插入hello world

​	-p	打印

​	-s  替换       //sed 's/cat/dog/' filename  将filename文件中dog替换cat 

sed -i -a ...

 ...   //对源文件修改

 

//find查找

find -name filename  //find /root -name filename

​	 -user 用户名

​	 -group 组名

​	 -mtime n 查找n天前被修改过的文件 //find /var -mtime -3  查找var目录3天内修改过的文件

​	 -atime n 查找n天前被访问过的文件

​	 -size     //find /root -size +5M 大于5MB的文件(-5M小于5MB)

​	 -type d/f/b/l/p

   -empty

​	 -exec command {} \;   //find /root -size -5M -exec ls -l {} \;

​	 ...

//磁盘分区

sda,dha,vda  //

tmpfs 	//硬盘驱动文件

lsblk 	//查看分区信息

//创建分区

​	1,fdisk /dev/vda        //创建分区

​	2,partprobe /dev/vda  //重新读取分区表

​	3,mkfs.ext4 /dev/vda1 //格式化分区vda1 

​	4,挂载(将硬盘和目录挂钩)

​		1.手动挂载

​			mkdir /mnt/sdb1-lewis

​			mount /dev/sdb1 /mnt/sdb1-lewis/

​		2.永久挂载(将设备添加到/etc/fstab)

​			//可以用/dev/sdb1(目录)或UUID(#blkid //查看设备UUID号)进行挂载

​			/dev/sdb1  /mnt/sdb1-lewis  ext4 defaults 0(转成标志) 0(不检查开机直接挂载)

​				//default 应用于设备的自定义选项，defaults是必须的

​				//0表示内容不需要备份 1相反

​				//0不检查开机直接挂载 1检查后挂载 2检查后第二个挂载

​			//挂在后使用 #mount -a 检查避免文件错误导致开机困难

//swap(虚拟内存)

作用

1,存放内存中不活动的信息

2,内存写满时，使用

3，如果虚拟内存写满，Linux会very卡，even奔溃

<=4G    at least 4G

4-16G   at least 8G

16-64G   at least 16G

64-256G  at least 32G

\# free -h  		//查看可用的内存和虚拟内存空间 

创建步骤:

 创建分区

 将分区类型设为swap-fdiskt (修改分区类型)

 partprobe /dev/vda  //重新读取分区表

 格式化-mkswap分区

 挂载(注：虚拟内存不需要挂载到特定的目录)		/dev/sdb2  swap  swap  defaults 0 0

 激活虚拟内存	swapon /dev/sdb2

 显示 free -h

//MBR(main boot record)主引导分区:告诉硬盘如何进行分区

1,支持4个主分区

2,使用扩展分区和逻辑分区可支持15个分区

3，允许最大分区的磁盘大小为2T

 

\#df -h 		//查看磁盘空间

 

 

***\*有趣的linux命令\****

 sl

 

 

 

 

> systemctl  start  mysql
>
> systemctl  enable  mysql   # 设置开机自动启动

 

 

 