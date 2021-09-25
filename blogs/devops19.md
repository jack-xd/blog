# 【学习笔记】建立DevOps正向度量体系 | 落地篇15

> If you can’t measure it, you can’t manage it。
>
> -- 爱德华·戴明博士

落地实践篇来到尾声，还剩最后两讲，作者谈到的主题是两个，**度量**与**持续改进**。

学习到现在，度量与持续改进是专栏里面两个出现频率最靠前的词语。原则、目标等论述不再重复赘述，直接上干货。

## 哪些是重要指标

作者直接给了一套指标框架，分3个维度，共8个指标。

- **交付效率-需求前置时间**：从需求提出到完成整个研发交付过程，并最终上线发布的时间。这个时间是最能客观反映团队交付速度的指标。
- **交付效率-开发前置时间**：从需求进入排期、研发真正动工的时间点开始，一直到最终上线发布的时长。它体现的是研发团队的交付能力。
- **交付能力-发布频率**：单位时间内的系统发布次数。原则上发布频率越高，代表交付能力越强。
- **交付能力-发布前置时间**：指研发提交一行代码到最终上线发布的时间，是团队持续交付工程能力的最直观的考察指标。
- **交付能力-交付吞吐量**：单位时间内交付的需求点数。体现出标准需求颗粒度下的团队交付能力。
- **交付质量-线上缺陷密度**：单位时间内需求缺陷比例。缺陷越多，说明需求交付质量越差。
- **交付质量-线上缺陷分布**：所有缺陷中的严重致命等级缺陷所占的比例。这个比例的数值越高，说明缺陷等级越严重。
- **交付质量-故障修复时长**：从有效缺陷提出到修复完成并上线发布的时间。这个指标考察了故障定位和修复的时间，同时考察了发布前置时间。

粗看这3个维度，交付效率与交付能力两个维度的边界有点模糊，个人觉得何以合并起来，总共是两个维度，**快不快**与**好不好**。

快不快分两类指标：

1. 要等待的时间：xx前置时间，等待的时间追求尽量短；
2. 输出量：单位时间内的xx次数，越多越快能力越好。

好不好直接对应交付质量。

## 开启度量工作

1. 细化指标：关键是大家要认。



1. 收集数据：形成习惯。
2. 数据可视化：大家都能看到。

> 度量只是一种手段，而非目的。归根结底，度量的真正目的还是团队效率的提升和业务的成功。只有通过度量激起团队自发的改进意愿，提升团队改进的创造性和积极性，才是所谓的“正向度量”。

## Reference

- [DevOps实战笔记](https://time.geekbang.org/column/intro/235?code=GC0JpoFVv4WPkRF1zJR2ApOvhfke36rvSRJoaCEOd50%3D&utm_term=SPoster)