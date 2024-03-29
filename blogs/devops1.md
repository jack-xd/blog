# 【学习笔记】DevOps解决什么问题 | 基础篇01

> 基础篇共分4篇，介绍 DevOps 的定义、价值、实施与衡量，建立对 DevOps 的体系认知

基础篇的第一篇，回答了两个问题：

1. DevOps 的定义是什么？答：没有统一的官方的定义，每个人都能从自己的立场来为 DevOps 做贡献。
2. DevOps 解决什么问题？答：软件工程领域的协作与组织问题，打破开发、测试、运维乃至产品、安全的效率竖井，使得价值快速交付，组织持续改进成为可能。

有点抽象，想象一个具体的场景，我们到医院体检，常常能够碰到一位进行体检顺序安排的医生，”B超的人比较多，现在可以先去拍胸片“。这给了我们一个启发，我们可以通过聚焦整体流动效率，使得价值能够更快交付。

回到软件工程，看看下面三个重要的发展阶段。

## 瀑布开发模式

> 在项目一开始就确定项目目标、范围以及实现方式。而这个时间点往往是我们对用户和市场环境信息了解最少的时候，这样做出来的决策往往带有很大的不确定性，很容易导致项目范围不断变更，计划不断延期，交付上线时间不断推后，最后的结果是，即便我们投入了大量资源，却难以达到预期的效果。
>

每次谈到软件工程，瀑布模式总是会被拿出来鞭打一顿。这次鞭打的角度，火力集中在开发、测试、运维各个部门中间的“墙”，如图。



## 敏捷开发模式

> 既然我们无法充分了解用户的真实需求是怎样的，那么不如将一个大的目标不断拆解，把它变成一个个可交付的小目标，然后通过不断迭代，以小步快跑的方式持续开发。
>
> **敏捷源于开发实践，敏捷的应用使得开发和测试团队抱团取暖。但是还有一群人在冷冰冰的看着他们，“现在没到发布窗口”。**

达成敏捷开发的其中一个标准，可以是这样的：质量内建于研发的环节中，而不是与开发独立的一个环节，能够保障功能交付的质量。

同时要注意，敏捷并不能直接提升团队的开发速度。但是持续的迭代与验证，能够节省不必要的浪费与返工，如图。

## DevOps模式

> DevOps 最开始想要打破的就是开发和运维之间的对立和隔阂。
>
> 开发团队的一个常见绩效指标是看开发完成了多少需求。运维团队的考核指标却是系统的稳定性、可用性和安全性。

这个故事的另外一个版本，可能是这样的，**运维团队是考核者，开发团队的考核指标是完成了多少需求，以及系统的稳定性、可用性和安全性**。

扎心。

处在软件交付中心的开发团队，始终处于一种“背锅”的状态。因此，每一次的上线发布都是一场战役，整个团队如临大敌，上线失败的焦虑始终如影随形。



## Reference

- [DevOps实战笔记](https://time.geekbang.org/column/intro/235?code=GC0JpoFVv4WPkRF1zJR2ApOvhfke36rvSRJoaCEOd50%3D&utm_term=SPoster)