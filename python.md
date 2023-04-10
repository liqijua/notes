## 1. pip

### 1.1 windows

```shell
# 使用国内华为镜像源进行安装（下载速度快）
pip install virtualenv -i https://repo.huaweicloud.com/repository/pypi/simple/
# 2. 创建一个名为venv01的虚拟环境
virtualenv venv01
# 3. 进入虚拟环境（需要提进入venv01/Scripts/文件夹执行）
activate
# 4. 退出虚拟环境（需要提进入venv01/Scripts/文件夹执行）
deactivate

# 查看当前环境下安装的所有包及版本
pip freeze
# 查看当前环境下安装的所有包及版本
pip list
# 默认下载最新版本
pip install 包名
# 指定版本下载
pip install 包名==版本号
# 安装指定包（-i指定从国内华为镜像源下载，下载速度快。默认下载镜像源中最新版本）
pip install 包名 -i https://repo.huaweicloud.com/repository/pypi/simple/
# 指定版本下载
pip install 包名==版本号 -i https://repo.huaweicloud.com/repository/pypi/simple/
# 卸载指定包
pip uninstall 包名

# 导出当前环境中安装的所有包及其版本导出到requirements.txt
pip freeze > requirements.txt
# 安装requirements.txt中所有包到当前环境中
pip install -r requirements.txt -i https://repo.huaweicloud.com/repository/pypi/simple/

# 检查那些包需要更新
pip list --outdated
# 更新指定的包
pip install --upgrade 包名
```



### 1.2 linux

```shell
# 安装virtualenv
pip install virtualenv -i https://repo.huaweicloud.com/repository/pypi/simple/
# 创建名为venv1的虚拟环境
virtualenv -p python3 venv1
# 进入虚拟环境
source  env/bin/activate               
# 退出虚拟环境
deactivate

# 查看虚拟环境中安装的包
pip freeze 或 pip list     
# 收集当前环境中安装的所有包及其版本到requirements.txt 中
pip freeze > requirements.txt
# 安装requirements.txt中的所有包
pip install -r requirements.txt

# 检查那些包需要更新
pip list --outdated   
# 更新指定的包        
pip install --upgrade 包名

# 利用python3安装falsk
python3 -m  pip install flask -i https://repo.huaweicloud.com/repository/pypi/simple/
```







```python

```



## 2. 基础语法



### 运算符

```python
print(4 and 5)	# 5
print(7 or 8) 	# 7
```





### sort和sorted

> 1. sort 是应用在 list 上的方法，sorted 可以对所有可迭代的对象进行排序操作；
> 2. sort()原地排序返回值为None，内建函数sorted()返回的一个新的 list；

```python
list2 = [('b', 5), ('c', 12), ('a', 3)]
# 根据元组第二个元素降序排序
list2.sort(key=lambda x: x[1], reverse=True)
# [('c', 12), ('b', 5), ('a', 3)]
print(list2)

# 根据字典age值进行降序排序
list1 = [{"age": 20, "name": "a"}, {"age": 25, "name": "b"}, {"age": 10, "name": "c"}]
res = sorted(list1, key=lambda x: x["age"], reverse=True)
# [{'age': 25, 'name': 'b'}, {'age': 20, 'name': 'a'}, {'age': 10, 'name': 'c'}]
print(res)
```



> 三元表达式

```python
a,b = 5,6
x = a if a > b else b
```



### String

> python使用了字符串驻留机制，同样的字符串对象只会保存一份

```python
s1: str = 'fffff$%a#ffff34823—'
s2: str = 'fffff$%a#ffff34823—'
print(s1 is s2)  # True  地址相同
print(s1 == s2)  # True	 内容相同

a: int = 1200000000000000000000
b: int = 1200000000000000000000
print(a is b)  # True
print(a == b)  # True
```





```python
# -----------错误------------
print('错误'。center(22, '-'))

s = "\thello world，hello title"
# 如果s头部为\t就删除
s = s.removeprefix("\t")
```





### List 

> python中切片操作不会引起下标越界异常

```python
s1 = 'abcdefg'
list1 = [e for e in s1]		# ['a', 'b', 'c', 'd', 'e', 'f', 'g']
```





