# Nginx CBC (3): 真实的客户端IP

> 真实的客户端IP，能获取到吗？

## Why 获取客户端IP

 基于 IP 可以做很多事情，譬如限速乃至黑名单，可前提是要获取一个真实的客户端IP。

## 基本操作

按照上一节步骤，Nginx 的可执行文件位于目录`/usr/local/nginx/sbin`，为了便于后续执行，我们可以把路径添加到系统 PATH 变量中。

常用命令可以通过 `nginx -h` 查看。实验中主要使用到两个命令。

- `nginx -t`: 测试配置文件的合法性
- `nginx -s reload`: 重载配置文件

## 实验基本配置

后续还要做很多实验，提前规划规划目录。

主目录叫 JackTest，下面的 `ngingx.conf` 是最简化的配置文件，具体的各个实验配置，分别放在 `http.d` 以及 `tcp.d` 两个目录下面，通过 `include` 引入到配置文件中。

ps：4 层转发目前尚未涉及，先占上坑

```
JackTest
├── nginx.conf
├── http.d
│   └── default.conf
└── tcp.d
```

简化的配置文件如下，安装 默认的配置文件中删除了所有注释，并引入 `include`

```
worker_processes  1;

events {
    worker_connections  1024;
}

http {
    include       mime.types;
    default_type  application/octet-stream;
    sendfile      on;
    keepalive_timeout  65;

    include http.d/*.conf;
}
```

## 具体操作

1. 涉及使用 Nginx 的 `ngx_http_realip_module`，需要重新配置编译, `./configure --with-http_realip_module` ，程序换版。
2. 配置测试文件。
3. 使用 `curl` 进行测试

测试文件，`realip.conf`

```
server {
	listen 80;
	server_name localhost;

	set_real_ip_from  127.0.0.1;
	#real_ip_header X-Real-IP;
	real_ip_recursive off;
	#real_ip_recursive on;
	real_ip_header    X-Forwarded-For;

	location /{
		return 200 "remote_addr [$remote_addr]; XFF [$http_x_forwarded_for]\n";
	}
}
```

使用命令`curl -H 'X-Forwarded-For: 1.1.1.1,127.0.0.1' localhost` 进行测试

- 当 `real_ip_recursive off` 的时候，返回结果是 `remote_addr [127.0.0.1]; XFF [1.1.1.1,127.0.0.1]`
- 当 `real_ip_recursive on` 的时候，返回结果是 `remote_addr [1.1.1.1]; XFF [1.1.1.1,127.0.0.1]`

## 模块纪要

Nginx 的 `ngx_http_realip_module` 涉及3个命令

- `set_real_ip_from` : 一般设置为可信地址。
- `real_ip_header` : 从哪个 HTTP 头文件中获取客户端 ip。
- `real_ip_recursive` : 见上文例子。

## 生产级考虑

- 生产中，往往并不是 CVM 绑定公网 IP 对外服务，可能会使用到防火墙，CLB 等负载均衡产品，那么，可信地址应该设置为哪个呢？
- 复杂网络环境中的 IP 可信吗？