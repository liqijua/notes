## 1. http概述

​		（HyperText Transfer Protocol，超文本传输协议)，字符集是ISO-8859-1，这个字符集不支持中文，所以在传递数据时不会直接包含中文字符。

1. HTTP协议用于客户端和服务端之间的通信；
2. HTTP是基于请求和响应的；
3. HTTP是无状态的，协议对于发送过的请求或响应都不做持久化处理
4. HTTP工作在应用层
5. HTTP是基于TCP/IP协议的



## 2. HTTP1.1

- HTTP1.1支持持久连接，持久连接的特点是，只要任意一端没有明确提出断开连接，则保持TCP连接状态。

使用浏览器浏览一个包含多张图片的HTML页面时，在发送请求访问HTML页面资源的同时，也会请求该HTML页面里包含的其他资源。因此，每次的请求都会造成无谓的TCP连接建立和断开，增加通信量的开销。

<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/10.jpg" alt="10" style="zoom: 50%;"/>

- 持久连接

    持久连接的好处在于减少了TCP连接的重复建立和断开所造成的额外开销，减轻了服务器端的负载。

    <img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/11.jpg" alt="11" style="zoom: 50%;"/>

- 管线化

    持久连接使得多数请求以管线化（pipelining）方式发送成为可能。从前发送请求后需等待并收到响应，才能发送下一个请求。管线化技术出现后，不用等待响应亦可直接发送下一个请求。这样就能够做到同时并行发送多个请求，而不需要一个接一个地等待响应了。

    比如，当请求一个包含10张图片的HTML Web页面，与挨个连接相比，用持久连接可以让请求更快结束。而管线化技术则比持久连接还要快。请求数越多，时间差就越明显。

    <img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/line.jpg" alt="line" style="zoom:60%;"/>

    

## 3. 请求方法

### getpost区别

|            | GET                                       | POST                                                         |
| ---------- | ----------------------------------------- | ------------------------------------------------------------ |
| 浏览器回退 | 无害                                      | 再次提交请求                                                 |
|            | 被浏览器主动cache                         | 不会，除非手动设置                                           |
|            | 只能进行url编码                           | 支持多种编码方式                                             |
|            | 参数大小有限制                            | 没有限制                                                     |
|            | 只接受ASCLL字符                           | 没有限制                                                     |
|            | 参数暴露在url上                           | 在请求正文中                                                 |
|            | url传递参数                               | 请求正文中                                                   |
|            | GET请求参数会被完整保留在浏览器历史记录里 | POST中的参数不会被保留                                       |
|            | 产生一个TCP数据包                         | 产生两个TCP数据包(并不是所有浏览器都会发送两次包，Firefox就只发送一次) |





---

<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/methods.jpg" alt="methods" style="zoom:60%;"/>



CONNECT方法要求在与代理服务器通信时建立隧道，实现用隧道协议进行TCP通信。主要使用SSL（Secure Sockets Layer，安全套接层）和TLS（Transport Layer Security，传输层安全）协议把通信内容加密后经网络隧道传输。

## 4. 幂等性

幂等：如果一个请求不管执行多少次，其执行的副作用都是一样的，这个请求就是幂等的(如:get、put, delete, head)
非幂等:post（如相同url都是执行新增的操作）
POST和PUT很容易让人混淆，之前我总是简单的认为：POST表示创建资源，PUT表示更新资源；但是实际上它们都可用于创建和更新资源，只不过本质的差别就在于幂等性上。POST所对应的URI并非创建资源的本身，而是「资源的接收者」。例如：POST http://lindaidai.wang/articles的语义是在http://lindaidai.wang/articles下创建一篇帖子，HTTP响应中应包含帖子的创建状态以及帖子的URI。两次相同的POST请求会在服务器端创建两份资源，它们具有不同的URI，所以POST是「非幂等」的。
PUT方法所对应的URI是要创建或者更新「资源本身」。这点很容易让人误会它不是幂等的，但其实它是「幂等」的。例如：PUT http://lindaidai.wang/accout/321 的语义是创建或者更新ID为321的帖子。第一次PUT方法执行之后，其在服务器上生成的资源，不能被后续的PUT方法更改，所以对同一URI进行多次PUT的副作用和一次PUT是相同的，因而它是「幂等」的。
请求方法

HEAD：只从服务器获取文档的头部不获取资源，幂等操作

PUT：PUT 方法的语义就是让服务器用请求的主体部分来创建一个由所请求的 URL 命名的新文档。 如果那个文档已存在，就覆盖它，幂等操作

PATCH：对资源进行局部更新，非幂等操作

