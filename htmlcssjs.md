## HTML

​		HTML ( HyperTest Markup Language ) 超文本标记语言

### 一、基本标签

#### 1. 列表

1. 无序列表

    ```html
    <ul type="square">
        <li>苹果</li>
        <li>香蕉</li>
        <li>西瓜</li>
    </ul>
    ```

2. 有序列表

    ```html
    <ol type="A" reversed><!-- 1 a I i-->
        <li>奶茶</li>
        <li>咖啡</li>
        <li>果汁</li>
    </ol>
    ```

3. 自定义列表

    ```html
    <dl>
        <dt>热菜：</dt>
        <dd>开水白菜</dd>
        <dd>宫保鸡丁</dd>
        <dd>葱爆牛肉</dd>
        <dt>凉菜：</dt>
        <dd>凉拌猪耳</dd>
        <dd>凉拌木耳</dd>
    </dl>
    ```

4. 嵌套列表

    ```html
    <ol type="1">
        <li>饮品：</li>
        <ul>
            <li>牛奶</li>
            <li>咖啡</li>
            <li>果汁</li>
        </ul>
        <li>主食：</li>
        <ul>
            <li>面条</li>
            <li>米饭</li>
            <li>馒头</li>
        </ul>
    </ol>
    ```

#### 2. 图片

- 如果只指定宽或高，会保持图片等比例缩放；
- 如果指定图片宽或高百分比，会按照img标签的上级标签的宽作为100%；

```html
<img src="img/xihui.png" alt="西湖" title="西湖美景" height="150" width="150"> <br>
```

#### 3. 链接

```html
<!--点击放大图片链接-->
<a href="http://localhost:63342/webproject/img/xihui.png" target="_blank">
    <img height="50" src="img/xihui.png">
</a>
<!--下载-->
<a href="img/xihui.png" download="img/xihui.png">下载西湖断桥图片</a>
```



### 二、表单

<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/image-20220122114427037.png" alt="image-20220122114427037" style="zoom:80%;" />

```html
<form action="" method="get" style="width: 30%">
    <fieldset>
        <legend>个人信息</legend>
        <table>
            <tr>
                <td><label for="username">用户名：</label></td>
                <td><input type="text" name="username" id="username" value="默认值" placeholder="请输入用户名" required></td>
            </tr>
            <tr>
                <td><label for="pwd">密码：</label></td>
                <td><input type="password" name="pwd" id="pwd" placeholder="密码" required></td>
            </tr>
            <tr>
                <td>性别：</td>
                <td>
                    <input type="radio" name="gender" value="1" id="man" checked><label for="man">男</label>
                    <input type="radio" name="gender" value="0" id="woman"><label for="woman">女</label>
                </td>
            </tr>
            <tr>
                <td><label for="birth">生日：</label></td>
                <td>
                    <input type="date" name="birth" id="birth">
                </td>
            </tr>
            <tr>
                <td><label for="icon">头像：</label></td>
                <td>
                    <input type="file" name="icon" id="icon">
                </td>
            </tr>
            <tr>
                <td>爱好：</td>
                <td>
                    <input type="checkbox" name="hobby" value="swim">游泳
                    <input type="checkbox" name="hobby" value="food">美食
                    <input type="checkbox" name="hobby" value="music">音乐
                </td>
            </tr>
            <tr>
                <td>城市：</td>
                <td>
                    <select name="city">
                        <optgroup label="上海">
                            <option value="pudong">浦东</option>
                            <option value="pudong" selected>闵行</option>
                            <option value="pudong">新装</option>
                        </optgroup>
                        <optgroup label="福建">
                            <option value="fuzhou">福州</option>
                            <option value="fuqing">福清</option>
                            <option value="minhou">闽侯</option>
                        </optgroup>
                    </select>
                </td>
            </tr>
            <tr>
                <td>
                    <button type="submit">提交</button>
                </td>
                <td>
                    <button type="reset">重置</button>
                </td>
            </tr>
        </table>
    </fieldset>
</form>
```



### 三、表格

<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/image-20220122115105666.png" alt="image-20220122115105666" style="zoom:80%;" />

