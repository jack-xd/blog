# 【学习笔记】探索试验中的混沌工程 | 落地篇14

> 混沌工程采用了一种全新的思路，在系统中主动注入混沌进行实验，以此来发现潜在的真实世界的问题

阅前提醒，本篇作者介绍了一个应对复杂分布式系统可用性挑战的新学科——混沌工程。

所以，本篇内容讨论的混沌工程，适用面其实不广，大多数系统，都还没有达到“复杂分布式系统”的标准。

那么怎样才算达到标准？作者在文中放了一张Netflix 公司在 2014 年公开的微服务调用关系图，我觉得简单判断的方法，就是看公司里面有没有人说他能够说清楚所有的系统调用关系，如果有，那还不算复杂。

通篇看完，联想到的是一句话“**用复杂性对抗复杂性**”。

> 我们正在进入一个知识经济的时代，整个系统，正在变得极其复杂。
>
> 能处理这种级别的复杂性的，唯有同等级别的复杂性。

这句话来自于罗辑思维，《创造性的工作怎么激励》，通过分析梅奥诊所的例子，来讨论“怎么样大量的知识工作者在一起工作，还能提高效率”这个问题。

摘录几段有启发的话。

> 我们凭常识就知道，这种盐多了就加糖、糖多了就加盐，面干了就加水、面稀了就加面的方法搞出来的制度，肯定不是越来越有效，而是越来漏洞越大。
>
> 如果要确立一个激励的维度，本质上就是在让一个复杂的事，坍缩成了一个简单的事。激励制度是有了，但是这个事本身就必败无疑。

扯回来，看看神马是混沌工程。

作者谈了混沌工程的五大原则，及对应的实践。

## 建立稳定状态的假设

关于系统的稳定状态，就是说，**有哪些指标可以证明当前系统是正常的、健康的**。

实践，定义一组系统指标，并围绕它们建立一整套完善的数据采集、监控、预警机制。参考指标如下图。

## 真实世界的事件

个人理解，作者在这段说的，是混沌工程的理论基础。我们认为

1. 我们无法模拟所有的异常事情
2. 即便是特别不起眼的事件，都会带来严重的后果
3. 真实世界的问题，只有在生产环境中才会出现

## 在生产中实验

存在明显风险的一点，要求实验范围可控，并且具备随时停止实验的能力。

如果系统没有为弹性模式做好准备，那么就不要开启生产实验。

实践，随机选择部分业务模块，并圈定部分实验节点，然后开启常态化压测（注意这个压测是没有通知对应系统进行针对性准备的）-- 往往在没有准备的时候才能发现真实问题。

## 持续的自动化实验

自动化是所有重复性活动的最佳解决方案。

实践，相关的工具，例如阿里的 ChaosBlade ，开源的 Resilience4j 和 Hystrix 等。

## 最小的影响范围

混沌工程实践的原则就是不要干扰真实用户的使用。

实践，有点类似于上一篇说的部署一个灰度实验环境，或者暗部署的方式。

> 如果现有的服务连基本的可恢复性这个条件都不具备的话，那么混沌实验是没有意义的。

## Reference

- [DevOps实战笔记](https://time.geekbang.org/column/intro/235?code=GC0JpoFVv4WPkRF1zJR2ApOvhfke36rvSRJoaCEOd50%3D&utm_term=SPoster)