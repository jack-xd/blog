# 【学习笔记】部署与发布分离 | 落地篇13

> 部署和发布这两个概念，经常会被混用，但严格来说，部署和发布代表两种不同的实践。

**部署是一组技术实践**，表示通过技术手段，将本次开发测试完成的功能实体（比如代码、二进制包、配置文件、数据库等）应用到指定环境的过程，包括开发环境、预发布环境、生产环境等。

**部署的结果是对服务器进行变更**，但是这个变更结果不一定对外可见。

发布，**更偏向一种业务实践**，也就是将部署完成的功能正式生效，对用户可见和提供服务的过程。

作者本篇专栏的题目是部署管理，而在Devops理念指引下的部署管理，落脚点是在于实现一种低风险的业务发布策略。

> 要在保障**一定的质量水平**的前提下，尽量加快发布节奏，并通过**低风险发布手段**，以及**线上测试和监控能力**，尽早地发现问题，并以一种最简单的手段来**快速恢复**。

## 一定的质量水平

关键词，**问题分级**。

作者举了一个例子，造卫星的公司追求软件质量可以做到不计成本；但是互联网业务却偏好快速迭代。

**快速迭代的本质是默认软件会出问题，而且允许软件出问题。**只要完成严重问题的修复即可发布，低级别的问题可以在后续的众测和灰度的环节继续处理。

## 低风险的发布手段

**蓝绿部署**

- 为应用准备两套一模一样的生产环境，只有一套环境提供线上服务。
- 应用版本部署在没有提供线上服务的环境中，进行上线前验证。
- 服务发布仅通过简单的流量环境切换进行。



**灰度发布**

又名金丝雀发布，就是**采用一种渐进式的滚动升级来完成整个应用的发布过程**。

对于移动端应用来说，最难搞定的是 IOS 平台。采用灰度发布的过程如下。

- 公司的内部用户可以自行下载安装企业包
- 通过官方的 Testflight 平台对外开启灰度
- 灰度指标符合预期后，再开启全量用户升级

作者提出，不少应用采用特性开关，控制不同用户看到不同功能，实践中容易被苹果判断为欺诈，需要慎用。

另外，兄弟理解，灰度发布是有一段不短的时间过程的，目前实践中使用的“应用轮起”，不是灰度发布，而是一种保证应用服务不中断的部署方式。

作者还提到了**暗部署**，兄弟理解偏向一种业务选择的线上验证方法，类似A/B测试。

## 线上测试和监控

> 测试环境就像动物园，你能在里面看到各种野生动物，它们都活得都挺好的；
>
> 生产环境就像大自然，你永远无法想象动物园里的动物回到大自然之后会有什么样的行为，它们面临的就是一个完全未知的世界。

线上测试！线上测试！线上测试！

记忆中，线上测试都是配合外部来进行的，例如双十一；自家的系统貌似没有说自己做线上测试的。

监控方面，除了现有的系统成功率、业务成功率，应该更向前一步，能够**监控业务效果**。

因为业务成功率高，往往与业务效果佳不是一致的，举个极端的例子，一支没有访问的交易，成功率是100%，但是却业务效果是0。

## 快速恢复

对问题进行分析定位后，你可以有两种选择：**向前修复和向后回滚**。

向前修复就是快速修改代码并发布一个新版本上线，向后回滚就是将系统部署的应用版本回滚到前一个稳定版本。

无论选择哪一种，考验的都是自动化的部署流水线和自动化的回滚能力，这也是团队发布能力的最佳体现。

解决问题，关键就是要快。而要真正实现快，审批与处置过程一定是高度自动化的。

> 质量活动是有成本的，为了保证快速迭代发布，一定程度的问题发生并不是末日。

## Reference

- [DevOps实战笔记](https://time.geekbang.org/column/intro/235?code=GC0JpoFVv4WPkRF1zJR2ApOvhfke36rvSRJoaCEOd50%3D&utm_term=SPoster)