```html
<table border="1" cellspacing="0" width="30%" style="text-align: center">
    <thead>
    <tr>
        <th colspan="4">学生</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <th></th>
        <th>姓名*</th>
        <th>性别</th>
        <th>年龄</th>
    </tr>
    <tr>
        <td rowspan="3">总计</td>
        <td>婉儿</td>
        <td>女</td>
        <td>18</td>
    </tr>
    <tr>
        <td>晴儿</td>
        <td>女</td>
        <td>20</td>
    </tr>
    <tr>
        <td>兰儿</td>
        <td>女</td>
        <td>17</td>
    </tr>
    </tbody>
    <tfoot>
    <tr>
        <td colspan="4" style="color: red;"><small>*为必填</small></td>
    </tr>
    </tfoot>
</table>
```



**表格练习：**

<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/image-20220122115155335.png" alt="image-20220122115155335" style="zoom:80%;" />

```html
<table border="1" cellspacing="0" width="100">
    <tr>
        <td colspan="2">1-1</td>
        <td rowspan="2">1-3</td>
    </tr>
    <tr>
        <td rowspan="2">2-1</td>
        <td>2-2</td>
    </tr>
    <tr>
        <td colspan="2">3-2</td>
    </tr>
</table>
```



### 四、特殊符号

```html
<html>
    <head>
        <meta>
        <title></title>
    </head>
    <body>
    	<header>春&nbsp;江花月夜</header>
		<article>
    		<!--&quot;双引号-->
    		<!--&rarr;右箭头-->
    		&rarr;唐&quot;张若虚&quot; <br> 
    		春江潮水连海平，海上明月共潮生。<br>
		</article>
		<footer>尾部</footer>
	</body>
</html>


```









---

## CSS

​		CSS（Cascading Style Sheet）层叠样式表

### 一、html页面添加css的三种方式

> 优先级：就近原则

1. 内联

    ```html
    <p style="color: green;">海上升明月</p>
    ```

2. 内部

    ```html
    <!DOCTYPE html>
    <html>
        <head>
            <meta charset="UTF-8">
            <style>
                p { color: green; }
            </style>
        </head>
    </html>
    ```

3. 外部

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <link rel="stylesheet" href="css/index.css">
    </head>
</html>
```



### 二、选择器

#### 1. 一般选择器

> 优先级：id > class > label>伪类

1. id选择器（文件内唯一）

    ```css
    #head {
        color: red;
    }
    ```

2. 类选择器

    ```css
    .name {
        color: red;
    }
    ```

3. 标签选择器

    ```css
    p {
       colo: green; 
    }
    ```

#### 2. 分组选择器

> 格式：div, #name, .foot

```css
p, #name, .foot {
    color: red;
}
```

#### 3. 属性选择器

> 格式：p[属性名='属性值'] {}

```css
a[href='index.html'] {
    color: pink;
}
input[type='text'] {
    color: pink;
}
```

#### 4. 子孙后代选择器

> 格式：div div span {} 

```css
div div span {}
```

#### 5. 子元素选择器

```css
div>div>span {
    color: red;
}
body>p{}
```

#### 6. 伪类选择器

> a: <伪类选择器> {}

```css
a: hover {
    color: red;
}
a: link {
    color: blue;
}
a: visited {
    color: gray;
}
```

#### 7. 任意选择器

```css
* {}
```



### 三、颜色和图片

#### 1. 背景颜色

```css
p {
    background-color:rgb(255, 255, 255);
    backgroung-color: rgba(255, 255, 255, 0.5);
    backgroung-color: red;
    backgroung-color: #FFFFFF;
}
```

#### 2. 背景图片

```css
#img {
	background-image: url("../image/bg1.jgp");
    background-repeat: no-repeat; /*不重复，默认repeat。repeat-x...*/
    background-size: 100% 100%; /*宽，高*/
    background-position: left;  /*center right bottom top*/
    /*所有的块级元素都可以设置宽高*/
	width: 1200px;
    height: 700px;
}
```

#### 3. 溢出设置

overflow属性设置

1. visible   : 超出显示（默认）
2. hidden：超出不显示
3. scroll：超出滚动显示

```html
<head>
    <style>
        #d1 {
            width: 400px;
            height: 200px;
            /*visible默认超出显示；
            scroll 超出滚动显示
            hidden 超出范围不显示*/
            overflow: scroll; 
        }
    </style>
</head>
<body>
    <div id="d1">
        <img src="img/1.jpg">
    </div>