POST：通常用来向服务器发送表单数据。创建或更新资源，非幂等操作

TRACE：客户端发起一个请求时，这个请求可能要穿过路由器、防火墙、代理、网关等。每个中间节点都可能会修改原始的 HTTP 请求，TRACE 方法允许客户端在最终发起请求时，看看它变成了什么样子。幂等操作

## 5. cookie

​		Cookie技术通过在请求和响应报文中写入Cookie信息来控制客户端的状态。Cookie会根据从服务器端发送的响应报文内的一个叫做Set-Cookie的首部字段信息，通知客户端保存Cookie。当下次客户端再往该服务器发送请求时，客户端会自动在请求报文中加入Cookie值后发送出去。服务器端发现客户端发送过来的Cookie后，会去检查究竟是从哪一个客户端发来的连接请求，然后对比服务器上的记录，最后得到之前的状态信息。

1. 请求报文（无Cookie）

    ```http
    GET /imgage/ HTTP/1.1
    Host: baidu.com
    ```

2. 响应报文（服务端生成Cookie）

    ```http
    HTTP/1.1200 OK    
    Date: Thu, 12 Jul 2012 07:12:20 GMT    
    Server: Apache    
    Set-Cookie: sid=1342077140226724; path=/; expires=Wed, 10-Oct-12 07:12:20 GMT 
    Content-Type: text/plain; charset=UTF-8
    ```

3. 请求报文（携带Cookie信息）

    ```http
    GET /imgage/ HTTP/1.1
    Host: baidu.com
    Cookie: sid=123123123
    ```

    

## 6. HTTP报文

> 用于HTTP协议交互的信息被称为HTTP报文。请求端的HTTP报文叫做请求报文，响应端的叫做响应报文。

1. HTTP报文大致可分为报文首部和报文主体
    - 报文首部：服务端或客户端需处理的请求和响应的内容及属性
    - 报文主体：应被发送的数据



- General

```http
Referrer Policy	引用策略HTTP头管理在引用头中发送的哪些引用者信息应该包含在所发出的请求中	strict-origin-when-cross-origin
```



### 6.1 Http 请求报文

1. 请求行

    - 请求方法  请求URI  HTTP版本

    - 编码ASCLL

2. 请求头（消息头）
    - 编码ASCLL
    - 每个消息头结尾CRLF
        - CR ：回车，ASCLL值13
        - LF： 换行，ASCLL值10
    - 末尾有两个CRLF表示消息头结束

3. 请求正文（消息正文）  
    - 取决于请求头中的  Content-Type
        - Content-Type规定了body里面是什么，采用什么编码，如Content-Type: text/html; charset=UTF-8，表示body里的内容是html文件，采用UTF-8编码。Content-Type: application/x-www-form-urlencoded, 这是POST常用的消息类型，它表明body里放的是表单数据，采用的编码为urlencoded。
    - get请求没有消息正文，消息正文是一个二进制数据，是用于提交给服务器端的数据（比如表单）。

> 格式：

```
POST /index.html HTTP/1.1	
CRLF
Host: www.baidu.com
CRLF
Connection: keep-alive
CRLF
Content-Length: 100
CRLF
Content-type: application/x-www-form-urlencoded
CRLF
Cookie: ...
CRLF
CRLF
username: %CE%DB%B0
pwd: 12312
```



<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/image-20210825151655411.png" alt="image-20210825151655411" style="zoom:60%;" />



### 6.2 Http 响应报文

1. 状态行

2. 响应头

3. 响应正文
    - 相应正文是二进制数据

<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/image-20210825154436621.png" alt="image-20210825154436621" style="zoom:60%;" />



## 7. 状态码

<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/code.jpg" alt="code" style="zoom:80%;" />

- 200  OK  请求成功

    ​		表示从客户端发来的请求在服务器端被正常处理了。

- 204  No Content  请求成功

    ​		代表服务器接收的请求已成功处理，但在返回的响应报文中不含实体的主体部分。另外，也不允许返回任何实体的主体。比如，当从浏览器发出请求处理后，返回204响应，那么浏览器显示的页面不发生更新。一般在只需要从客户端往服务器发送信息，而对客户端不需要发送新信息内容的情况下使用。

- 206 Partial Content

    ​		表示客户端进行了范围请求，而服务器成功执行了这部分的GET请求。响应报文中包含由Content-Range指定范围的实体内容。使用场景为HTTP分块下载和断点续传。

- 301 Moved Permanently  永久重定向

    ​		永久性重定向。该状态码表示请求的资源已被分配了新的URI，以后应使用资源现在所指的URI。也就是说，如果已经把资源对应的URI保存为书签了，这时应该按Location首部字段提示的URI重新保存。

