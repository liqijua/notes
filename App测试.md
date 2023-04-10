# APP测试

## 概述

> 移动app特性：

- 设备多样性
- 网络多样性
- 平台多样性

> 移动app测试与传统软件测试的区别 

- 页面布局不同
- 使用场合不同
- 输入方法不同
- 操作方式不同



## 测试要点 

1. 专项测试
    - 安装测试
    - 卸载测试
    - 升级测试
    - 交互性测试
    - 弱网测试
    - 耗电量测试
2. UI测试
3. 功能测试
4. 兼容性
5. 易用性
6. 性能测试
7. 安全测试



## 专项测试

### 安装测试

> 移动设备比较多，例如一个品牌的手机会有不同的系列，每个系列有多个型号，App以来的平台也比较多，在测试时要考虑不同手机，不同OS的==兼容性==。

1. 安装渠道

    - 移动App的==安装渠道==比较多，如应用商店，应用宝，扫码，对于多种渠道的安装方式，在测试时每个渠道都要进行测试，以确保通过每个渠道都能正确安装软件。

2. 安装前

    - 如果设备空间==不足==，要确保有相应提示。有的App直接提示空间不足，无法安装；有的App会先安装，待空间用尽时再提示。

3. 安装中

    > 常见bug：中断安装后，未完成安装的应用图标一直显示在手机上，无法删除（僵尸程序）

    - App安装过程中要进行UI测试，例如给用户提供进度条提示。
    - App在安装过程中是否可以==取消安装==，如果可以，确保取消安装的处理要与概要设计要求一致，例如：如果App概要设计要求取消安装处理过程为：取消安装进行回滚处理，将已经安装的我呢见全部删除，那么在实际取消安装也必须如此。
    - 如果安装过程中出现==中断==，如：死机、重启、电量耗尽、关机等，App安装的处理是否与App概要设计一致，如中断安装，当再次开机时继续安装；启动后台进程守护安装，当再次开机时提示App安装完成。
    - 取消安装后再次安装

4. 安装后

    - App安装完成后，测试其是否能正常运行，安装后的文件夹及文件是否写入了指定的目录下。
    - 是否可以卸载应用
        - 通过桌面卸载
        - 通过软件设置卸载
    - 卸载之后重新安装，是否能安装成功

5. 对于已经安装的软件，如果再次安装，要弹出已安装或更新提示，而不是产生冲突。

    

### 卸载测试

- 卸载时，要有卸载提示信息。
- App在卸载过程中是否支持取消卸载，如果支持，要确保取消卸载的处理与App概要设计描述一致。
- 卸载软件的过程中如果出现意外情况，如司机，重启，点亮耗尽，关机等，要有相应的处理措施，如进行回滚，当再次开机时需要重新卸载。
- 中断卸载，当再次开机时继续卸载；启动后台进程守护卸载，当再次开机时提示卸载完成。
- 卸载完成之后，App相应的安装文件是否要全部删除，应当给用户一个提示信息，提示相应文件全部删除或让用户选择是否删除。

### 升级测试

1. 升级渠道

    - App安装渠道有多种，相应的升级渠道也有多种，要对多渠道升级进行测试，确保每个渠道的升级都能顺利完成；
    - 测试不同OS版本时升级是否都能通过；

2. 升级前

    - 如果有新版本升级，打开软件时要有相应的提示；升级包下载中断时要有相应处理措施，支持继续下载或则重新下载；

3. 升级后

    - 升级之后各个功能能否正常使用，老数据是否正常（新旧版本兼容）

4. 非强制升级

    - 用户可以选择不更新，老版本能正常使用，用户在下次启动app时仍能出现更新提示；

5. 强制升级

    - 用户没有更新时，自动退出客户端，下次启动App仍出现强制升级提示；

6. 在线跨版本升级

    - 升级后能正常使用
    - 选择用户使用量最多的版本进行跨版本升级测试

    

    > 版升级测试要注意哪些问题？
    >
    > 1. 新功能和旧功能都可以正常使用；
    > 2. 旧数据不会丢失；
    > 3. 跨版本升级测试时选择主流版本；



### 中断测试

- 移动设备大多具有电话，短信，蓝牙，手电筒等功能，在使用App时难免会受到干扰，例如使用App时，如果需要拨打/接听电话、启动蓝牙、相机、手电筒等，App要做好相应的处理措施，确保App不会产生功能性错误。
- 主要对==核心功能==存在实时数据交换的页面进行中断测试，除了确保中断过程中有合理处理，还需确保中断过后，回复正常
    - 来电、来短信、锁屏解锁、断网重连、断点、低电量提醒、前后台切换、App切换
    - 手机插拔数据线、耳机、闹铃、弹出框提示等操作
