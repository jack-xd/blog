# Nginx CBC (2): 热部署

> 优雅的热部署，而且是单机热部署

## Why 热部署

 生产服务总有升级的时候，Nginx 也一样，譬如说需要引入新模块，又或者安全等原因，需要更换版本。Nginx 能够做到优雅的热部署，而且是单机热部署。

话说小王刚按照上一个教程搭起来一台 Nginx，随即就收到安全的告警了。

> 存在泄漏服务器版本的风险

仔细一看，说的是这个。`curl -I localhost:8000`

[图片]

OK，马上修改。

操作步骤和放大象一样，总共分为三步

1. 修改源码，重新编译
2. 备份换版
3. 热部署

## 修改源码重新编译

定位源码文件 `src/http/ngx_http_header_filter_module.c`文件，找到下面两行

```c
static char ngx_http_server_string[] = “Server: nginx” CRLF;
static char ngx_http_server_full_string[] = “Server: ” NGINX_VER CRLF;
```

更改为

```c
static char ngx_http_server_string[] = “Server: JackTest” CRLF;
static char ngx_http_server_full_string[] = “Server: JackTest” CRLF;
```

回到源码根目录 `make`，注意这里与之前有区别，无需 `make install`。

## 备份换版

换版前备份老的可执行程序是一个关键时候可以救命的好习惯，回退不常有，可是万一真遇到需要回退呢?

搞不好就只能跑路了，哈哈。

```
cd /usr/local/nginx/sbin/
cp nginx nginx.old
cd /root/nginx-1.16.1/objs
cp nginx /usr/local/nginx/sbin/
```

## 热部署

1. 再次检查，比对可执行文件，例如大小比较一下

2. `kill -USR2 [old_pid]`，告诉老master进程，我们准备热部署升级了。

   这里是关键，Nginx 会使用新的可执行文件拉起 master 进程与 worker 进程；但是同时保留旧的 master 进程与 worker 进程。

3. `kill -WINCH [old_pid]` 停止老的 worker 进程，这时候就可以用上面的命令测试修改后的效果了。

4. `kill -HUP [old_pid]` 【可选】模拟回退处理。重新拉起老的 worker 进程。

5. `kill -QUIT [old_pid]` 升级完成，验证通过，告诉老 master 进程可以退休了。

## 进一步思考

- 实际生产中，很多人采用的办法是相对简单粗暴的 `pkill nginx` 再重新拉起新进程的方法，为了避免业务影响，只能熬到深夜动手，靠氪肝。
- 生产往往是多台 nginx 组成的集群，是否可以有自动化的方法。
- 扩展知识：Linux 的信号量