### 作用域

> Python 中只有模块（module），类，函数（def、lambda）才会引入新的作用域，
>
> ​	其它的代码块（如 if/elif/else/、try/except、for/while等）是不会引入新的作用域的，
>
> ​	也就是说这些语句内定义的变量，外部也可以访问





### 内置函数

```python
****

**map()** 

会根据提供的函数对指定序列做映射

第一个参数 function 以参数序列中的每一个元素调用 function 函数，返回包含每次 function 函数返回值的新列表

**语法**

​                map(function, iterable, ...)              

**参数**

- function -- 函数
- iterable -- 一个或多个序列

**返回值**

- python 2.x 返回列表
- python 3.x 返回迭代器

**实例**

​                def square(x):    return x ** 2 print(list(map(square,[3,4,5])))    #输出:  [9, 16, 25] print(list(map(lambda x:x*x,[3,4,5])))    #输出:  [9, 16, 25]              

**reduce()** 

函数会对参数序列中元素进行累积

函数将一个数据集合（链表，元组等）中的所有数据进行下列操作：用传给 reduce 中的函数 function（有两个参数）先对集合中的第 1、2 个元素进行操作，得到的结果再与第三个数据用 function 函数运算，最后得到一个结果。

**语法**

​                reduce(function, iterable[, initializer]])              

**参数**

- function -- 函数，有两个参数
- iterable -- 可迭代对象
- initializer -- 可选，初始参数

**返回值**

返回函数计算结果

**实例**

​                from functools import reduce print(reduce(lambda x,y:x*y,[1,2,3,4])) #计算过程：((1*2)*3)*4 结果：24 print(reduce(lambda x,y:x*y,[1,2,3,4],0)) #计算过程：(((1*0)*2)*3)*4 结果：0              

**filter()** 

1. 函数用于过滤序列，过滤掉不符合条件的元素，返回一个迭代器对象
2. 该接收两个参数，第一个为函数，第二个为序列，序列的每个元素作为参数传递给函数进行判，然后返回 True 或 False，最后将返回 True 的元素放到新列表中
3. 由于filter()使用了惰性计算，所以只有在取filter()结果的时候，才会真正筛选并每次返回下一个筛出的元素

**语法**

以下是 filter() 方法的语法:

filter(function, iterable)

**参数**

- function -- 判断函数。
- iterable -- 可迭代对象。

**返回值**

- 返回迭代器

​                \#!/usr/bin/python3 # 过滤出1~100中平方根是整数的数： from math import sqrt new_list = list(filter(lambda x:sqrt(x)%1==0, range(1, 101))) print(newlist)    # 输出结果 ：[1, 4, 9, 16, 25, 36, 49, 64, 81, 100]              
```





> **函数注解**
>
> - python3.5引入
> - 对函数的参数进行类型注解
> - 对函数的返回值进行类型注解
> - 只对函数参数做一个辅助说明，并不对函数参数进行类型检查
> - 提供给第三方工具，做代码分析，发现隐形bug
> - 函数注解的信息，保存在__annotations__属性中
> - python3.6中引入变量注解	i:int = 3





### 深copy浅copy

```python
list1 = [[1, 2, 3], ['a', 'b', 'c'], [13, 13, 89]]
# 浅copy
copy_list1 = list1.copy()
print(list1 is copy_list1)  # False
print(list1[0] is copy_list1[0])  # True
print(list1[1] is copy_list1[1])  # True
print(list1[2] is copy_list1[2])  # True
# 改变copy_list1值，list1值也会被修改
copy_list1[0].append('hello')
print(list1 == copy_list1)  # True

from copy import deepcopy

list1 = [[1, 2, 3], ['a', 'b', 'c'], [13, 13, 89]]
# 深copy
deepcopy_list1 = deepcopy(list1)
print(deepcopy_list1 is list1)
print(list1[0] is deepcopy_list1[0])  # False
print(list1[1] is deepcopy_list1[1])  # False
print(list1[2] is deepcopy_list1[2])  # False
# 改变deepcopy_list1值，list1值不会被修改
copy_list1[0].append('hello')
print(list1 == copy_list1)  # false
```







### 类

> 类变量

