## 1. Fiddler介绍

​		Fiddler 是以代理web服务器的形式工作的，它使用代理地址:127.0.0.1，端口:8888。Fiddler的运行机制其实就是本机上监听8888端口的HTTP代理。当Fiddler退出的时候它会自动注销，这样就不会影响别的 程序。不过如果Fiddler非正常退出，这时候因为Fiddler没有自动注销，会造成网页无法访问。解决的办法是重新启动下Fiddler。

<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/image-20230408213436725.png" alt="image-20230408213436725" style="zoom:80%;" />

> 参考：https://blog.csdn.net/weixin_46806288/article/details/124320597



## 2. 使用场景

1. 需要做接口测试/压力测试，但又没有接口文档；

2. 快速定位前后端问题；

3. 篡改数据，模拟假数据

4. 复杂场景

    ​	比如：同一域名下的请求，/img/xxx的资源发送到ServerA上，请求/api/xxx资源发送到ServerB上





## 3. 设置

### Fiddler抓取https

1. Tools>Options>HTTPS

2. 勾选Decrypt HTTPS CONNECTs，弹出框点击确定信任根证书

3. 勾选Ignore server certificate errors(unsafe)
4. 点击确定

### 抓取手机包设置

1. Tools>Options>Connections，勾选Allow remote cmputers to connect
2. 手机和Fiddler要连上同一个wifi
3. 设置手机链接的wifi使用手动代理
    - 主机名：Fiddler所在电脑ip
    - 端口号：Fiddler监听的端口号，默认8888
4. 打开手机浏览器输入 电脑ip:8888，下载Fiddler根证书
5. 完成



## 3. 过滤





## 4. 断点

> 全局断点
>
> Rules>Automatic Breakpoint>Before Requests
>
> 局部断点
>
> ​	请求之前
> ​    	左下角命令行输入：`bpu 指定的url + 回车`  ，取消局部断点：`bpu + 回车`
> ​	请求之后
> ​		bpafter url +回车`





## 5. 弱网测试

<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/image-20230219172702739.png" alt="image-20230219172702739" style="zoom: 67%;" />



>  弱网：
>
> - download: 10.7KB/s
> - upload: 2.7KB/s

> 开启弱网步骤：
>
> 1. Rules ->  Customize Rules
>
> 2. 配置文件设置网速
>
>     ```shell
>     if (m_SimulateModem) {
>     	// Delay sends by 300ms per KB uploaded.  每上传一KB延迟发送300毫秒
>         oSession["request-trickle-delay"] = "300"; 
>         // Delay receives by 150ms per KB downloaded. 每下载一KB延迟接收150毫秒
>         oSession["response-trickle-delay"] = "150"; 
>     }
>     ```
>
> 3. 开启弱网功能 Rule -> performance -> Simulate Modem Speeds





## 6. 插件

> https://www.telerik.com/fiddler/add-ons
>
> Willow插件：管理Rule List，Host List

