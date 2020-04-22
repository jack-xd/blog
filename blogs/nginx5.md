# Nginx CBC (5): 继承与内部跳转

> 什么？继承？难道也是面向对象么？

## 指令继承规则

在上一篇中学习到的`set` 指令，如果有多个地方设置，会出现什么效果呢？

```
server {
	listen 80;
	set $foo "1";

	location / {
		set $foo "2";
		return 200 "$foo \n";
		set $foo "3";
	}
}
```

上面的例子中，我们对变量设置了 3 次，

- 直接访问，输出的结果是 2 ；
- 把 `set $foo "2";` 这行添加注释，输出结果是 1；

得到一个结论，有的指令是可以“覆盖”的，覆盖的规则是：

- 子配置不存在时，直接使用父配置块；
- 子配置存在时，直接覆盖父配置块；

需要注意的是，指令可以分两类，覆盖的规则有所不同：

- 值指令，存储配置项的值，一般可以覆盖。例如 `set` `root` `access_log` `gzip` 等；
- 动作指令，指定行为，一遍不可以覆盖。例如 `rewrite` `proxy_pass` 等。

Nginx中， HTTP 模块的嵌套规则是这样的。

```
main
http {
	upstream { ... }
	split_clients { ... }
	map { ... }
	geo { ... }
	server {
		if() { ... }
		location {
			limit_except { ... }
		}
		location {
			location { ... }
		}
	}
}
```

## 内部跳转

变量的生命周期，是否与它所在的配置块相关呢？再来看一个例子。

```
server {
	listen 80;

	location / {
		set $foo "hello world";
		rewrite ^ /bar;
	}

	location /bar {
		return 200 "$foo \n";
	}
}
```

这里使用到了 Nginx 标准模块 `ngx_http_rewrite_module` 的 `rewrite` 指令，让请求进行了一个“内部跳转”。

所谓内部跳转，就是在处理请求的过程中，从一个 location 跳转到另一个 location，区别于利用 HTTP 状态码 30x 所进行的“外部跳转“。

既然是内部跳转，有如下结果：

- `curl localhost/123` , 先匹配 `location /`，对变量进行了赋值，能够输出 `Hello world`；
- `curl localhost/bar`，匹配到 `location /bar`，变量未赋值，输出结果为空。

从上面的实验，我们得到一个结论，Nginx 变量的生命周期是与当前处理的请求绑定的，而与 location 无关。

## rewrite 指令

上面的例子中，还有一条语句值得注意，`rewrite ^ /bar`。

来看看它的使用方法

- Syntax ： rewrite regex replacement [flag];
- Default : --
- Context : server, location, if

这个指令可以将 regex 指定的 url 替换成 replacement 这个新的 url。（可以使用强大的正则表达式）

flag 是可选的，指定后的效果是对替换后的 url 按指定的方式进行处理。

-  `--last` : 用 replacement 这个 url 进行新的 location 匹配；
- `--break` : 停止当前脚本指令的执行；
- `--redirect` : 返回 302 重定向；
- `--permanent` : 返回 301 重定向。