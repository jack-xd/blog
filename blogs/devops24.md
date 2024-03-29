# 【学习笔记】持续交付平台十大必备特征（下） | 平台篇04

> 持续交付对企业的 DevOps 落地起到了举足轻重的作用，流水线是持续交付中最核心的实践，也是持续交付实践最直接的体现。

作者结合自身在企业内部建设落地流水线平台的经验，以及业界各家公司的平台设计理念，总结了**现代流水线设计的十大特性**，计划通过两篇专栏讲述。



## 特性六：流程可控

流水线可以为了满足不同阶段的业务目标而存在，并且每条流水线上实现的功能都不相同。

1. 多条流水线。比如开发阶段流水线、集成阶段流水线，以及部署阶段流水线等，一起覆盖了整个软件交付流程。
2. 支持多种触发方式，比如定时触发、手动触发、事件触发等。
3. 流水线需要支持人工审批。

特别地，事件触发是实现持续集成的一个非常重要的能力。以Gitlab为例，需要在代码仓库中添加 Webhook。

## 特性七：动静分离配置化

解决啥问题？**在不改变代码的情况下，实现原子的动态化配置**。

动静分离是一种配置化的实现方式。这就是指，将需要频繁调整或者用户自定义的内容，保存在一个静态的配置文件中。然后，系统加载时通过读取接口获取配置数据，并动态生成用户可见的交互界面。

无论在原子结构设计，还是前后端交互等领域，定义一个通用的数据结构是设计标准化的系统的最佳实践。

这个特性没看懂，需要补充流水线开发相关知识。

## 特性八：快速接入

借助版本控制系统的强大功能，流水线代码和业务代码一样纳入版本控制系统，可以简单追溯每次流水线的变更记录。

流水线的很多能力都不是自己提供的，而是来源于垂直业务平台。那么，在建设流水线平台的时候，能否快速地实现外部平台能力的接入，就成了一个必须要解决的问题。

能力来源于垂直业务平台，要求快速接入外部平台能力。

定义一套标准的接入方式。以接口调用类型为例，接入平台需要提供一个任务调用接口、一个状态查询接口以及一个结果上报接口。

按照作者经验，快的标准是在几天内完成一个平台的接入。

## 特性九：内建质量门禁

通过在持续交付流水线的各个阶段注入质量检查能力，可以让内建质量真正落地。

在流水线平台上，要完成质量规则制定、门禁数据收集和检查，以及门禁结果报告的完整闭环。

## 特性十：数据聚合采集

原则就是满足用户对最基本的结果数据的查看需求。

实话说，这后五个特征，需要结合实际的流水线平台研发经验。兄弟目前尚无法深入理解。

## Reference

- [DevOps实战笔记](https://time.geekbang.org/column/intro/235?code=GC0JpoFVv4WPkRF1zJR2ApOvhfke36rvSRJoaCEOd50%3D&utm_term=SPoster)