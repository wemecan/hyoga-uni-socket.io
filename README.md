## @hyoga/uni-socket

项目源自：[weapp.socket.io](https://github.com/10cella/weapp.socket.io)，该项目作者已经两年没有维护，出现bug无法修复。

最近需要在uni-app中用到socket.io，遇到bug没有人修复很是头疼，所以基于weapp.socket.io新起一个项目。

如果该项目对您有帮助，可以给作者一个[star](https://github.com/AspenLuoQiang/hyoga-uni-socket.io)。

### 介绍

重写socket.io-client的engin.io-client处理件，h5依旧使用原生WebSocket，APP与小程序使用uni-app的WebSocket协议，所以h5端任然可以支持长轮询等方式，APP与小程序只能支持WebSocket协议。

### 安装

```
// 建议使用npm或yarn包形式引入以保证插件的更新迭代
npm i @hyoga/uni-socket.io --save
// yarn add @hyoga/uni-socket.io
```

### 使用

```
import io from '@hyoga/uni-socket.io';

const socket = io('your websocket path', {
  query: {},
  transports: [ 'websocket', 'polling' ],
  timeout: 5000,
});

socket.on('connect', () => {
  // ws连接已建立，此时可以进行socket.io的事件监听或者数据发送操作
  // 连接建立后，本插件的功能已完成，接下来的操作参考socket.io官方客户端文档即可
  console.log('ws 已连接');
  // socket.io 唯一连接id，可以监控这个id实现点对点通讯
  const { id } = socket;
  socket.on(id, (message) => {
    // 收到服务器推送的消息，可以跟进自身业务进行操作
    console.log('ws 收到服务器消息：', message);
  });
  // 主动向服务器发送数据
  socket.emit('send_data', {
    time: +new Date(),
  });
});

socket.on('error', (msg: any) => {
  console.log('ws error', msg);
});
```

更多使用方法，请参考[socket.io-client](https://github.com/socketio/socket.io-client)写法即可。

### API

参考[官网API](https://socket.io/docs/client-api/)

### 常见问题

1. 为什么没有聊天室示例代码？  

    本项目仅仅是将socket.io封装到uni-app使用，并非完整的聊天室。

2. Exception: ReferenceError: Can't find variable: window  

    hbuilder x 2.6.3版本中v3编译有bug，升级hbuilder x即可。

3. 真机运行TypeError: undefined is not an object (evaluating 'document.createElement')？  
    示例代码中：  

    ```
    const socket = io('your websocket path', {
      query: {},
      transports: [ 'websocket', 'polling' ],
      timeout: 5000,
    });
    ```
    不要漏写`transports: [ 'websocket', 'polling' ]`，如果没有指定协议，貌似socket.io会默认走`JSONP Polling`请求，导致报错。

### 加群

如果以上没有解决您的问题，可以在[github issue](https://github.com/AspenLuoQiang/hyoga-uni-socket.io/issues)上提交问题，并附上问题详细介绍以及相关代码和截图。或者加QQ群 207879913 与大家一起讨论。或者您对websocket或者IM感兴趣也可以加群讨论！！

<img src="https://cdn2.waikuaiba.cn/uploads/20200526/ef46f4aacc5776dafcf70985edc515f4.jpeg" >