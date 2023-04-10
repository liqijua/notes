# Git

<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/git.png" alt="git" style="width:80%;" />



### 文件的状态

- untracked：未跟踪，表示文件不受git管理，一般新建的文件处于该状态 Untracked files

- staged：已暂存，表示对以修改的文件做了标记，使之包含在下次要提交的文件列表中 Changes to be committed

- committed：已提交，表示文件已经被提交到本地仓库

- modified：已修改，表示文件内容已被修改，但是没有做标记 Changes not staged for commit

  ​    

> .gitignore

```sql
# 注释
*.txt       # 忽略所有.txt结尾的文件
!lib.txt    # 但lib.txt除外
/temp       # 忽略根目录下的temp文件
build/      # 忽略build/目录下的所有文件
doc/*.txt   # 忽略 doc/notes.txt 但不包括doc/下子目录中的.txt
debug/*.obj: 忽略 debug/io.obj，不忽略 debug/common/io.obj 和 tools/debug/io.obj
**/foo: 忽略/foo, a/foo, a/b/foo等
a/**/b: 忽略a/b, a/x/b, a/x/y/b等
!/bin/run.sh: 不忽略 bin 目录下的 run.sh 文件
config.php: 忽略当前路径的 config.php 文件
```



>  idea中文件颜色的意义

| 文件颜色                           | 意义                                              |
| :--------------------------------- | :------------------------------------------------ |
| <font color="green">green</font>   | 已加入版本控制（add）但未提交到本地仓库（commit） |
| <font color="blue">blue </font>    | 已add 已commit  但有modify                        |
| <font color="red">red</font>       | 未加入版本控制（add）                             |
| white                              | 已add 已 commit 无modify                          |
| <font color="yellow">yellow</font> | 版本控制忽略的文件                                |

  

> 配置

```java
// 查看版本
git --version
// 全局配置用户名、邮箱
git config --global user.name "Kitty"    
git config --global user.email 123@qq.com   
// 删除全局配置
git config --global --unset user.name
    
// 查看系统配置信息
git config --list    
// 查看全局配置情况
git config --global --list
// 查看用户名、邮箱
git config --global user.name
git config --global user.email
                
    
// 查看某仓库下的配置情况
git config --local --list 
    

// 查看所有git命令
git --help -a
// 更新git
git update-git-for-windows
// 设置默认文本编辑器
git config --global core.editor vim
// 编辑Git配置文件
git config -e [--global]
    
/*
如果用了 --global 选项，那么更改的配置文件就是位于你用户主目录下的那个，以后你所有的仓库都会默认使用这里配置的用户信息。如果要在某个特定的仓库中使用其他名字或者电邮，只要去掉 --global 选项重新配置即可，新的设定保存在当前仓库的 .git/config 文件里。
*/
```



> 配置公钥

```java
// 配置秘钥
shh-keygen -t rsa -C "helloliqiju@gmail.com"
// 指定路径
shh-keygen -t rsa -C "email" -f C://Users/奈之若何/.ssh/gitee_id_rsa
/* 在github上配置公钥
   回到github上，进入Account Settings粘贴在你电脑上生成的key
   验证是否成功 
*/
ssh -T git@github.com
// 错误：出现 Permission denied (publickey) ；执行
ssh-add gitee_id_rsa
//若出现，执行
Identity added: gitee_id_rsa(gitee_id_rsa)
/*则成功；若出现：
Could not open a connection to your authentication agent.
则说明未启动ssh agent, 执行： */
ssh-agent bash
    
/*错误:You've successfully authenticated, but Gitee.com does not provide she access.
错误fatal: refusing to merge unrelated histories:*/
//执行
git pull origin master --allow-unrelated-histories
```



> 分支

```java
git branch       //查看当前分支
git branch -r    //查看远程分支
git branch                    //列出所有本地分支
git branch b1                 //创建分支b1
git checkout -b b2            //创建分支b2，并切换到分支b2
(先commit之后才会真正建立master分支，此时才可以建立其它分支)
git checkout b1               //切换分支到b1
git branch -d b1              //安全删除分支b1
git branch -D b1              //强行删除分支b2
git merge b1                    //合并分支b1到当前分支
    
    当你以此方式在上次提交更新之后创建了新分支，如果后来又有更新提交， 然后又切换到了 testing 分支，Git 将还原你的工作目录到你创建分支时候的样子。
合并冲突，可以用 git add 要告诉 Git 文件冲突已经解决
```

> 仓库

| 命令                    | 功能介绍                            |
| ----------------------- | ----------------------------------- |
| git init                | 在当前目录新建一个Git代码库         |
| git init [project-name] | 新建一个目录，将其初始化为Git代码库 |
| git clone [url]         | 下载一个项目和它的整个代码历史      |

> 增加/删除文件

| 命令                                  | 功能介绍                                                     |
| ------------------------------------- | ------------------------------------------------------------ |
| git add [file1] [file2] ...           | 添加指定文件到暂存区                                         |
| git add [dir]                         | 添加指定目录到暂存区，包括子目录                             |
| git add .                             | 添加当前目录的所有文件到暂存区                               |
| git rm [file1] [file2] ...            | 删除工作区文件，并且将这次删除放入暂存区                     |
| git rm --cached [file]                | 停止追踪指定文件，但该文件会保留在工作区                     |
| git mv [file-original] [file-renamed] | 改名文件，并且将这个改名放入暂存区                           |
| git add -p                            | 添加每个变化前，都会要求确认 # 对于同一个文件的多处变化，可以实现分次提交 |

> 代码提交

