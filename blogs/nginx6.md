# Nginx CBC (6): 对连接进行流控

> 防止把水池撑爆的一种方式，是把进水的管子弄小一点。

Nginx 其中一种广泛使用的方式是作为软负载均衡，即客户端请求先到达 Nginx，再路由到上游 upstream 服务器。拿 Java Web 应用来说，上游服务器往往是跑着 Weblogic 或者 Tomcat 等 Java 容器的 Ap，它们能承受的连接数大大低于 Nginx。

为了“保护“上游服务器，可以考虑在 Nginx 对连接进行流控。

## 单个 server 的例子

道理不多说，先来看一个简单的例子，Nginx 配置单个 server。

```
limit_conn_zone $server_name zone=perserver:10m;

server {
    listen       80;
    server_name  localhost;

    error_log logs/myerror.log info;

    limit_conn perserver 1;
    limit_conn_status 500;
    limit_conn_log_level  warn;
    limit_rate 50;

    location / {
        root   html;
        index  index.html index.htm;
    }
}
```

这个例子里面出现了很多之前没有讨论到的命令，没有关系，先把例子跑起来。

期待的效果如下：

1. 执行 `curl localhost` ，能看到服务器的返回内容特别慢，`index.html` 的内容几乎是逐行显示出来的；
2. 第一步成功之后，再次跑 `curl localhost` ，这次不用等待内容全部返回，按 `Ctrl + Z` 让当前进程切换到后台。然后再跑一次 `curl localhost`。

第 2 步实验成功的结果如下。

结果1 ： 返回了 500 的出错页面

```
<html>
<head><title>500 Internal Server Error</title></head>
<body>
<center><h1>500 Internal Server Error</h1></center>
<hr><center>nginx/1.16.1</center>
</body>
</html>
```

结果2 ：在 error.log 日志中有一条 `warn` 级别的拒绝记录。

```
2020/04/22 06:47:46 [warn] 64#0: *6 limiting connections by zone "perserver", client: 127.0.0.1, server: localhost, request: "GET / HTTP/1.1", host: "localhost"
```

## 实验解析

这里我们使用到了 Nginx 标准模块 `ngx_http_limit_conn_module` 中的几个指令，从实验结果可以看到，这个模块提供了不少流控功能，这些配置是对所有 worker 进程生效的。

- `limit_conn_zone` : 定义共享内存（包括大小），以及 key 关键字。
- `limit_conn` : 定义限制并发连接数。
- `limit_conn_log_level` : 定义当限制发生时的日志级别。
- `limit_conn_status` : 定义当限制发生时向客户端返回的错误码。

注意在上面实验中，使用到的流控方式是 `perserver` ，按照 `server` 维度进行控制。

## 多个 server 的例子

下面例子中，配置了两个 server ，验证是否按照我们设想，Nginx 是按 `server` 维度进行管控。

```
limit_conn_zone $server_name zone=perserver:10m;

server {
    listen       80;
    server_name  localhost;

    error_log logs/myerror.log info;

    limit_conn perserver 1;
    limit_conn_status 500;
    limit_conn_log_level  warn;
    limit_rate 10;

    location / {
        root   html;
        index  index.html index.htm;
    }
}

server {
    listen       8000;
    server_name  localhost;

    location / {
        root   html;
        index  index.html index.htm;
    }
}
```

期待效果

- 执行 `curl localhost` ，能看到服务器的返回内容特别慢，`index.html` 的内容几乎是逐行显示出来的；
- 执行 `curl localhost:8000` ，页面瞬间返回。

## 进一步思考

- 本文没有注明 4 条指令的 `Syntext`，`Default`，`Context`，大家知道去哪里查吗？
- `limit_conn_zone` 还可以通过什么维度进行控制？