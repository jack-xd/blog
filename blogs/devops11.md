# 【学习笔记】分支策略让研发高效协作 | 落地篇07

> 如果说多人软件协作项目中有一个灵魂的话，我认为，这个灵魂就是分支策略。
>
> 可以说，**分支策略就是软件协作模式和发布模式的风向标**。选择一种符合 DevOps 开发模式的分支策略，对于 DevOps 的实践落地也会大有帮助

7、8年前，谈分支策略应该是一个较为领先的话题，今天来看就有点“老生常谈”的感觉了。

有需要了解的同学，建议看 W3Cschool 的介绍，感觉说的足够全面了。

专栏中，作者提到的另外一个点，是 Facebook 团队领先实践，“主干开发，主干发布”。

> 为了保证主干分支的质量，自动化验收手段是必不可少的，因此，每一次代码提交都会触发完整的编译构建、单元测试、代码扫描、自动化测试等过程。在代码合入主干后，会进行按需发布，先是发布到内部环境，也就是只有 Facebook 的员工才能看到这个版本，如果发现问题就立刻修复，如果没有问题，再进一步开放发布给 2% 的线上生产用户，同时自动化检测线上的反馈数据。直到确认一切正常，才会对所有用户开放。
>
> 最后，通过分支策略和发布策略的整合，注入自动化质量验收和线上数据反馈能力，最终将发布频率从固定的每天 2 次，提升到每天多次，甚至实现了按需发布的模式。

故事来自于 Facebook 工程团队在 2017 年发布的一篇文章 “Rapid release at massive scale“，高山仰止。

## 思考题

以一个典型的移动应用项目来说，涉及多个代码仓库，IOS端、Android端、前端、后端 等等，一个需求，往往依赖于跨小组的配合实施。

在这种背景下，有效的开发管理与分支策略就凸显其研发协作的重要性了。目前想法是这样来做，

- 需求分析，起点是接收需求，终点是形成开发任务（以需求编号为索引，进行拆分，可能涉及多个代码工程）
- 研发协同，每个代码工程，同一个需求指定专人跟进，固定前后端对接人
- 产品进行端到端的用户验证
- 利用特性分支，当需求通过验证后，同步回主干；再按照版本点进行发布。

对比 Facebook 工程团队的实践，差距还是很大。英文好的同学可以看看。

> By applying traditional continuous delivery techniques to our mobile stack, we’ve gone from four-week releases to two-week releases to one-week releases. 
>
> Today we use the same kind of branch/cherry-pick model on mobile that we previously used on web. Although we push to production only once a week, it’s still important to test the code early in real-world settings so that engineers can get quick feedback. We make mobile release candidates available every day for canary users, including 1 million or so [Android beta testers](https://play.google.com/apps/testing/com.facebook.katana).

## Reference

- [DevOps实战笔记](https://time.geekbang.org/column/intro/235?code=GC0JpoFVv4WPkRF1zJR2ApOvhfke36rvSRJoaCEOd50%3D&utm_term=SPoster)