# websocket-chartroom
分别使用了原生websocket和 socket.io实现一个聊天室雏形

socketio文件夹内为使用了socket.io完成的聊天室

### 技术栈
websocket ，socket.io

### 依赖
```
"devDependencies": {
    "express": "^4.15.2",
    "nodejs-websocket": "^1.7.2",
    "socket.io": "^2.2.0"
  }

```
在控制台
node wsServer.js
由于没有配置webpack.config.js 所以需要从html文件打开网页

### websocket和http的关系
两者有交集，其实websocket是一种新协议，和http协议没有多大关系，只是为了兼容浏览器的握手规范，可以说是对http协议的一种补充


### websocket是什么样的协议，有什么特点？
websocket是一个持久连接， 借用了http协议来完成一部分握手。他允许服务器主动向客户端发送数据

我们可以通过send（）向服务器发送数据，通过监听onmessage事件来就接受服务器返回的数据

建立连接的过程 客户度先向服务器发起一个http请求，和通常的http请求不一样，包含了一些附加的头信息，例如 upgrade：websocket 表示这是一个申请协议升级的请求




```
GET /chat HTTP/1.1
Host: server.example.com
Upgrade: websocket
Connection: Upgrade
Sec-WebSocket-Key: x3JJHMbDL1EzLkh9GBhXDw==
Sec-WebSocket-Protocol: chat, superchat
Sec-WebSocket-Version: 13
Origin: http://example.com


```


### 在websocket出现之前
ajax轮询和长轮询

ajax轮询原理：让浏览器隔几秒钟发送一次请求，询问服务器是否有新的数据

长轮询和ajax轮询有些类似，区别在于它是阻塞的，也就是说，客户端建立连接之后，没有新的数据，服务器一直不 返回response给客户端，直到有新数据，返回之后，客户端再建立连接

ajax轮询 需要服务器有很快的处理速度和资源。（速度）long poll 需要有很高的并发，也就是说同时接待客户的能力。（场地大小）

所以在这种情况下出现了，Websocket出现了。他解决了HTTP的这几个难题。首先，被动性，当服务器完成协议升级后（HTTP->Websocket），服务端就可以主动推送信息给客户端啦

就变成了这样，只需要经过一次HTTP请求，就可以做到源源不断的信息传送了。（在程序设计中，这种设计叫做回调，即：你有信息了再来通知我，而不是我傻乎乎的每次跑来问你 ）

这样的协议解决了上面同步有延迟，而且还非常消耗资源的这种情况。那么为什么他会解决服务器上消耗资源的问题呢？

其实我们所用的程序是要经过两层代理的，即HTTP协议在Nginx等服务器的解析下，然后再传送给相应的Handler（PHP等）来处理。简单地说，我们有一个非常快速的 接线员（Nginx） ，他负责把问题转交给相应的 客服（Handler） 。

本身接线员基本上速度是足够的，但是每次都卡在客服（Handler）了，老有客服处理速度太慢。，导致客服不够。Websocket就解决了这样一个难题，建立后，可以直接跟接线员建立持久连接，有信息的时候客服想办法通知接线员，然后接线员在统一转交给客户。

这样就可以解决客服处理速度过慢的问题了。


同时，在传统的方式上，要不断的建立，关闭HTTP协议，由于HTTP是非状态性的，每次都要重新传输 identity info （鉴别信息），来告诉服务端你是谁。

至于怎么在不支持Websocket的客户端上使用Websocket。。答案是： 不能

但是可以通过上面说的 long poll 和 ajax 轮询 来 模拟出类似的效果

[参考](https://www.zhihu.com/question/20215561)
