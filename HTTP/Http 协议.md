### 一、Http 的特点

1. **简单快速**：客户端向服务器发送请求时，只需传送请求方法和路径。请求方法常用的有 GET、HEAD、PUT、DELETE、POST。每种方法规定了客户与服务器联系的类型不同。由于 HTTP 协议简单，使得 HTTP 服务器的程序规模小，因而通信速度很快
2. **灵活**：HTTP 允许传输任意类型的数据对象
3. **无连接**（http/1.0）：无连接的含义是限制每次连接只处理一个请求。服务器处理完客户的请求，并收到客户的应答后，即断开连接。采用这种方式可以节省传输时间
4. **无状态**（http/0.9）：HTTP 协议是无状态的，HTTP 协议自身不对请求和响应之间的通信状态进行保存。任何两次请求之间都没有依赖关系
5. **持久连接**（http/1.1）：只要任意一端没有明确提出断开连接，则保持 TCP 连接状态



### 二、Http 报文

Http 报文包括**请求报文**和**响应报文**两大部分

- 请求报文：由请求行（request line）、请求头（header）、空行和请求体四个部分组成
- 响应报文：由状态行、响应头部、空行和响应体四个部分组成



请求报文：

1. 请求行，用来说明请求类型，要访问的资源以及所使用的 HTTP 版本

```js
POST  /chapter17/user.html HTTP/1.1
```

2. 请求头由关键字/值对组成，每行一对，关键字和值用英文冒号 “:” 分隔

请求头部通知服务器有关于客户端请求的信息。它包含许多有关的客户端环境和请求正文的有用信息。其中比如：

- Host：表示主机名，虚拟主机
- Connection：HTTP/1.1 增加的，使用 keepalive，即持久连接，一个连接可以发多个请求
- User-Agent：请求发出者，兼容性以及定制化需求

3. 最后一个请求头之后是一个空行，这个行非常重要，它表示请求头已经结束，接下来的是请求正文
4. 请求体，可以承载多个请求参数的数据



### 三、HTTP 请求方法

- GET 请求指定的页面信息，并返回实体主体
- HEAD 类似于 get 请求，只不过返回的响应中没有具体的内容，用于获取报头
- POST 向指定资源提交数据进行处理请求（例如提交表单或者上传文件）。数据被包含在请求体中
- PUT 从客户端向服务器传送的数据取代指定的文档内容
- DELETE 请求服务器删除指定的内容



### 四、GET 与 POST 区别

- GET 在浏览器回退时是无害的，而 POST 会再次提交请求
- GET 请求会被浏览器主动缓存，而 POST 不会，除非手动设置
- GET 请求参数会被完整保留在浏览器历史记录里，而 POST 中的参数不会被保留
- GET 请求在 URL 中传送的参数是有长度限制的，而 POST 没有限制
- GET 参数通过 URL 传递，POST 放在 Request body 中



### 五、Http 状态码

状态代码有三位数字组成，第一个数字定义了响应的类别，共分五种类别:

- 1xx：指示信息 -- 表示请求已接收，继续处理
- 2xx：成功 -- 表示请求已被成功接收、理解、接受
- 3xx：重定向 -- 要完成请求必须进行更进一步的操作
- 4xx：客户端错误 -- 请求有语法错误或请求无法实现
- 5xx：服务器端错误 -- 服务器未能实现合法的请求



### 六、持久连接

HTTP 协议的初始版本中，每进行一次 HTTP 通信就要断开一次 TCP 连接，当请求数增多时，每次的请求都会造成无谓的 TCP 连接建立和断开，增加通信量的开销

持久连接的特点：**只要任意一端没有明确提出断开连接，则保持 TCP 连接状态**

在 HTTP/1.1 中，所有的连接默认都是持久连接，但在 HTTP/1.0 内并未标准化。除了服务器端，客户端也需要支持持久连接



### 七、管线化

从前发送请求后需等待并收到响应，才能发送下一个请求

而管线化技术**能够同时并行发送多个请求，而不需要一个接一个地等待响应了**。通俗地讲，请求打包一次传输过去，响应打包一次传递回来。管线化的前提是在持久连接下

**与挨个连接相比，用持久连接可以让请求更快结束。 而管线化技术则比持久连接还要快**

客户端需要请求这十个资源：

- 以前的做法是，在同一个 TCP 连接里面，先发送 A 请求，然后等待服务器做出回应，收到后再发出 B 请求，以此类推
- 管道机制则是允许浏览器同时发出这十个请求，但是服务器还是按照顺序，先回应 A 请求，完成后再回应 B 请求



