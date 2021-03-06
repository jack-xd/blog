# 公有云的爽与痛--痛篇

>玩儿了一年多公有云，投产版本顶过去5年！

## 那只叫Tom的猫

特殊时期，生产投产版本严格控制，兄弟正盼着这个月能少熬夜几天，结果Tom猫没有给机会。

> 2020年1月6日，国家信息安全漏洞共享平台（CNVD）收录了由北京长亭科技有限公司发现并报送的Apache Tomcat文件包含漏洞（CNVD-2020-10487，对应CVE-2020-1938）。攻击者利用该漏洞，可在未授权的情况下远程读取特定目录下的任意文件。目前，漏洞细节尚未公开，厂商已发布新版本完成漏洞修复。

诺，就是这只猫。
![tomcat](https://ss1.bdstatic.com/70cFvXSh_Q1YnxGkpoWK1HF6hhy/it/u=1966654476,3850892987&fm=26&gp=0.jpg)

风险提示邮件很快就收到了：`高危漏洞，限时反馈整改计划` 。

安全无小事，漏洞马上改。

系统管得多，效果就是好，兄弟趁机积累起丰富的撸猫经验，7.x 的撸一遍，8.x 的撸一遍；容器撸一遍，CVM 也撸一遍。

## 公有云的痛

**公有云的痛，痛在版本太多。**

1. 业务需求，自然不必说。公有云系统，敏捷迭代，更要灵活发布！
2. 公开漏洞，限时修复。

私有云年代，开放平台玩儿的是 Weblogic/Oracle，其它允许使用的中间件也有限，应用只需要管功能实现，下层中间件的漏洞升级数据中心/原厂都包了。

公有云年代，时髦的开源中间件都可以上，系统架构日渐向互联网迁移，安全相关的版本同样日渐增多。

**站在开发团队的角度，既要开发又要运维**（隔壁兄弟喊话，还有运营！）

兄弟掐指一算，玩儿了一年多公有云，投产版本顶过去5年！

**公有云的痛，痛在不够敏捷。**

1. 系统部署以 CVM 为单位；
2. 投产操作靠人肉逐台敲命令；
3. 容器化的应用，测试与生产的镜像仓库没有打通。（还是要手敲命令） 

## 怎么破

> 发展的问题，只能用发展来解决。

开源软件有漏洞，怎么破？

自己造轮子？这可能是大牛的操作，兄弟自问没有此等功力，因此，该用就用，该升级升级，关键是要让升级的操作简单、快捷。

- 开源中间件：公有云现有产品可以满足的，优先采用产品。（例如公有云提供了cos，就不必自己再搭一个FastDFS集群）。
- 开源依赖包：Maven父子工程，统一依赖管理。

业务需求多，怎么破？

- 分布式仓库，自动化：推广使用 git，替换现有的集中式 cc 仓库；推广使用流水线，替换现有的纯手工/半手工编译、测试、安全扫描、测试环境部署工作。
- 容器化：消除开发、测试、生产各个环境差异；减少在各个环境中“找不同”的无效动作。
- TDD：用测试用例框定需求范围，驱动开发。

我有一个梦想。

我梦想有一天，敏捷的理念成为团队的共识；

我梦想有一天，敏捷的实践在团队生根发芽。