</body>
```



### 四、元素显示方式

- block  ：块级元素的默认值，独占一行，可以修改宽高，包括：h1-h6、p、div
- inline ： 行内元素默认值，占一行，不可以修改宽高，包括：span、b、i、a、small
- inline-block： 行内块元素默认值，占一行但可以修改宽高

 ```css
 span {
     height: 100px;
     width: 100px;
     display: inline-block; /*块显示*/
 }
 #div1 {
     display: none; /*不显示该块*/
 }
 ```



### 五、盒子模型

#### 1. 内边距

```css
padding: 50px;
padding: 50px 30px; /*上下50px， 左右30px*/
padding: 10px 20px 30px 40px; /*顺时针，上右下左*/
```



#### 2. 外边距

```css
margin: 50px;
margin: 0 auto; /*居中*/
margin: 50px 30px; /*距上下50px， 左右30px*/
margin: 10px 20px 30px 40px; /*顺时针，上右下左*/ 
```

##### 2.1 外边距粘连

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title></title>
        <style>
            #fuDiv {
                height: 150px;
                width: 200px;
                background-color: red;
                /*在fuDiv和ziDiv上边框重叠时，解决粘连问题*/
                overflow: hidden;
            }
            #sonDiv {
                height: 50px;
                width: 20px;
                background-color: blue;
                margin-left: 50px;
                /*在设置上外边距时，会对他所在的父div有影响，这种现象叫外边距粘连*/
                margin-top: 50px;
            }
        </style>
    </head>
    <body>
        <div id="fatherDiv">
            <div id="sonDiv">
                
            </div>
        </div>
    </body>
</html>
```



#### 3. 边框

```css
body {
    margin: 0; /*贴边*/
}

div {
    margin: 0 auto; /*居中对齐*/
    /*边框：宽度，样式（solid实线, dashed虚线, dotted点,double双线），颜色*/
    border: 3px solid red;
    border-top: 5px dashed green;
    /*圆角边框，顺时针：左上、右上、右下、左下*/
    border-radius: 10px 10px 5px 5px;
}
```



#### 4. 文本修饰和字体

1. 文本水平对齐方式text-align: left/right/center
2. 文本修饰text-decoration: overline/underline/line-through/none
3. 文本阴影text-shadow :  颜色  x偏移值  y偏移值  浓度值（越大越模糊）
4. 行高 line-height: 20px   可以实现文本垂直居中

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        #test {
            height: 70px;
            width: 700px;
            border: red solid 1px;
            font-size: 40px;
            text-align: center;
            line-height: 70px; /*垂直居中*/
            font-weight: bold; /*加粗*/
            font-style: italic; /*斜体*/
            font-family: 楷体;
            text-shadow: gray 10px 5px 3px; /*颜色 x偏移值 y偏移值 浓度值（越大越模糊）*/
        }
    </style>
</head>
<body>
<div id="test">
    虎虎生威
</div>
</body>
</html>
```



### 六、定位

#### 1. 静态定位static（文档流定位）

> 格式：position: static（默认）

特点：块级元素从上往下排列，行内元素从左往右排列；

#### 2. 相对定位

> 格式：position: relative

特点：元素不脱离文档流（不管元素移动到哪里，仍然占据原来的位置）；通过top/bottom/left/right 让元素相对于初始位置做位置偏移。

```css
#d2 {
	background-color: green;
	/*相对定位*/
	position: relative;
	left: 50px;
	top: 50px;
}
```



#### 3. 绝对定位

> 格式：position: absolute

特点：元素脱离文档流（只要元素修改绝对定位则它原来所占的位置立马让出）；

通过top/bottom/left/right让元素相对于窗口（默认）或某一个上级元素（需要在上级元素中做相对定位）做位置偏移

```html
#d2 {
	background-color: green;
	/*相对定位*/
	position: absolute;
	left: 50px;
	top: 50px;
}
```



示例：

<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/image-20220130200357049.png" alt="image-20220130200357049" style="zoom:80%;" />

```html
<style type="text/css">
	div {
		width: 253px;
		padding: 10px;
		background-color: rgba(0, 0, 0, 0.3);
		position: relative;
	}
	input {
		width: 213px;
		border: 0;
		padding: 10px 20px;
	}
	img {
		height: 20px;
		position: absolute;
		top: 17px;
		right: 30px;
	}