| 命令                                        | 功能介绍                                       |
| ------------------------------------------- | ---------------------------------------------- |
| git commit -m [message]                     | 提交暂存区到仓库区                             |
| git commit [file1] [file2] ... -m [message] | 提交暂存区的指定文件到仓库区                   |
| git commit -a                               | 提交工作区自上次commit之后的变化，直接到仓库区 |
| git commit -v                               | 提交时显示所有diff信息                         |

> 分支

| 命令                                               | 功能介绍                                     |
| -------------------------------------------------- | -------------------------------------------- |
| git branch                                         | 列出所有本地分支                             |
| git branch -r                                      | 列出所有远程分支                             |
| git branch -a                                      | 列出所有本地分支和远程分支                   |
| git branch [branch-name]                           | 新建一个分支，但依然停留在当前分支           |
| git checkout -b [branch]                           | 新建一个分支，并切换到该分支                 |
| git branch -d [branch-name]                        | 删除分支                                     |
| git merge [branch]                                 | 合并指定分支到当前分支                       |
| git checkout [branch-name]                         | 切换到指定分支，并更新工作区                 |
| git checkout -                                     | 切换到上一个分支                             |
| git push --set-upstream origin dev                 |                                              |
| git branch --set-upstream [branch] [remote-branch] | 建立追踪关系，在现有分支与指定的远程分支之间 |
| git push origin --delete [branch-name]             | 删除远程分支                                 |
| git branch -dr [remote/branch]                     | 删除远程分支                                 |

> 标签

| 命令                             | 功能介绍                   |
| -------------------------------- | -------------------------- |
| git tag                          | 列出所有tag                |
| git tag [tag]                    | 新建一个tag在当前commit    |
| git tag [tag] [commit]           | 新建一个tag在指定commit    |
| git tag -d [tag]                 | 删除本地tag                |
| git push origin [tag]            | 推送本地指定标签到远程仓库 |
| git push origin --tags           | 推送本地所有标签到远程仓库 |
| git tag -a [tag] -m  'v1.1'      | 新建标签，并指定标签描述   |
| git push origin :refs/tags/[tag] | 删除一个远程标签           |

> 查看信息

| 命令                        | 功能介绍                                       |
| --------------------------- | ---------------------------------------------- |
| git status                  | 显示有变更的文件                               |
| git status -s               | 简化显示有变更的文件                           |
| git log                     | 显示当前分支的版本历史                         |
| git tag -d [tag]            | 删除本地tag                                    |
| git log -3 --pretty=oneline |                                                |
| git reflog                  | 查看记录在本地的HEAD和分支引用在过去指向的位置 |

> 远程同步

| 命令                             | 功能介绍                               |
| -------------------------------- | -------------------------------------- |
| git pull [remote] [branch]       | 取回远程仓库的变化，并与本地分支合并   |
| git push [remote] [branch]       | 上传本地指定分支到远程仓库             |
| git push [remote] --force        | 强行推送当前分支到远程仓库，即使有冲突 |
| git push [remote] --all          | 推送所有分支到远程仓库                 |
| git remote -v                    | 显示所有远程仓库                       |
| git remote show [remote]         | 显示某个远程仓库的信息                 |
| git remote add [shortname] [url] | 增加一个新的远程仓库，并命名           |

> 撤销 

| 命令                                            | 功能介绍                                    |
| ----------------------------------------------- | ------------------------------------------- |
| git checkout [file]                             | 恢复暂存区的指定文件到工作区（手动删除）    |
| git restore --staged [file]  git restore [file] | 恢复暂存区的指定文件到工作区（git rm 删除） |
| git checkout .                                  | 恢复暂存区的所有文件到工作区                |
| git reset --hard HEAD^                          | 回退1个版本                                 |
| git reset --hard HEAD^^                         | 回退2个版本                                 |
| git reset --hard HEAD~1                         | 回退1个版本                                 |
| git reset --hard 版本号                         | 回退到哪个版本                              |
| git reset HEAD                                  | 取消加入版本控制的文件                      |



#### ++

---



| 命令                          | 功能介绍                             |
| ----------------------------- | ------------------------------------ |
| git push origin liqiju:master | 将本地liqiju分支推送到远程master分支 |
| git push origin liqiju:liqiju |                                      |
| git pull origin liqiju:master | 拉取远程master分支到本地liqiju分支   |
| git merge master              | 合并master分支到==当前==分支         |







### Tag



```sh
git tag -a tagname -m '提交信息'
git tag -a tagname 版本号 -m '解释' 		 # 补录标签
git tag -l 'v1.8*'			  			# 显示符合指定格式的标签

# 列出所有tag
$ git tag

# 新建一个tag在当前commit
$ git tag [tag]

# 新建一个tag在指定commit
$ git tag [tag] [commit]

# 删除本地tag
$ git tag -d [tag]

# 删除远程tag
$ git push origin :refs/tags/[tagName]

# 查看tag信息
$ git show [tag]

# 提交指定tag
$ git push [remote] [tag]

# 提交所有tag
$ git push [remote] --tags

# 新建一个分支，指向某个tag
$ git checkout -b [branch] [tag]
```











```sh
# 推送tag到远端仓库
# 推送tag名为V1.0到远程liqiju分支上
git push origin liqiju V1.0

# 当前分支回退到tag_name版本
git checkout tag_name

# 下面两个指令有问题
# 如何取到指定tag的代码
#    在测试验证和开发回归的时候，我们经常会遇到回退版本，特别是回退到某个发布的版本，由于打了tag，就很好的能快速退到，tag号# 要记住啊，记不住也没事，下拉代码执行git tag会弹出来所有的tag，自己复制你需要的那个就是；
# 将branch_name分支，回退到tag_name版本
git checkout -b branch_name tag_name
很简单了，对应分支名称，tag号就行了。
git checkout -b liqiju  V8V1R010C010B021
```

