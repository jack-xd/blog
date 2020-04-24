# Nginx CBC (7): 对请求进行流控

> 能控管子不特别，还能控管子里面的水。

在上一篇文章中，经过实验，我们知道来 Nginx 能通过“连接”的维度进行流控，进一步地，它还可以通过“请求”的维度进行流控。

打个比方说就是，Nginx 能够管控从客户端伸过来的“水管”，还能管控“管子里面的水”。

我们先来重复上篇文章中，单个 server 的例子代码，这次采用 宿主机的 chrome 浏览器发送请求。

还记得在实验环境搭建中，`docker run -itd --name nginx1 -p 8000:80 centos:7.4.1708`，我们对端口进行了映射。

浏览器打开开发工具，关闭 cache，地址栏输入 `http://localhost:8000/` 。期望效果如下：

- 与上次一样，流控起效，页面返回速度很慢。在兄弟电脑中，耗时 16 s。
- 在等待返回的过程中，点地址栏旁边的叉叉停止，然后再重发一次请求。
- 第二次请求依然能够获取 `index.html` 页面的内容，没有被流控。

为什么没有被流控？这与之前使用 `curl` 有什么区别吗？

查看请求报文头，可以看到一行 `Connection: keep-alive` ，这就是传说中的 “长链接”。第二个请求复用了之前的连接，通过“连接”的维度进行流控自然就不起效果了。

## 请求流控

来看看请求流控的例子。

```
limit_req_zone $server_name zone=one:10m rate=1r/m;

server {
    listen       80;
    server_name  localhost;

    error_log logs/myerror.log info;

    #limit_req zone=one burst=3 nodelay;
    limit_req zone=one;

    location / {
        root   html;
        index  index.html index.htm;
    }
}
```

在这个配置中，我们按请求进行了流控，控制每分钟处理 1 个请求。注意此处仅仅为了实验演示，生产照搬的话会出大问题。

再次按照上文步骤进行实验，应该能观察到下面的效果。

- 第一次请求，页面瞬间返回了。（速度没有管控）
- 第二次请求，服务器返回 503。
- 如果隔上 1 分钟再次访问，会重复上面 2 步的效果。
- 观察日志，有这么一条。`[error] 56#0: *14 limiting requests, excess: 0.978 by zone "one", client: 172.17.0.1, server: localhost, request: "GET / HTTP/1.1", host: "localhost:8000"`

## 模块解析

这里我们使用到了 Nginx 标准模块 `ngx_http_limit_req_module` ，也许你已经发现了，这个模块中的命令与上一篇 `ngx_http_limit_conn_module` 很类似。

上面例子中，还有一句 `#limit_req zone=one burst=3 nodelay;` ，之前是注释掉了，还有两点需要说明。

1. 模块中采用了 leaky bucket 算法。`burst=3` 设置了1个大小为 3 的桶。
2. `nodelay` 指示对 burst 中的请求不再采用延时处理的做法，而是立即处理。

举例来说，

- 如果配置为 `limit_req zone=one burst=3;`， 那么第二个请求需要等上 1 分钟才会返回；
- 如果配置为 `limit_req zone=one burst=3 nodelay;` ，那么前 4 次请求都很快返回，但是第 5 次请求将返回 503。

类似的，这个模块中同样有 `limit_req_log_level` 以及 `limit_req_status` 这两条指令，效果与上一篇描述的一致。

## 进一步思考

如果同时配置基于“连接”以及“请求”两个维度的流控，会有什么效果呢？具体试试看吧。