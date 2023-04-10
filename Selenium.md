> Python 代码 -- 调用 ---> selenium --- 发送 HTTP 请求 ---> 浏览器驱动 ---- （特殊方法） --> 浏览器

### webDriver-helper

> webdriver-helper的作用：

1.自动获取浏览器的版本号

2.自动下载合适的浏览器驱动

3.自动把浏览器驱动启动

4.自动启动浏览器



> 安装（python版本需3.9以上）

```python
# 1.*版本是免费的，2.*是收费的
pip install webdriver-helper==1.*
```



> 基本使用

```python
from webdriver_helper import *
import time
# 默认chrome，可指定get_webdriver("firefox")
driver = get_webdriver()
driver.get("https://baidu.com")
time.sleep(5)
# 退出驱动程序并关闭所有相关窗口
driver.quit()
```

> 第二种方式

```python
from webdriver_helper import *
import time
with get_webdriver() as driver:
	driver.get("https://baidu.com")
	time.sleep(5)
```