</style>
<body>
	<div>
		<input type="text" name="username" id="username" placeholder="请您输入用户名" />
		<img src="img/username.png">
		<br>
		<span style="color: red;font-size: 12px;">用户名不能为空！</span>
	</div>
</body>
```



#### 4. 固定定位

> position: fixed; （网页中返回头部按钮）

特点：脱离文档流，元素会固定在窗口的某个位置，不会随着内容的改变而改变；

<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/image-20220130203741929.png" alt="image-20220130203741929" style="zoom:30%;" />

```html
<style type="text/css">
	a {
		position: fixed;
		right: 100px;
		bottom: 50px;
	}
</style>
<body>
    <span id="head1">head</span>
	<a href="#head1">&rarr;返回头部</a>
</body>
```



#### 5. 浮动定位

> float: left/right;

特点：脱离文档流，元素从当前行向左或向右浮动，当撞到上级元素边框或其他浮动元素时停止。如果一行显示不下会自动换行，换行时有可能被卡住，如果元素的所有子元素全部浮动则自动识别的高度为0，通过给元素添加overflow: hidden解决。

如何移动元素：通过外边距



##### 练习一：

<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/image-20220206095232809.png" alt="image-20220206095232809" style="zoom:30%;" /><img src="htmlcssjs.assets/image-20220206100134207.png" alt="image-20220206100134207" style="zoom:60%;" />

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<style type="text/css">
			div {
				text-align: center;
				line-height: 100px;
				height: 100px;
				width: 100px;
				border: red solid 1px;
			}

			#box1 {
				float: left;
				background-color: red;
				height: 150px;
			}

			#box2 {
				float: left;
				background-color: yellow;
			}

			#box3 {
				float: left;
				background-color: blue;
				height: 120px;
			}

			#container {
				overflow: hidden;
				width: 500px;
				height: 200px;
				border: red solid 1px;
			}
		</style>
	</head>
	<body>
		<div id="container">
			<div id="box1">
				div1
			</div>
			<div id="box2">
				div2
			</div>
			<div id="box3">
				div3
			</div>
		</div>

	</body>
</html>
```



##### 练习二：

<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/image-20220206102255989.png" alt="image-20220206102255989" style="zoom:80%;" />

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title>首页</title>
		<style type="text/css">
			ul {
				margin: 0;
                padding: 0;
				list-style-type: none; /*去掉li前面的点*/
				line-height: 50px;
			}

			ul>li {
				float: left;
				margin-left: 50px;
			}

			header {
				background-color: #DCDCDC;
				height: 50px;
			}
		</style>
	</head>
	<body>
		<header>
			<ul>
				<li>首页</li>
				<li>免费课</li>
				<li>直播课</li>
				<li>会员课</li>
				<li>精品课</li>
				<li>线上班</li>
				<li>线下班</li>
			</ul>
		</header>
	</body>