- 常见bug
    - 爱奇艺视频播放过程中，微信通话/电话中断：
        - 正常：app暂停播放，接听完电话后回复（自动回复或点击回复）
        - 异常：App卡死，音视频不同步
    - 微信视频聊天，低电量提醒中断：（电话中断-优先级最高）
        - 正常：聊天不中断，关掉提示信息后，正常通讯
        - 异常：App卡死/崩溃，微信聊天被强行断开



### 弱网测试

<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/App弱网测试要点.png" alt="App弱网测试要点" style="zoom:50%;" />

- 弱网测试

    - 移动App使用移动网络，移动网络的情况比较复杂，网络信号会受到环境的影响，容易发生网络不稳定的情况，而很多App的一些隐藏问题只有在复杂的网络环境下才会显现出来，例如正在使用的App遇到网络信号切换或变弱时，App不能响应或产生功能性错误，因此在测试时要特别对App进行弱网测试，及早发现问题。
    - 弱网场景下请求超时是否有友好提示，是否有重发机制
    - 数据多次提交（支付）是否只能被执行一次
    - 最大尝试次数，App是否正常工作（3-5次）

- 网络切换（3G/4G/5G/wifi）测试，例如从wifi切换到4G是否有相应的提示

- 测试有网/无网切换下应用的运行情况

    - 有网->无网->有网切换时，数据是否可以自动恢复，正常加载（网络中断重连）
    - 无网络时，是否有友好的断网提示（比如提示当前已断开网络，请检查网络设置）

- 离线测试（断网）

    - App在本地客户端会缓存一部分数据，离线状态下可以浏览本地数据
        - 对于离线（无网络）时，刷新获取新数据时，不能获取数据时能给出友好提示
        - 离线下，退出App再启动App时能正常浏览本地缓存数据
        - 离线后，测试切换、锁屏App是否正常运行
        - 再次连接时，是否收到离线时接受到的信息
    - 对于只有在线才能使用的功能或查看的数据，需要给出相应的提示
    
    

> 为什么要进行弱网测试？
>
> 弱网测试更贴近用户
>
> 弱网测试关注点有哪些？
>
> 1. 提交数据，是否重复提交
> 2. 友好提示
> 3. 确保App不会闪退，crash，ANR



### 耗电量测试

<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/image-20221018104801895-1680243734971-39.png" alt="image-20221018104801895" style="zoom:67%;" />



> 为什么要做专项测试

- 奔溃（crash）
- 卡顿
- 兼容性问题
- 发热/发烫
- 响应慢（anr）
    - 内存泄漏



<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/image-20230408094746688.png" alt="image-20230408094746688" style="zoom:80%;" />

> 



## UI测试

移动app的UI测试主要测试app界面（如窗口、菜单、对话框）布局、风格是否满足客户要求，文字标鼠是否简介准确、页面是否美观、操作是否友好等。确保产品UI需求原型图。

1. 界面布局
    - 界面布局合理且友好，符合用户习惯；
    - 列表型界面有滚动条；
    - 功能入口明显，容易找到；
2. 图形测试
    - 图片大小合适，显示清晰；
    - 页面字体与风格一致；
    - 背景颜色和字体、图片颜色搭配得当，让用户视觉体验良好；
3. 内容测试
    - 文字表达准确，符合app功能；
    - 文字没有错别字；
    - 文字用语简洁友好；
4. 安装、卸载、更新、分享页面logo测试





## 功能测试

> 移动App功能测试要点

- 注册
- 登录
- 运行
- 切换
    - 后台切换
    - 删除进程
    - 锁屏
- 推送





### 登录测试

- 登录方式

    1. 用户名密码
    2. 手机号验证码
    3. 指纹
    4. 二维码
    5. 手势
    6. 语音
    7. 头像识别（刷脸）
    8. 第三方登录（微信，QQ等）
    9. 一键登录

- 未登录用户

    - 只能访问指定页面，点击某些资源，提示登录或跳转登录页面
    - 用户主动退出登录后，下次启动App时，应该进入登录界面（竞品分析）

- 切换账号登录

    - 检验登录信息是否做到及时更新
    - 用户信息和权限是否错乱

