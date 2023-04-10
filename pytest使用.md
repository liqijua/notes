# pytest的使用

## 1. 简介

pytest是python的一种单元测试框架，同自带的unittest测试框架类似，相比于unittest框架使用起来更简洁,效率更高。

> Pytest特点

1. 非常容易上手，入门简单，文档丰富，文档中有很多实例可以参考；
2. 支持简单的单元测试和复杂的功能测试；
3. 支持参数化；
4. 执行测试过程中可以将某些测试跳过，或者对某些预期失败的Case标记成失败；
5. 支持重复执行失败的Case；
6. 支持运行由Nose，Unittest编写的测试Case；
7. 具有很多第三方插件，并且可以自定义扩展；
8. 方便的和持续集成工具集成；



> 优势

```
1. 编写用例格式更简单
2. 更加灵活的标签和更加好用的 firtures
3. 插件丰富：pytest-selenium（集成selenium）、  
           pytest-html（完美html测试报告生成）、
           pytest-rerunfailures（失败case重复执行）、          
           pytest-xdist（多CPU分发）
4. 可以使用全局配置文件 pytest.ini  --- 使用pytest --help指令可以查看pytest.ini的设置选项
5. 可以很好的和CI工具结合，例如jenkins
6. 兼容unittest用例
```



## 2. 安装

```
pip install pytest -i https://mirrors.aliyun.com/pypi/simple
```



## 3. 入门案例

```python
import pytest

def test_case1():
    print('this is test_a')
    res = 1 / 0

def test_case2():
    print('this is test_b')
    res = 1 * 0

if __name__ == "__main__":
    # demo1.py是当前脚本的名称
    # 也可以通过命令 pytest -s demo1.py 来运行
    pytest.main(['-s', 'demo1.py'])

```





### 3.1 main()参数详解

main()括号内可传入执行参数和插件参数，通过[]进行分割，[]内的多个参数通过 ‘逗号’ 进行分割。

```
运行目录及子包下的所有用例  		pytest.main(['目录名'])
运行指定模块所有用例  		  pytest.main(['test_reg.py'])
运行指定模块指定类指定用例  		pytest.main(['test_reg.py::TestClass::test_method'])  冒号分割

-q: 安静模式, 不输出环境信息
-v: 丰富信息模式, 输出更详细的用例执行信息 最高级别信息 — verbose
-s: 显示程序中的print/logging输出
-k: 来挑选要执行的测试项,后面接的名称可以为函数名称、类名称、文件名称、目录名称,支持模糊查询
-m: 运行打标签的用例,后面接标签名称
-x: 出现一个用例失败则停止执行测试用例
--resultlog=./log.txt 生成log
--junitxml=./log.xml 生成xml报告
--html=./log.html   生成html报告；上面方法生成的报告，css是独立的，可以把css样式合并到html里，再加一个参数--self-contained-html
--maxfail=num  表示用例失败总数等于num 时停止运行
--tb=line    错误信息在一行展示
```





### 3.2 Pytest测试用例标准

> 默认规则

1. 函数或方法名——必须==test开头==来命名，例如：`test_case1(), testCase2()`；
2. 模块名——命名规则  `test_*.py` 或  `*_test.py`；
3. 类名——以==Test开头== 且 没有初始化`__init__`方法；
4. 其他——也会执行 unittest定义的测试用例类；



> 自定义规则

可以通过配置文件进行指定。在运行pytest的时候，pytest会自动搜索所在目录中的配置文件，命名`pytest.ini`。

```
[pytest]
; ini文件中的 英文分号后面的内容都是注释
; 选项 通常是- 或者 -- 开头内容
addopts = -s
; 测试模块所在目录
testpaths = ./
; 测试模块文件名称规则 多个内容用空格分隔
python_files = test_*.py *test.py
; 测试类名称规则
python_classes = Test_*
; 测试函数或者方法的名称规则
python_functions = hello_*
```