</html>
```





### 七、示例

#### 1. 链接按钮

<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/image-20220205221119532.png" alt="image-20220205221119532" style="zoom:80%;" />

```css
a {
    display: block;
    height: 40px;
    width: 132px;
    background-color: #0aa1ed;
    color: #FFFFFF;
    font-size: 20px;
    text-align: center;
    text-decoration: none;
    line-height: 40px;
    /*鼠标移动上，变成小手*/
	cursor: pointer;
}
```







---

---

## JavaScript

### 一、简介

#### 1. 什么是javascript

​		javaScript简称js，功能是负责给页面添加动态效果；

#### 2. js特点

1. js是脚本语言，解释型语言，不需编译，由浏览器解释执行；
2. js是弱类型语言；
3. 基于面向对象的语言；
4. 安全性高；
5. 交互性强；

#### 3. 使用

HTML页面引入js三种方式：

1. 内联

    ```html
    <button type="button" onclick="alert('点击了提交')">提交</button>
    ```

2. 内部

    ```html
    <html>
    	<head>
    		<meta charset="utf-8">
    		<title></title>
    	</head>
    	<body>
            <button type="button" onclick="submit()">提交</button>
            <!--内部-->
    		<script type="text/javascript">
        		// js代码     
                var submit = function() {
                    alert('点击了提交');
                }
    		</script>
    	</body>
    </html>
    ```

3. 外部

    ```html
    <html>
    	<head>
    		<meta charset="utf-8">
    		<title></title>
            <!--外部引入js-->
    		<script src="js/index.js" type="text/javascript" charset="utf-8"></script>
    	</head>
    	<body>
            <button type="button" onclick="submit()">提交</button>
    	</body>
    </html>
    
    ```
    



### 二、数据类型

javaScript统称对象类型

1. 数值类型（number）
2. 字符串（string）
3. 布尔类型（boolean）
4. 未定义类型（undefined）
5. 自定义对象类型
6. typeof（变量）获取变量的类型



```js
console.log("undefined==null: " + (e == null)); // true
```



#### 1. var和let

1. var关键字定义的变量可以先使用后声明；let关键字定义的变量需要先声明再使用（let不存在变量提升）；

2. 使用var关键字声明的全局作用域变量属于window对象；使用let关键字声明的全局作用域变量不属于window对象

3. 使用var关键字声明的变量在任何地方都可以修改；

4. 在相同的作用域或块级作用域中，不能使用let关键字来重置var关键字声明的变量。在相同的作用域或块级作用域中，不能使用let关键字来重置let关键字声明的变量。let关键字在不同作用域，或不用块级作用域中是可以重新声明赋值的。

    

#### 2.const

1. 在相同的作用域或块级作用域中，不能使用const关键字来重置var和let关键字声明的变量；
2. 在相同的作用域或块级作用域中，不能使用const关键字来重置const关键字声明的变量；
3. const关键字定义的常量，声明时必须进行初始化，且初始化后不可再修改；
4. const 关键字在不同作用域，或不同块级作用域中是可以重新声明赋值的；



#### 计算器示例

<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/image-20220206220225507.png" alt="image-20220206220225507" style="zoom:80%;" />

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
	</head>
	<body>
		数值：<input type="text" name="num1" id="num1" value="" /> <br>
		数值：<input type="text" name="num2" id="num2" value="" /> <br>
		结果：<input type="text" name="result" id="result" /> <br>
		<button type="button" onclick="calcu('+')">+</button>
		<button type="button" onclick="calcu('-')">-</button>
		<button type="button" onclick="calcu('*')">*</button>
		<button type="button" onclick="calcu('/')">/</button>
		<!-- js -->
		<script type="text/javascript">
			var calcu = function(symbol) {
				var num1 = document.getElementById("num1").value;
				var num2 = document.getElementById("num2").value;
				var res = 0.0;
				if (isNaN(num1) || isNaN(num2)) {
					alert("非数值");
					document.getElementById("num1").value = '';
					document.getElementById("num2").value = '';
					return;
				}
	
				switch (symbol) {
					case '+':
						res = num1*1 + num2*1;
						break;
					case '-':
						res = num1 - num2;
						break;
					case '*':
						res = num1 * num2;
						break;
					case '/':
						res = num1 / num2;
						break;
				}
				document.getElementById("result").value = res;
			}
		</script>
	</body>
</html>
```







### 三、js组成

js:  ECMAScript，DOM，BOM

#### 1. BOM对象的使用

##### 1.1 常用方法

window: 该对象中的属性称为全局属性，方法称为全局方法，访问时可以省略window.

```js
window.alert(); // 提示框
window.confirm(); // 确认框
window.prompt(); // 弹出文本输入框
window.parseInt();
window.parseFloat();
var timer = setInterval(方法, 时间间隔); // 定时器
clearInterval(timer); // 停止定时器
setTimeout(方法, 时间间隔); // 只执行一次的定时器
```

例子：

```html
<!DOCTYPE>
<html>
    <head>
    </head>
    <body>
        <div id="content"></div>
        <!-- js -->
        <script type="text/javascript">
            var confirm = confirm(); 
            console.log(confirm); // false取消, true确认
            var name = prompt("请输入姓名");
			console.log(name);
            // 定时器
            var i = 0;
			var timer = setInterval(function() {
				console.log(i++);
                document.getElementById("content").innerHTML += "<h1>" + (i++) + "</h1>"
				if (i === 10) {
					clearInterval(timer);
				}
			}, 1000);
        </script>
    </body>
</html>
```



##### 1.2 常用属性

```js
// history 历史
window.history.length; // 得到历史页面数量
window.history.back(); // 返回上一页面
window.history.forward(); // 前往下一页面

// location位置
window.location.href=""; // 获取和修改浏览器的请求地址
window.location.reload(); // 刷新

// screen屏幕
screen.width; //获取屏幕的分辨率
screen.height;
document.documentElement.clientWidth; // 获取浏览器宽
document.documentElement.clientHeight; // 获取浏览器高

// navigator 导航/帮助
navigator.userAgent得到浏览器的版本信息
```



