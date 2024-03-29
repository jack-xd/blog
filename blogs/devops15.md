# 【学习笔记】小心技术债务滚雪球 | 落地篇11

> 技术债务，是指团队在开发过程中，为了实现短期目标选择了一种权宜之计，而非更好的解决方案，所要付出的代价。
>
> 这个代价就是团队后续维护这套代码的额外工作成本，并且**只要是债务就会有利息，债务偿还得越晚，代价也就越高**。

作者指出，带来技术债务的原因有很多，除了压力之下的快速开发之外，还包括不明真相的临时解决方案、新员工技术水平不足，和历史债务累积下来的无奈之举等。总之，代码维护的时间越长，引入的技术债务就会越多，从而使团队背上沉重的负担。

## 技术债务的类型

借用“Sonar Code Quality Testing Essentials”一书中的代码“七宗罪”，也就是复杂性、重复代码、代码规范、注释有效性、测试覆盖度、潜在缺陷和系统架构七种典型问题。

## 带来的问题

技术债务的积累就像真的债务一样，属于“**出来混，迟早要还**”的那种。

只不过是谁来还的问题而已。

- 额外的研发成本：完成一个需求需要更长的时间；
- 不稳定的产品质量：没有人知道上线会不会出严重问题；
- 难以维护的产品：代码质量陷入一种不断变坏的向下螺旋，越来越难以维护，问题越积累越多

## 如何量化

目前业界比较常用的开源软件，就是 **SonarQube**。

通过将技术债务可视化，团队会对代码质量有更直观的认识。

> 技术债务比例 = 修复已有技术债务的时间 / 完全重写全部代码的时间

在极端情况下，一份代码的技术债务修复时长甚至比完全推倒重写还要长，这就说明代码已经到了无法维护的境地。

## 解决方法与原则

作者提到了4个步骤以及4条原则。

- 步骤：共识、可见、止损、改善
- 原则：让技术债务呈良性下降趋势；优先解决高频修改的问题；在新项目中启动试点；技术债务无法被消灭，也不要等到太晚

跟着作者学习专栏到现在，大约到了1/3了，整体的感觉是原则看着都能懂，要能做到，真的需要天时地利人和。

- 天时：组织战略
- 地利：机构定位
- 人和：团队凝聚力，领导有魄力

后续再细说。

> 一个人出门时衣着得体，但是家里却乱成一团，找点东西总是要花很长时间。
>
> 小心啦，别让技术债务滚雪球。

## Reference

- [DevOps实战笔记](https://time.geekbang.org/column/intro/235?code=GC0JpoFVv4WPkRF1zJR2ApOvhfke36rvSRJoaCEOd50%3D&utm_term=SPoster)