- 注意
    - windows系统 可能运行会报错，在配置文件中有中文的情况， 需要调整配置文件的编码为 GBK 而不使用 UTF-8；
    - 配置文件中路径、文件名、类名、函数名规则不区分大小写；







## 4. 标记

### 4.1 标记跳过

```python
'''
	@pytest.mark.skip(reason=None)
	添加到函数或方法上，跳过函数或方法的执行
	
	@pytest.mark.skipif(condition: bool, reason=None)
	只有条件为True才会跳过，跳过函数或方法的执行
'''
import pytest


@pytest.mark.skip("就想跳过")
def test_case1():
    print('this is test_case2')
    res = 1 * 0


@pytest.mark.skipif("1<2", reason="符合条件才跳过")
def test_case2():
    print('this is test_case3')
    res = 1 * 0


def test_case3():
    print('this is test_case4')
    res = 1 * 0


if __name__ == "__main__":
    # -s   运行正确或错误都打印结果
    # 'demo1.py'  只运行demo1.py
    pytest.main(['-s', 'demo1.py'])

    
# =================== 
# 1 passed, 2 skipped in 0.06s 
# ===================
```



### 4.2 标记失败

```python
'''
	@pytest.mark.xfail(condition=None,reason=None,raises=None)
	标记预期会出异常的测试，只有出现异常才对，不出异常反而不对
'''
import pytest


@pytest.mark.xfail(reson="除数为0异常", raises=ZeroDivisionError)
def test_case1():
    print('this is test_case1')
    res = 1 / 0

if __name__ == "__main__":
    # -s   运行正确或错误都打印结果
    # 'demo1.py'  只运行demo1.py
    pytest.main(['-s', 'demo1.py'])


# =================== 
# 1 xfailed in 0.06s 
# ===================
```





## 5 参数化

可以向函数动态传参

```
@pytest.mark.parametrize(argnames, argvalues, ids=None)
	- argnames    参数名，[]或()
	- argvalues   参数值，[(),()]或[[],[]]
	- ids 		  测试id，可省略
```



`

```python
import pytest


# ids元素个数要和数据组数相同（len(ids)==数据中元组个数）
@pytest.mark.parametrize(["x", "y", "z"], [(5, 5, 5), (10, 9, 20)], 
                         ids=["group1", "group1"])
def test_case(x, y, z):
    volume = x * y * z
    print(f"体积：{volume}")


if __name__ == "__main__":
    pytest.main(['-s', 'demo2.py'])

```







## 6. 夹具

类似生命周期钩子，用于定义在...之前执行，在...之后执行。

### 6.1 setup&teardown方式

==注意：== 模块，类，方法，函数夹具==名称是固定的==。

```python
# --------模块中---------
# 在模块中所有普通函数执行前执行，并且只执行一次
def setup_module(module):
    ...
    
# 在模块中所有普通函数执行后执行，并且只执行一次
def teardown_module(module):
    ...


# ----------函数--------
# 在模块中 任意一个普通函数 执行前都会执行一次，一个函数执行一次
def setup_function(function):
    ...

# 在模块中 任意一个普通函数 执行后都会执行一次，一个函数执行一次
def teardown_function(function):
    ...
    
    

# -------类中---------
# 在类中，所有普通方法执行前执行，并且只执行一次
@classmethod
def setup_class(cls):
    ...
    
# 在类中，所有普通方法执行后执行，并且只执行一次
@classmethod
def teardown_class(cls):
    ...


# ---------方法---------
# 类中方法，任意一个普通方法 执行前都会执行一次
# 也可以 def setup()
def setup_method(method):
    ...
    
# 类中方法，任意一个普通方法 执行后都会执行一次
# 也可以 def teardown()
def teardown_method(method):
    ...