- 302 Found  临时重定向，

    ​		和301不同，它表示请求的资源临时被移动到了别的URI上，因为是暂时的，所以不会被缓存。

- 303 See Other  临时重定向

    ​		该状态码表示由于请求对应的资源存在着另一个URI，应使用GET方法定向获取请求的资源。303状态码和302 Found状态码有着相同的功能，但303状态码明确表示客户端应当采用GET方法获取资源，这点与302状态码有区别。

    ​		当301、302、303响应状态码返回时，几乎所有的浏览器都会把POST改成GET，并删除请求报文内的主体，之后请求会自动再次发送。301、302标准是禁止将POST方法改变成GET方法的，但实际使用时大家都会这么做。

- 304 Not Modefied  

    ​		该状态码表示客户端发送附带条件的请求[插图]时，服务器端允许请求访问资源，但因发生请求未满足条件的情况后，直接返回304 Not Modified（服务器端资源未改变，可直接使用客户端未过期的缓存）。304状态码返回时，不包含任何响应的主体部分。304虽然被划分在3XX类别中，但是和重定向没有关系。

- 307 Temprary Redirect：临时重定向

    ​		临时重定向。该状态码与302 Found有着相同的含义。尽管302标准禁止POST变换成GET，但实际使用时大家并不遵守。307会遵照浏览器标准，不会从POST变成GET。但是，对于处理响应时的行为，每种浏览器有可能出现不同的情况。

    ​		但是比302更加明确，重定向的请求方法和实体都不允许变动。场景例如：HSTS协议，强制客户端使用https建立连接，比如你的网站从HTTP升级到了HTTPS，而你还是通过http://xxx访问的话，就会返回307 Internal Redirect。

- 400 Bad Request

    ​		请求报文中存在语法错误，但是没有具体指出是哪里。

- 401 Unauthorized

    ​		需要有通过HTTP认证的认证信息或者表示用户认证失败。

- 403 Forbidden：请求资源被拒绝

    ​		该状态码表明对请求资源的访问被服务器拒绝了。服务器端没有必要给出拒绝的详细理由，但如果想作说明的话，可以在实体的主体部分对原因进行描述，这样就能让用户看到了。未获得文件系统的访问授权，访问权限出现某些问题（从未授权的发送源IP地址试图访问）等列举的情况都可能是发生403的原因。

- 404 Not Found  请求资源未找到

    ​		表示没在服务器上找到相应的资源。

- 500 Internal Server Error  服务器内部错误

    ​		该状态码表明服务器端在执行请求时发生了错误。也有可能是Web应用存在的bug或某些临时的故障。

- 501 Not Implemented：表示客户端请求的功能还不支持

- 502 Bad GateWay：服务器自身是正常的，但是代理服务器无法获取到合法响应

- 503 Service Unavailable

    ​		该状态码表明服务器暂时处于超负载或正在进行停机维护，现在无法处理请求。如果事先得知解除以上状况需要的时间，最好写入Retry-After首部字段再返回给客户端。



## 8. 代理服务器

缓存是指代理服务器或客户端本地磁盘内保存的资源副本。利用缓存可减少对源服务器的访问，因此也就节省了通信流量和通信时间。缓存服务器是代理服务器的一种，并归类在缓存代理类型中。换句话说，当代理转发从服务器返回的响应时，代理服务器将会保存一份资源的副本。

缓存服务器的优势在于利用缓存可避免多次从源服务器转发资源。因此客户端可就近从缓存服务器上获取资源，而源服务器也不必多次处理相同的请求了。

> 为什么要使用Web缓存？

- 降低客户端的请求响应时间
- 可以减少一个机构内部网络和Internet接入链路上的流量
- 互联网大量采用了缓存：可以使较弱的 ICP 也能够有效提供内容

### 8.1 缓存有效期

<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/cache2.png" alt="cache2" style="zoom: 67%;" />



## 8. HTTP1.1首部字段

- 通用首部字段（请求报文和响应报文都会使用的首部）

<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/head1.jpg" alt="code" style="zoom: 67%;" />

- 请求首部字段（从客户端向服务器端发送请求报文时使用的首部。补充了请求的附加内容、客户端信息、响应内容相关优先级等信息）

<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/head3.jpg" alt="head3" style="zoom: 67%;" />

- 响应首部字段（从服务器端向客户端返回响应报文时使用的首部。补充了响应的附加内容，也会要求客户端附加额外的内容信息）

<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/head2.jpg" alt="head2" style="zoom: 67%;" />

- 实体首部字段（针对请求报文和响应报文的实体部分使用的首部。补充了资源内容更新时间等与实体有关的信息）

