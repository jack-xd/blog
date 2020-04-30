# Nginx CBC (8): 虚拟主机

> 什么人会用 Nginx？可能是穷人。

在之前流控的实验中，我们测试过多个 server 的情况，是通过 `listen` 指令监听不同端口实现的。其实，仅仅通过 `server_name` 指令，就能达到单个 Nginx 配置多个虚拟主机的需求。

毫不夸张的说，Nginx 可以说是穷人挚友啊。

## 重新认识 server_name

如果要找官方文档的话，`server_name` 是在 `ngx_http_core_module` 中定义的。来看看它的规则：

- Syntax：server_name name ...;
- Default：server_name "";
- Context：server

注意到指令后可以跟多个域名，其中第 1 个是主域名。怎么理解主域名这个概念呢，请看如下例子。

完成本次 CBC 实验，需要首先配置 `hosts` 文件。

```
127.0.0.1 primary.jack.com
127.0.0.1 second.jack.com
```

接下来是我们熟悉的 Nginx 配置文件。

```
server {
	server_name primary.jack.com second.jack.com;
	server_name_in_redirect off;

	return 302 /redirect;
}
```

修改 `hosts` 文件，让`primary.jack.com` 以及 `second.jack.com` 都指向本地。进入如下测试，`curl -I second.jack.com` ：

- 当 `server_name_in_redirect` 配置为默认的 `off` 时，返回的结果是 `Location: http://second.jack.com/redirect` 。
- 当 `server_name_in_redirect` 配置为 `on` 的时候，将返回主域名，浏览器下一步会尝试通过主域名请求对应的资源。

通过上述实验，可以看到，`server_name_in_redirect` 指令的效果，就是是否启用主域名。

## 多面手server_name

`server_name` 后面配置的域名，不光光可以写像上面例子中完全精确匹配的，还有其它多种用法，可以说，它是一个多面手。

1. 支持泛域名。可以把通配符 `*` 写在最左或者最右，但是写在中间的话会报错，避免这样的写法 `primary.*.com`。
2. 支持正则表达式，使得配置更灵活优雅。ps：Nginx 中用到正则要在前面加 `~`，这是个通用的规则。
3. 正则表达式加小括号创建变量。这块用法比较灵活，后续详细说。
4. 可以用 `_` 来指定匹配所有域名。
5. `.jack.com` 可以用于同时匹配 `jack.com` 以及`*.jack.com`。

## 虚拟主机的匹配顺序

既然能同时配置多个虚拟主机，那必然有一个匹配的顺序，确保当多个 server 配置块都匹配到请求的域名时，请求会经由特定的虚拟主机处理。匹配顺序如下：

1. 精确匹配；
2. 通配符在前的泛域名；
3. 通配符在后的泛域名；
4. 多个正则表达式匹配都能匹配的，第一个成功匹配的进行处理。

来看下面例子。

```
server {
	server_name *.jack.com;

	return 200 "primary \n";
}

server {
	server_name primary.jack.*;
	listen 80 default;
	
	return 200 "second \n";
}
```

注意到即使通过 `default` 也不能改变匹配的顺序。

再来看一个正则的匹配顺序例子。

```
server {
	server_name ~^primary.*;

	return 200 "primary \n";
}

server {
	server_name ~^primary.jack.*;
	
	return 200 "second \n";
}
```

## 进一步思考

- 重定向能够用在什么应用场景？
- 你是怎么使用虚拟主机的呢？