```





### 6.2 注解方式

> 定义夹具（先定义，才能使用）

- 无返回值

    ```python
    @pytest.fixture()
    def before():
        print("*****before*****")
    ```

- 有返回值

    ```python
    @pytest.fixture()
    def login():
        print("login")
        return "user"
    ```

- 有参数

    ```python
    @pytest.fixture()
    def gen_data(request):
        print("gen_data")
        # 有无返回值均可
    ```



> 使用

```python
@pytest.mark.usefixtures("before")
def test_1():
    print('test_1()')
```

这里的用法有点怪异，但pytest做了 依赖注入处理

下面的login是形参的名字，也是夹具函数的名字，pytest会调用夹具，把返回值传入此测试方法

```python
def test_1(login):
    print ('test_1()' , login)
```



在夹具函数上添加参数自动使用

```python
def fixture(
    scope="function",
    params=None,
    autouse=False,
    ids=None,
    name=None
):
```

- 参数
- scope 夹具的级别 有 session module fuction(包含method) class

- autouse 是否自动使用



- 代码

    ```python
    import pytest
    
    @pytest.fixture(scope="module", autouse=True)
    def mod_header(request):
        print('module      : %s' % request.module.__name__)
    
    @pytest.fixture(scope="function", autouse=True)
    def func_header(request):
        print('function    : %s' % request.function.__name__)
    
    def test_one():
        print('in test_one()')
    
    def test_two():
    print('in test_two()')
    ```

    

### 6.3 参数化使用夹具

- 代码例子

    ```python
    import pytest
    
    @pytest.fixture(params=[1, 2, 3])
    def init_data(request):
        print("test_data   " ,request.param )
        return request.param
    
    def test_not_2(init_data):
        print('test_not_2: %s' % init_data)
        assert test_data != 2
    Copy
    ```

    - 说明(执行顺序，和数据传递)
        - 因为 被测试方法有 参数名称 为 init_data
        - 所以pytest会找到 同名的 fixture 函数
        - 但装饰器上有参数 params，长度为3
        - 所以会进行三次测试函数的调用，
        - 但测试之前会先执行 fixture函数
        - 在执行fixture函数之前 组装好 request对象，里面有 scope param 等属性





## 7. 插件

插件可以进行增强。 地址列表：https://plugincompat.herokuapp.com/

### 7.1 html报告

- 安装插件

    `pip install pytest-html`

- 使用

    - 命令行方式

        `pytest --html=存储路径/report.html`

    - 配置文件方式

        ```ini
        [pytest]
        addopts = -s --html=./report.html
        Copy
        ```



### 7.2 指定执行顺序

- 安装插件

    `pip install pytest-ordering`

- 使用插件

    添加装饰器 @pytest.mark.run(order=x) 到测试函数或者方法上

- 例子

```python
  import pytest

  @pytest.mark.run(order=-2)
  def test_1():
      print("1")


  @pytest.mark.run(order=-1)
  def test_2():
      print("2")


  @pytest.mark.run(order=0)
  def test_3():
      print("3")


  def test_4():
      print("4")


  @pytest.mark.run(order=1)
  def test_5():
      print("5")


  @pytest.mark.run(order=2)
  def test_6():
      print("6")

  # 打印结果为3 5 6 4 1 2
```

- 规则
    1. 自然数(从0开始的整数)顺序 (从小到大)
    2. 未加标注
    3. 负数从小到大





### 7.3 失败重试

- 作用

    对于有外部依赖，可能会失败的函数，在失败后多试几次

- 安装插件

    `pip install pytest-rerunfailures`

- 使用

    - 命令行方式

        `pytest --reruns 5

    - 配置文件方式

        ```ini
        [pytest]
        addopts = -s --reruns 5
        Copy
        ```

- 代码示例

```python
  import pytest
  import random


  def test_num():
      num = random.randint(1, 10)
      # print(num)
      assert num > 8


  if __name__ == '__main__':
      pytest.main([ '-s', '--reruns' , '5', 'runrun.py'])
```