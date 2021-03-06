## 1.http和tcp协议
- TCP链接
::: tip TCP
1. 手机能够使用联网功能是因为手机底层实现了TCP/IP协议，可以使手机终端通过无线网络建立TCP连接。TCP协议可以对上层网络提供接口，使上层网络数据的传输建立在“无差别”的网络之上。<br>
2. 建立TCP链接需要三次握手
    1. 客户端发送syn包(syn=j)到服务器，并进入SYN_SEND状态，等待服务器确认；
    2. 服务器收到syn包，必须确认客户的SYN（ack=j+1），同时自己也发送一个SYN包（syn=k），即SYN+ACK包，此时服务器进入SYN_RECV状态；
    3. 客户端收到服务器的SYN＋ACK包，向服务器发送确认包ACK(ack=k+1)，此包发送完毕，客户端和服务器进入ESTABLISHED状态，完成三次握手。
3. 完成三次握手，客户端与服务器才正式开始传送数据
:::
- HTTP链接
::: tip HTTP
1.  HTTP协议即超文本传送协议(Hypertext Transfer Protocol )，是Web联网的基础，也是手机联网常用的协议之一，HTTP协议是建立在TCP协议之上的一种应用。
2. 特点：客户端发送的每次请求都需要服务器回送响应，在请求结束后，会主动释放连接
    1. 在HTTP 1.0中，客户端的每次请求都要求建立一次单独的连接，在处理完本次请求后，就自动释放连接。
    2. 在HTTP 1.1中则可以在一次连接中处理多个请求，并且多个请求可以重叠进行，不需要等待一个请求结束后再发送下一个请求。
3. 由于HTTP在每次请求结束后都会主动释放连接，因此HTTP连接是一种“短连接”
:::
- 相互关系
::: tip 相互关系
1. http是要基于TCP连接基础上的
    1. TCP就是单纯建立连接，不涉及任何我们需要请求的实际数据，简单的传输。
    2. http是用来收发数据，即实际应用上来的。
    3. 过程：从传输层，先说下TCP连接，我们要和服务端连接TCP连接，需要通过三次连接，包括：请求，确认，建立连接。即传说中的“三次握手协议”。
        简单就是:请求，确认，连接
2. 从实际上的数据应用来说http
    在前面客户端和应用服务器建立TCP连接之后，就需要用http协议来传送数据了，HTTP协议简单来说，还是请求，确认，连接。
3. TCP是底层通讯协议，定义的是数据传输和连接方式的规范
    1. HTTP是应用层协议，定义的是传输数据的内容的规范
    2. HTTP协议中的数据是利用TCP协议传输的，所以支持HTTP也就一定支持TCP    
    3. HTTP支持的是www服务,而TCP/IP是协议 
    4. 它是Internet国际互联网络的基础。TCP/IP是网络中使用的基本的通信协议。 
    5. TCP/IP实际上是一组协议，它包括上百个各种功能的协议，如：远程登录、文件传输和电子邮件等，而TCP协议和IP协议是保证数据完整传输的两个基本的重要协议。通常说TCP/IP是Internet协议族，而不单单是TCP和IP。
:::
<a href='https://www.cnblogs.com/wx-1996/p/10685576.html' target='_blank'>HTTP与TCP的区别和联系</a>

## 2.HTTP状态码
::: tip HTTP状态码
200 正常 <br>
302 表示临时性重定向。访问一个Url时，被重定向到另一个url上。<br>
401请求需要认证<br>
403请求对应资源禁止访问<br>
404服务器无法找到对应资源<br>
502网关错误<br>
504网关超时<br>
:::
## 3.https和http是的区别
- HTTP
::: tip HTTP
超文本传输协议，明文传输，不安全
:::
- HTTPS
::: tip HTTPS
1. https在http的基础上加入了SSL协议，SSL依靠证书来验证服务器的身份，并在浏览器和服务器之间加密<br>
2. https是由SSL+http协议构建的可进行加密传输，身份认证的网络协议<br>
3. 因为http是明文传输未加密，不安全，所以设计了SSL协议用于对http协议传输进行加密<br>
:::
::: tip HTTPS工作流程
1. 客户端浏览器访问服务器，建立SSL加密链接
2. 服务器收到请求后，将证书信息(包含公钥)返回给客户端浏览器 
3. 客户端拿到公钥，产生对称秘钥，使用公钥对对称秘钥进行加密
4. 客户端将加密后的对称秘钥发送给服务器
5. 服务器利用自己的私钥解密出会话秘钥
6. 服务器利用会话秘钥加密进行客户端通信
:::
::: tip HTTPS优点
1. 使用https可以认证用户和服务器，确保数据发送到正确的客户机和服务器
2. https使用SSL+http构建的可加密传输、身份认证的网络协议，比http更加安全
3. https是现行最安全的解决方案，增加了中间人的盗取成本
:::
::: tip HTTPS缺点
1. https协议握手比较费时，会使页面加载时间延长
2. https的缓存不如http高效，增加数据开销
3. SSL协议需要成本费用
4. SSL需要绑定IP，不能在同一个IP绑定多个域名
5. https加密范围有限
:::
- HTTP和HTTPS区别
::: tip HTTP和HTTPS区别
1. https协议需要ca申请证书
2. http是超文本传输协议，是明文传输，https是具有安全性SSL加密传输协议，可进行加密传输，身份认证的网络协议，比http更安全
3. http和https使用的不同的连接方式，用的端口也不一样，http默认端口是80,https默认端口是443
:::
<a href='https://www.jianshu.com/p/97af35e81912' target='_blank'>HTTP与HTPPS的区别</a>
## 4.一个页面从输入URL到页面加载显示完成，这个过程中都发生了什么？
::: tip 步骤
1. 浏览器开启一个线程来进行处理请求，同时在远程开启DNS查询IP地址
2. 浏览器与远程服务器通过TCP进行三次握手简历TCP/IP链接
3. TCP建立链接，浏览器向远程服务器发送应用请求，服务器返回相应资源，值为200的状态码表示正确相应
4. 此时web服务器提供资源服务，客户端进行下载资源
5. 页面开始渲染DOM，JS根据DOM API操作DOM,执行事件绑定等，页面显示完成。
:::




