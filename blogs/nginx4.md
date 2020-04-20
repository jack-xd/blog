# Nginx CBC (4): 打印个Hello World

> 天啊，难道不是在第一篇讲 Hello World 么

## Hello World

打印一句 Hello World，Nginx 需要多少行命令呢？

```
server {
	listen 80;

	location / {
		set $foo "hello world";
		return 200 "$foo \n";
	}
}
```

这里我们使用到了 Nginx 标准模块 `ngx_http_rewrite_module` 的 `set` 和 `return` 指令。注意变量前面的 `$` 修饰符，在定义变量与使用变量的时候都需要。

在很多编程语言中，**变量**有点类似容器，这个容器是放**值**的，而所谓的值，往往有多种类型，例如整形，浮点型，字符型，字符串乃至数组，链表等复杂数据结构。

可是通过 `set` 指令，只能放一种类型，字符串。

下面是几个错误例子 

- `set $foo hello world; ` ，提示 invalid number of arguments
- 未定义，提示 unknown "foo" variable，根本无法启动 Nginx 进程。

## 变量的可见范围

试试这个配置。

```
server {
	listen 80;

	location / {
		set $foo "hello world";
		return 200 "$foo \n";
	}

	location /bar {
		return 200 "foo: [$foo] \n";
	}
}
```

很神奇，能够通过语法检查，拉起 Nginx 进程，但是访问 `/bar` 却取不到变量的值。

实际上，Nginx 中，变量的创建与赋值是发生在不同的阶段中的。因此

- 变量在 `location /bar` 中可以使用，它的可见范围是整个配置文件；
- 变量在 `location /bar` 没有被赋值，它的取值为空；
- 另外一点，变量对于各个请求是独立的。我们访问 `/` 之后，再访问 `/bar` 同样不会有值。

## 好用的 return

`return` 是模块 `ngx_http_rewrite_module` 的另外一个指令，注意到它可以直接返回 HTTP 的状态码。

- 301􏰅 永久重定向
- 302 临时重定向，禁止被缓存
- 303 临时重定向，允许改变方法，禁止被缓存
- 307 临时重定向，不允许改变方法，禁止被缓存
- 308 永久重定向，不允许改变方法

## 纪要

Nginx 的 `ngx_http_rewrite_module` ，使用到 2 个命令。

1. `set` : 设置字符串变量
  - Syntax:   `set** $variable value;` 
  - Default:  — 
  - Context:  `server`, `location`, `if`
2. `return` : 停止处理，直接向客户端返回
  - Syntax:   `return code [text] | code URL | URL;`
  - Default:  —
  - Context:  `server`, `location`, `if`

进一步到官网了解这个模块吧。
