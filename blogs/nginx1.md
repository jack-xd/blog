# Nginx CBC (1): 实验环境

> 大神agentzh：我希望帮助读者养成不随便听信别人现成的观点和陈述，而通过自己运行实例来验证的好习惯。

## 立个flag

玩儿公有云来，遵循物理部署推荐实践，使用 Nginx 的场景越来越多了，工作中愈发感到其强大与自身对其认识的不足。

在此立个 flag ，发个小愿，深入了解 Nginx。

所谓 Nginx CBC 就是 case by case 的意思，灵感来源于圈内大神 agentzh，实践是检验真理的唯一标准。

## 环境说明

环境方面，一方面考虑加快搭建速度，另外也是尽量模拟实际生产环境。涉及如下工具

- docker desktop 社区版。兄弟电脑上是 Mac 版2.1.0.3
- base 镜像采用 centos:7.4.1708
- Nginx 版本采用当下（2020/4）稳定版本 1.16.1 

> 那么就开始拔 flag 吧

## 基础环境准备

使用docker拉取 CentOS 7.4 镜像
```
docker pull centos:7.4.1708
docker run -itd --name nginx1 -p 8000:80 centos:7.4.1708
docker exec -it nginx1 bash
```

更换阿里源，提升速度。注意下面已经进入容器啦
```
rm -f /etc/yum.repos.d/* && cd /etc/yum.repos.d
curl -o /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo
curl -o /etc/yum.repos.d/epel.repo http://mirrors.aliyun.com/repo/epel-7.repo
yum clean all
yum makecache
```
- 新增的一台CentOS 7 ，直接 yum info nginx 是找不到 nginx 的安装包的。nginx 是作为 epel 源来发行，epel 即 Extra Packages for Enterprise Linux
- 国内使用阿里源，可以加快速度

## Nginx 安装

有两种方法，

- 直接使用官方预编译好的二进制包。这个最简单。两条命令，`yum-config-manager`+`yum install`。与实验无关，省略。

- CBC，要做实验嘛，自然是通过源码编译的方式。进行试验性定制。

**相关依赖安装**

```
yum -y install gcc gcc-c++ make #编译工具
yum -y install pcre-devel # pcre库，对正则的支持
yum -y install zlib-devel # http_gzip_module 需要的依赖
yum -y install openssl openssl-devel # http_ssl_module需要的依赖
```

**安装 Nginx**

```bash
curl -o nginx-1.16.1.tar.gz http://nginx.org/download/nginx-1.16.1.tar.gz
tar -zxvf nginx-1.16.1.tar.gz
cd  nginx-1.16.1
./configure 
make & make install
```

**启动与验证**

```bash
/usr/local/nginx/sbin
./nginx
```
本地打开浏览器，访问 localhost:8000/

## 生产级考虑

放到生产上跑的程序，与测试练习的要求不一样，可以思考一下下面问题：

- yum源是否用企业级的？
- 安装包该从哪里获取？可以用什么方式校验
- 非 root 用户运行 Nginx
- 应用日志采集，滚动