**常用事件：**

什么是事件：系统给提供的一些特定时间点，事件包括：鼠标事件、键盘事件、状态改变事件、

##### 1.3 鼠标事件

- onclick    鼠标点击事件
- onmouseover   鼠标移入事件
- onmouseout   鼠标移出事件
- onmousedown   鼠标按下事件
- onmouseup 鼠标抬起事件
- onmousemove   鼠标移动事件

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<style type="text/css">
			#btn {
				height: 100px;
				width: 100px;
				background-color: #DCDCDC;
				margin: auto;
			}
		</style>
	</head>
	<body>
		<div id="btn" onclick="click()" onmousemove="move()">
		</div>

		<!-- js -->
		<script type="text/javascript">
			var click = function() {
				console.log('click事件触发');
			}

			var move = function() {
				console.log('move事件触发');
			}

			var btnDocument = document.getElementById("btn");
			btnDocument.onmouseover = function() {
				console.log('over事件触发');
			};
			btnDocument.onmouseout = function() {
				console.log('out事件触发');
			};
			btnDocument.onmousedown = function() {
				console.log('down事件触发');
			};
			btnDocument.onmouseup = function() {
				console.log('up事件触发');
			};
		</script>
	</body>
</html>

```



##### 1.4 键盘事件

- onkeydown  键盘按下
- onkeyup  键盘抬起
- event.keyCode获取按键编码，String.fromCharCode()  把按键编码转成字符；

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
	</head>
	<body>
		<input type="text" id="name" />
		
		<script type="text/javascript">
			document.getElementById("name").onkeydown = function() {
				//
				console.log(event.keyCode);
			}
			document.getElementById("name").onkeyup = function() {
				//
				console.log(String.fromCharCode(event.keyCode));
			}
		</script>
	</body>
</html>
```



##### 1.5 状态改变事件

- onload() 页面加载完成事件
- onresize 窗口尺寸改变事件
- onchange 值改变事件

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
	</head>
	<body>
		<input type="text" name="" id="" value="" onchange="change()" />
		<script type="text/javascript">
			onload = function() {
				console.log("页面加载完成事件");
			}
			onresize = function() {
				console.log("尺寸改变了");
			}
			var change = function() {
				console.log('文本改变了');
			}
		</script>
	</body>
</html>

```



##### 1.6 事件绑定

- 事件属性绑定

    ```html
    <body onload="console.log('页面加载完成了事件')">
    	<input type="text" 
               onfocus="focus()"
               onblur="console.log('失去焦点')"/>
        <!-- js -->
    	<script type="text/javascript">
    		var focus = function() {
    			console.log('获取焦点了')
    		};
    	</script>
    </body>
    ```
    
    
    
- 动态绑定

    ```html
    <head>
        <script type="text/javascript">
            onload = function() {
                // 动态绑定需要onload，静态绑定不需要
                var nameId = document.getElementById("name");
            	nameId.onchange = function() {
                	console.log('文本改变了');
            	}
    			nameId.onfocus = function() {
                	console.log('获取焦点了');
            	}
            	nameId.onblur = function() {
                	console.log('失去焦点了');
            	}
            }
    	</script>
    </head>
    <body>
    	<input type="text" id="name" />
    </body>
    ```
    
    

##### 1.7 事件冒泡传递

​		如果在某一个范围由多个元素的事件需要响应，响应的顺序是从最底层往上层传递（类似旗袍从下往上）

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
        <script>
            function fn() {
                // 获取事件源
                var obj = event.target || event.srcElement;
                if(obj.nodeName=="INPUT") {
                    alert("input");
                }else if(obj.nodeName=="P") {
                    alert("p");
                }else {
                    alert("div");
                }
            }
        </script>
	</head>
	<body onload="console.log('页面加载完成事件')">
        <!-- 最后触发 -->
		<div onclick="alert('div click')">
            <!-- 再触发 -->
			<p onclick="alert('p click')">
                <!-- 先触发 -->
				<button type="button" onclick="alert('按钮 click')">按钮</button>
			</p>
		</div>
        <hr>
        <div onclick="fn()">
            <p>
                <input type="button" value="按钮">
            </p>
        </div>
	</body>
</html>
```