- 登录控制

    1. 单点登录
        - 同时安装公司旗下的2个产品，登录一个，两一个会自动登录，信息互通，比如：淘宝，天猫；
    2. 多点登录
        - 不允许多点登录，将原用户下线，且给出相应提示信息
        - 允许多点登录，提示信息，且确保数据库操作无误，每个端数据都能同步更新
    3. 用户登录时间太久，账号信息会过期
        - 强制退出并提示，账号已过期，请重新登录
        - 出现：虽是登陆状态，但系统会提示用户没有登录

    

### 切换测试

- 后台切换：当并行运行多个程序时，在程序之间进行切换，要确保再次切换回来时App还保持在原来的页面上。
- 删除进程：测试从后台直接删除进程，当再次打开App时是否符合概要设计要求，同时测试删除进程时是否将App建立的会话一起删除。
- 锁屏包括手动锁屏和自动锁屏，测试锁屏之后App相应是否符合概要设计要求，例如再次打开时App还保持在原来的页面可以继续使用，当锁屏达到一定时间后就自动退出程序。

### 推送测试

1. 推送设置
    - 默认状态全部打开状态，移动App推送消息，确保推送及时，并且用户可以及时收到推送；
    - 设置开关可以打开，关闭；关闭时不会收到消息推送；
2. 未锁屏时
    - App应用后台运行，消息推送是否可以正常接受且可以点击查看；
    - App应用前台使用，可以接收到消息提醒，且可以点击查看；
3. 锁屏时：消息推送可以正常接收
4. 登录状态
    - 退出登录后，能否接受推送（按需求）；
    - 未登录用户登录，批量接受多条消息推送（红点/个数）；
    - 切换用户时，检查收到的推送与用户身份是否相符，没有将别人的消息推送过来；
5. 消息栏是否可以接收到消息提醒，且点击可查看。点击后消息



### 功能测试怎么做

> 功能测试点提取的用例设计方法都和web测试一致

根据产品需求文档编写测试用例，执行测试

- App是什么项目？核心业务功能梳理清楚--流程图分析
- App客户端的单个功能模块--细化分析
    - 使用等价类，边界值，考虑正常异常情况（长度，数据类型，必填，重复，隐形需求）
- 依据功能业务逻辑考虑功能交互



## 兼容性

> 云测平台，testin 免费50款机型 https://www.testin.cn/index.htm
>
> 云测平台对比：http://www.open-open.com/lib/view/open1463526042631.html

兼容性测试一般覆盖市面上主流的手机，例如：小米、华为、vivo、oppo等；ios手机就是x，xs，11，11plus，公司有哪些测试手机，就去测试那些手机的兼容性，界面测试。

- 应用是否在不同的OS中正常使用（Android，iOS）
- 每个平台的不同系统版本--系统更新后，需要做回归测试
- 能否适配各种屏幕尺寸（跟开发确认是否支持pad）
- 选择手机品牌，测试市场占有率最高的（使用百度统计）
- 分辨率适配：分辨率影响界面图标、文字大小，保证主流分辨率下页面显示完整



## 性能测试

<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/image-20230409201824250.png" alt="image-20230409201824250" style="zoom:67%;" />

> 测试要点：
>
> - 边界测试
> - 压力测试
> - 响应能力测试
> - 耗能测试
> - 稳定性测试

1. 边界测试

    ​		在各种边界压力下，如电量不足、存储空间不足、网络不稳定，测试App是否能正确相应，正常运行。

2. 压力测试

    ​		对移动App不断施加压力，如不断增加负载，不断增大数据吞吐量等以确定App的服务瓶颈，获得App能提供的最大服务级别，确定App性能是否满足用户需求。

3. 响应能力测试

    ​		相应能力测试实质上也是一种压力测试，在一定条件下App是否可以正确响应，

4. 耗能测试

    ​		测试App运行时对移动设备的资源占用情况，包括内存、CPU消耗、App长期运行时耗电量、耗流量情况，验证App对资源的消耗是否满足和用户需求。



### 稳定性测试

> 参考：http://testingpai.com/article/1595507210359

App长时间在前台/后台运行，用户对于App的稳定性提出了更高的要求。通过稳定性测试来避免崩溃（crash）、无响应（ANR）、内存泄漏等问题。



> monkey

