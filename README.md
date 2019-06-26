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
websocket是一个持久连接， 借用了http协议来完成一部分握手。

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