<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/head4.jpg" alt="head4" style="zoom: 67%;" />



### 8.1 通用首部字段

通过指定首部字段Cache-Control的指令，就能操作缓存的工作机制。

```
Cache-Control: private, max-age=0,  no-cache
```



## 9. Cookie首部字段

<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/cookie1.jpg" alt="cookie1" style="zoom: 67%;" />

```
Set-Cookie: status=enable; expires=Tue, 05 Jul 2011 07:26:31 GMT; path=/; domain=.hackr.jp;
```

- Set-Cookie字段的属性

<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/cookie2.jpg" alt="cookie2" style="zoom: 67%;" />

```
Cookie: status=enable
```

首部字段Cookie会告知服务器，当客户端想获得HTTP状态管理支持时，就会在请求中包含从服务器接收到的Cookie。接收到多个Cookie时，同样可以以多个Cookie形式发送。



## 10. HTTPS

### 10.1 HTTP缺点

1. 通信使用明文（不加密），内容可能会被窃听；

    - 通信加密

    ​		HTTP协议中没有加密机制，但可以通过和SSL（Secure Socket Layer，安全套接层）或TLS（Transport Layer Security，安全传输层协议）的组合使用，加密HTTP的通信内容。用SSL建立安全通信线路之后，就可以在这条线路上进行HTTP通信了。与SSL组合使用的HTTP被称为HTTPS（HTTP Secure，超文本传输安全协议）或HTTP over SSL。

    - 内容加密

2. 不验证通信方的身份，因此有可能遭遇伪装；

    - DoS攻击（拒绝服务攻击）
    - 可以通过证书来验证，虽然使用HTTP协议无法确定通信方，但如果使用SSL则可以。SSL不仅提供加密处理，而且还使用了一种被称为证书的手段，可用于确定方。证书由值得信任的第三方机构颁发，用以证明服务器和客户端是实际存在的。另外，伪造证书从技术角度来说是异常困难的一件事。所以只要能够确认通信方（服务器或客户端）持有的证书，即可判断通信方的真实意图。

3. 无法证明报文的完整性，所以有可能被篡改；

​		为了有效防止这些弊端，有必要使用HTTPS。SSL提供认证和加密处理及摘要功能。仅靠HTTP确保完整性是非常困难的，因此通过和其他协议组合使用来实现这个目标。

### 10.2 HTTPS

​		HTTPS并非是应用层的一种新协议。只是HTTP通信接口部分用SSL（Secure Socket Layer）和TLS（Transport Layer Security）协议代替而已。通常，HTTP直接和TCP通信。当使用SSL时，则演变成先和SSL通信，再由SSL和TCP通信了。

<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/ssl.jpg" alt="ssl" style="zoom: 67%;" />





## 11. cookieSessionToken

<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/wps1-1679463806007-2.jpg" alt="img" style="zoom: 80%;" />

<img src="https://tyimages.oss-cn-shanghai.aliyuncs.com/typoraImgs/image-20230216153017589.png" alt="image-20230216153017589" style="zoom: 67%;" />



## cookie和session的区别  

​		第一次执行getSession()时，会创建一个新的session对象，保存在服务器内存中同时会给客户端以cookie形式返回一个sessionId，之后同一个客户端再次发出请求时会带着这个sessionId；当再次调用getSession()时，会通过带着的sessionId去服务器内存中找到对应的session对象，此时session对象和第一次创建的session对象时同一个这个保存在同一个session对象中的数据可以共享给这个客户端的任何一次请求。

​		如果客户端禁用了cookie，那么session也会失效，这时候可以使用URL重写。

1. cookie数据保存在客户端，成本低；session数据保存在服务端，成本高，影响服务器性能；
2. cookie能长时间保存；session只能保存在这次会话的数据；
3. cookie安全性差，session安全性较好；
4. cookie只能保存字符串，session保存任何java语言类型的对象；
5. cookie大小限制4k，session没有大小限制；



|              | Cookie                                  | Session                                                      | Token                                       |
| ------------ | --------------------------------------- | ------------------------------------------------------------ | ------------------------------------------- |
| 数据存储位置 | 客户端                                  | 服务端                                                       | 客户端                                      |
| 数据保存时间 | 长时间保存                              | 一次会话                                                     | 一次会话                                    |
| 应用场景     | 记住密码，自动登录；记录用户浏览数据... | 判断用户是否登录...                                          |                                             |
| 关系         |                                         | 第一次访问服务器会返回一个名为SessionID的Cookie，下次访问会携带sessionId | 用解析token的计算时间换取 session的存储空间 |



