# 【学习笔记】内建质量 | 落地篇10

> 不应该将质量依赖于检验工作，因为检验工作既昂贵，又不可靠。最重要的是，检验工作并不直接提升产品质量，只是为了证明质量有缺陷。
>
> -- 《质量管理 14 条原则》

在 Devops解决什么问题 中，作者提到了敏捷模式中，**开发和测试团队抱团取暖**。

对内建质量的理解，可以从“抱团取暖”出发：

- 抱团：**开发和测试团队是平等的**，不是一个运动员一个裁判员的关系；
- 取暖：认可了第一点，那么对于这个广泛意义上的团队来说，团队所做的一切不是为了验证产品存在问题，而是为了确保产品没有问题。

作者提出，内建质量有两个核心原则，

1. 问题发现得越早，修复成本就越低；
2. 质量是每个人的责任。

进一步地，作者分析内建质量建设的思路、步骤、常见问题与方法。

## 实施思路

关键词：在软件交付的各个环节中注入质量控制的能力。

- 需求环节，可以定义清晰的需求准入规则；
- 开发阶段，坚持代码评审和持续集成；
- 测试阶段，合理采用各类测试手段；
- 部署和发布阶段，技术监控、业务监控、危险操作扫描等。

## 实施步骤

主要针对开发+测试论述，因为研发是软件产品质量的源头

1. **选择适合的检查类型**：按照软件产品的领域以及阶段，选择投入产出比相对比较高的检查类型。例如客户端业务，考虑引入 Infer 扫描，编码风格等优先级可以往后放；
2. **定义指标并达成一致**：指标可以结合静态指标与动态增量指标（取得一致就是艺术范畴了，无法说）；
3. **建立自动化执行和检查能力**：快速反馈，使得软件开发就像打游戏一样，通关给奖励，失败gg重来。
4. **定义问题处理方式**：做好持续投入，优化第3步能力；

## 常见问题与建议

参考作者提供的表格。

> 在公司中，无论是建立质量门禁的规则，还是开发一套平台系统，其实都不是最困难的事情.
>
> 难的是，在实际过程中，有多少正常流程走了特殊审批？有多少发布是走的紧急通道？又有多少人会说开启了质量门禁，就会阻碍业务交付？
>
> 说到底，还是要问问自己，你愿意付出多少代价，来践行自己的理念和原则。

## Reference

- [DevOps实战笔记](https://time.geekbang.org/column/intro/235?code=GC0JpoFVv4WPkRF1zJR2ApOvhfke36rvSRJoaCEOd50%3D&utm_term=SPoster)