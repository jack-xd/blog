# 【学习笔记】持续交付平台十大必备特征（上） | 平台篇03

> 持续交付对企业的 DevOps 落地起到了举足轻重的作用，流水线是持续交付中最核心的实践，也是持续交付实践最直接的体现。

作者结合自身在企业内部建设落地流水线平台的经验，以及业界各家公司的平台设计理念，总结了**现代流水线设计的十大特性**，计划通过两篇专栏讲述。



## 特性一：打造平台而非能力中心

关键动作：将持续交付流水线平台和垂直业务平台分开，并定义彼此的边界。

所谓的垂直业务平台，就是指单一专业领域的能力平台，比如自动化测试平台、代码质量平台、运维发布平台等等，这些也是软件交付团队日常打交道最频繁的平台。

流水线平台只专注于流程编排、过程可视化，并提供底层可复用的基础能力。比如，像是运行资源池、用户权限管控、任务编排调度流程等等。

## 特性二：可编排和可视化

所谓的流程可编排能力，就是指用户可以自行定义软件交付过程的每一个步骤，以及各个步骤之间的先后执行顺序。

流程可编排，需要平台前端提供一个可视化的界面，来方便用户定义流水线过程。典型的方式就是，将流水线过程定义为几个阶段，每个阶段按顺序执行。在每个阶段，可以按需添加步骤，这些步骤可以并行执行，也可以串行执行。

## 特性三：流水线即代码

借助版本控制系统的强大功能，流水线代码和业务代码一样纳入版本控制系统，可以简单追溯每次流水线的变更记录。

## 特性四：流水线实例化

首先，流水线需要支持参数化执行。

其次，流水线的每一次执行，都可以理解为是一个实例化的过程。

最后，流水线需要支持并发执行能力。

## 特性五：有限支持原则

流水线的设计目标，应该是满足大多数、常见场景下的快速使用，并提供一定程度的定制化可扩展能力，而不是满足所有需求。

流水线设计要提供有限的可能性，而非穷举所有变量因素。

孙子兵法，虚实原则，yyds！

## Reference

- [DevOps实战笔记](https://time.geekbang.org/column/intro/235?code=GC0JpoFVv4WPkRF1zJR2ApOvhfke36rvSRJoaCEOd50%3D&utm_term=SPoster)