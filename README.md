websocket
============
websocket api，查看其他插件-> [Maven](http://search.maven.org/#search%7Cga%7C1%7Ccn.dreampie)

maven 引用  ${websocket.version}替换为相应的版本如:0.11

```xml
<dependency>
<groupId>cn.dreampie</groupId>
<artifactId>websocket</artifactId>
<version>${websocket.version}</version>
</dependency>
```

链接服务端
```javscript

var WebSocketSrv=  {
    connect: function(url) {
      var wsClient;
      if (!window.WebSocket) {
        $log.error('cannot open websocket');
        return;
      }
      wsClient = new WebSocket(url);
      wsClient.onopen = function(event) {
        return wsClient.readySate = true;
      };
      wsClient.onmessage = function(event) {
        var msg;
        msg = JSON.parse(event.data);
        return $log.info(msg);
      };
      wsClient.onclose = function(event) {
        wsClient.readySate = false;
        return $log.info("close websocket");
      };
      wsClient.onerror = function(event) {
        wsClient.readySate = false;
        return $log.error(event.data);
      };
      return wsClient;
    }
}

var wsClient=WebSocketSrv.connect("ws://localhost:9090/im/" + user.id);
```

服务器发送消息给客户端

```java

MessageServer.send(new Message(user.get("id").toString(), "message"));

```