```shell
# 语法
adb -s <device> shell monkey <options>

# 此时当前连接仅一个设备
# -p 指定启动的程序包名，如不指定，启动所有app
adb shell monkey -p com.lemon 1000

# -s 随机事件，如果seed相同，则Monkey测试产生的事件序列也相同
adb shell monkey -p com.lemon -s 111 1000

# -v 指定反馈的信息级别（日志的详细程度），共3级
# 	-v 日志级别level0，仅提供启动提示，测试完成和最终结果等少量信息
#   -v -v 日志级别level1，提供较为详细的日志，包括每个发送到Activity的事件信息
# 	-v -v -v 日志级别level2 最详细的日志，包括了测试中选中/未选中的Activity信息
adb shell monkey -p com.lemon -s 111 -v -v -v 1000

# --throttle 用于指定用户操作的延迟，单位ms
# 每个操作之后延迟0.1s
adb shell monkey -p com.lemon -s 111 -v --throttle 100 1000
	# 停止monkey运行
	adb shell
	ps | grep 'monkey'
	kill pid
	exit

# --randomize-throttle 模拟用户操作随机延迟，范围0-throttle设置的时间
# 操作随机延迟0-1s
adb shell monkey -p com.lemon -s 111 -v --throttle --randomize-throttle 1000 1000
```



> Monkey 事件百分比

<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/image-20230407155237470.png" alt="image-20230407155237470" style="zoom:80%;" />







## 安全测试

<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/image-20230409201221131.png" alt="image-20230409201221131" style="zoom:67%;" />



### 触屏操作测试

<img src="App%E6%B5%8B%E8%AF%95.assets/image-20230330223134850-1680243734971-51.png" alt="image-20230330223134850" style="zoom:80%;" />





## 其他

<img src="App%E6%B5%8B%E8%AF%95.assets/image-20230331141635846-1680243734972-60.png" alt="image-20230331141635846" style="zoom:80%;" />





## App测试流程

<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/image-20221018104943488-1680243734971-42.png" alt="image-20221018104943488" style="zoom:80%;" />

- 接受测试版本：由开发人员提交给测试人员
- App版本测试：主要检查测试App开发阶段对应的版本是否一致
- 正式环境测试：模拟实际使用环境进行测试
- 上线准备：测试通过后，对测试结果进行总结分析，为App上限作准备



> 第三方平台测试
>
> 1. 阿里EasyTest
> 2. 华为云测

`app自动化测试工具：Appium`



## 常见面试题

> App测试与web测试区别？

<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/image-20230409204206202.png" alt="image-20230409204206202" style="zoom:67%;" />

> Android App测试和IOS App测试的区别？

1. Android开源，系统版本多，兼容性复杂，IOS闭源，安全性比较高，系统版本少，兼容性测试简单；
2. IOS系统不支持降级，只能单向升级；
3. Android App安装渠道多，IOS只能通过App Store安装（testflight-官方的测试版本的安装工具）
4. 推送消息：Android可以绕过系统，IOS不行；
5. 操作习惯：Android back键，IOS Home手势；



> 为什么web端不会闪退，App会闪退？

<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/image-20230331144802496.png" alt="image-20230331144802496" style="zoom:80%;" />



---

# 小程序测试

<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/image-20230405144834001.png" alt="image-20230405144834001" style="zoom:80%;" />





<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/image-20230405141651587.png" alt="image-20230405141651587" width="70%" style="zoom:80%;" >



<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/image-20230405150511616.png" alt="image-20230405150511616" style="zoom:80%;" />

<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/image-20230405150849761.png" alt="image-20230405150849761" style="zoom:70%;" />

> 视图层和逻辑层分离，视图层负责渲染页面结构，逻辑层负责处理数据请求、接口调用等



<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/image-20230405151539125.png" alt="image-20230405151539125" style="zoom:70%;" />

<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/image-20230405153936906.png" alt="image-20230405153936906" style="zoom:80%;" />







<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/image-20230405154307438.png" alt="image-20230405154307438" style="zoom:80%;" />

<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/applettestpoint.png" alt="applettestpoint" />



<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/image-20230405154604184.png" alt="image-20230405154604184" style="zoom:80%;" />

<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/image-20230405155419422.png" alt="image-20230405155419422" style="zoom:80%;" />

<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/image-20230405155528742.png" alt="image-20230405155528742" style="zoom:80%;" />

<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/image-20230405155949603.png" alt="image-20230405155949603" style="zoom:80%;" />

<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/image-20230405160042769.png" alt="image-20230405160042769" style="zoom:80%;" />

<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/image-20230405160425334.png" alt="image-20230405160425334" style="zoom:80%;" />

<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/image-20230405160605897.png" alt="image-20230405160605897" style="zoom:80%;" />

<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/image-20230405160854591.png" alt="image-20230405160854591" style="zoom:80%;" />