类和所有类的对象共享该

> 类方法和静态方法

- 类方法有一个隐形参数cls可以用来获取类信息
- 类方法使用@classmethod定义，静态方法使用装饰器@staticmethod定义

```python
class MyClass:
    def __init__(self, name, age):
        self.__name = name
        self.__age = age

    def __del__(self):
        print('析构方法被调用')

    @classmethod
    def count(cls, n, a):
        print(f'classname: {cls.__name__}')
        return cls(n, a)

    @staticmethod
    def sums():
        print('this is a static method: 静态方法中不能调用成员方法')


if __name__ == "__main__":
    t2 = MyClass.count('Tomcat', 49)
    # MyClass.sums()
```



> 访问权限

```python
class Student:
    def __init__(self, name, gender, age):
        # public
        self.name = name
        # protected
        self._gender = gender
        # private
        self.__age = age
    
    # private
    def __getAge(self) -> str:
        return self.age
```



> 继承中的构造函数

- 如果子类有自己的构造函数，不会自动调用父类的构造函数，如果需要用到父类的构造函数，则需要在子类的构造函数中显式的调用
- 子类继承多个父类，又没有自己的构造函数时，哪个父类在最前面且它又有自己的构造函数，就继承它的构造函数
- 在调用基类的方法时，需要使用super() 前缀
- Python总是首先查找对应类型的方法，不能在派生类中找到对应的方法时，它才开始到基类中逐个查找（先在本类中查找调用的方法，找不到才去基类中找）



> 抽象类



 

 

 









---

---------------Flask---------------

```
# flask run --host=127.0.0.1 --port=8000
# export FLASK_APP = hello(hello.py)       Linux中
# set FLASK_APP = hello                 window中
development environment and production environment
# FLASK_ENV=development              设置成开发环境
# FLASK_DEBUG=1/0                   开启或关闭debug调试
```



> flask项目部署步骤：

1. virtualenv -p python3 env
2. pip install -r requirements.txt
3. modify  database URI
4. modify  guni_cfg.py
5. export  FLASK_APP=projectname
6. migrate  database
7. init  table data
8. gunicorn -c 



> 将进程转到后台运行但xshell断开连接后无影响：

```shell
# no hung up
nohup python app.py &	

# 查询gunicorn的进程树以关闭gunicorn相关服务
pstree -ap | grep gunicorn      
```



> gunicorn部署flask项目

```shell
# 查看gunicorn进程树
pstree -ap | grep gunicorn
# 重启
kill -HUP 30080
```



```shell
#  -w: 表示进程（worker）  -b：表示绑定ip地址和端口号（bind）
gunicorn -w 4 -b 127.0.0.1:5001 运行文件名称:Flask程序实例名

# 指定配置文件运行
gunicorn -c gunicorn.conf 运行文件名称:Flask程序实例名
```



```sh
# gunicorn.conf配置文件
import os

# 用于处理工作的并发进程的数量，默认为1
workers = 5
# 允许挂起的连接数的最大值
backlog = 2048
# 指定进程的工作方式，默认为同步方式sync
# worker_class = "sync"
# 指定进程的工作方式为异步
worker_class = "gevent"
# 开启调试模式
# debug = True 
# 设置进程名称
proc_name = 'gunicorn.proc'
# 设置pid文件的文件名，如果不设置将不会创建
# pidfile = '/tmp/gunicorn.pid'
# 设置日志文件名
# logfile = '/var/log/gunicorn/debug.log'
# 定义错误日志输出等级
# loglevel = 'debug'
# 监听内网端口
bind = '0.0.0.0:80'
# 设置守护进程【关闭连接时，程序仍在运行】
daemon = True
# 设置超时时间120s，默认为30s。按自己的需求进行设置
timeout = 30
# 设置访问日志和错误信息日志路径
accesslog = '/www/wwwlogs/gunicorn_acess.log'
errorlog = '/www/wwwlogs/gunicorn_error.log'
# 由于指定了进程工作于同步方式，因此服务器运行时间长了可能会引起访问动态页面的卡顿，
# 这一般是Gunicorn阻塞引起的，可以将进程工程方式修改为异步工作方式，从而解决此类问题。
```