<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/image-20230405161138386.png" alt="image-20230405161138386" style="zoom:80%;" />

<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/image-20230405161630263.png" alt="image-20230405161630263" style="zoom:80%;" />

<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/image-20230405162247432.png" alt="image-20230405162247432" style="zoom:80%;" />

<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/image-20230405162413127.png" alt="image-20230405162413127" style="zoom:80%;" />



---

# H5

<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/image-20230406105632552.png" alt="image-20230406105632552" style="zoom:80%;" />



<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/image-20230406161107765.png" alt="image-20230406161107765" style="zoom:80%;" />

<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/image-20230406161231280.png" alt="image-20230406161231280" style="zoom:80%;" />

<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/image-20230406161312727.png" alt="image-20230406161312727" style="zoom:80%;" />

<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/image-20230406161328773.png" alt="image-20230406161328773" style="zoom:80%;" />

<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/image-20230406161351064.png" alt="image-20230406161351064" style="zoom:80%;" />



<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/image-20230406161414034.png" alt="image-20230406161414034" style="zoom:80%;" />

<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/image-20230406161427491.png" alt="image-20230406161427491" style="zoom:80%;" />

<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/image-20230406161602807.png" alt="image-20230406161602807" style="zoom:80%;" />

<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/image-20230406161633445.png" alt="image-20230406161633445" style="zoom:80%;" />

<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/image-20230406161729375.png" alt="image-20230406161729375" style="zoom:80%;" />

<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/image-20230406161745676.png" alt="image-20230406161745676" style="zoom:80%;" />





# adb

## adb安装

> adb下载地址：
>
> Windows：https://dl.google.com/android/repository/platform-tools-latest-windows.zip
> Mac：https://dl.google.com/android/repository/platform-tools-latest-windows.zip
> Linux：https://dl.google.com/android/repository/platform-tools-latest-linux.zip
>
> 1. 加压缩
> 2. 配置环境变量
> 3. cmd中 adb测试是否安装成功





## adb使用

### 1. 连接夜深模拟器

> 如果链接不成功，复制adb.exe和nox_adb.exe(adb重命名) 到夜神bin目录替换

```shell
adb connect 127.0.0.1:62001 # 62001夜深模拟器端口
adb disconnect ip:port
# 查看设备连接状态
adb devices
```



### 2. 真机连接

> 连接步骤：
>
> 1. 设置>关于本机>版本信息>点击5下版本号，打开开发者模式
> 2. 设置>系统设置>开发者选项>打开USB调试模式
> 3. cmd中adb devices 查看连接设备



### 3. adb命令

```shell
# 真机和模拟器不一样，真机没有权限，进不去
adb shell # 以shell模式进入设备的系统，可使用ls,cd等
exit	# 退出设备

# pull/push的目录要有权限
# 拉去手机文件到电脑
adb pull <手机文件路径> <本机路径>
# 推送电脑文件到手机
adb push <电脑文件路径> <手机路径>


# 安装软件
adb install <电脑上apk路径> 

# 查看当前活动应用包名（ <= android7）
adb shell dumpsys activity | find "mFocusedActivity"
# 查看当前活动应用包名（ >= android8）
adb shell dumpsys activity | find "mResumedActivity"
	# 结果：mResumedActivity: ActivityRecord{e86ba80 u0 com.android.settings/.Settings t6}
	# 包名为：com.android.settings

# 卸载（加上应用包名）
adb uninstall com.tencent.mobileqq


# 打印日志
adb logcat 

# 将日志输出到电脑指定文件，持续输出
adb logcat -v time > D:\log.txt
```

<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/image-20230406174314449.png" alt="image-20230406174314449" style="zoom:80%;" />



<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/image-20230406175553356.png" alt="image-20230406175553356" style="zoom:80%;" />



<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/image-20230406223242184.png" alt="image-20230406223242184" style="zoom:80%;" />

<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/image-20230406223336150.png" alt="image-20230406223336150" style="zoom:80%;" />

<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/image-20230406224752308.png" alt="image-20230406224752308" style="zoom:80%;" />

<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/image-20230406224842653.png" alt="image-20230406224842653" style="zoom:80%;" />

<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/image-20230406224910945.png" alt="image-20230406224910945" style="zoom:80%;" />

<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/image-20230406224949050.png" alt="image-20230406224949050" style="zoom:80%;" />

<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/image-20230406230047810.png" alt="image-20230406230047810" style="zoom:80%;" />

<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/image-20230406230642498.png" alt="image-20230406230642498" style="zoom:80%;" />





