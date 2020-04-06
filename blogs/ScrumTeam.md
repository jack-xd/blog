# 他山之石：身边的SCRUM团队

> 他们说，SCRUM是聚焦一件事，交付可使用的软件。

UNC 是一家软件服务公司，从天眼查上看，人员规模小于50人，是一个不折不扣的小微企业。参与我司相关开发工作的团队有10人，其中PO和内部SM各1人，测试3人，主力开发5人。

工作关系，自19年上半年，兄弟与UNC团队成员有较多的接触，虽未进行详细统计，但是明显感受到了两点：

1. 团队5个主程都有相当不错的开发能力；
2. 整个团队的软件交付能力比其它软件服务公司要高。

下文是对PO访谈后兄弟的思考，姑且称为**兄弟五力之SCRUM团队怎么来**。

> 你可能会想到行业分析中的波特五力，不同于波特提出的五种”恶势力“，**兄弟五力是五股团队的支撑力量**

## 老板之力

敏捷转型得到了UNC公司老板的大力支持。

实际上，这个开发团队是在2015年拉起来的，在团队成立之初，公司老板花了几十w聘请外部敏捷教练，对团队进行敏捷导入。

## 稳定之力

在这个小团队中，除了近年新招聘的测试人员外，PO/内部SM/主力开发都是当年参加敏捷导入的团队班底。

受人数限制，应该说这个小小的样本并不能推导出明确的结论，可是在软件行业人才流动较高的大背景下，团队人员架构稳定运行至今亦属难能可贵。

## 信任之力

之前与团队成员有多次交流，兄弟觉得UNC团队之间建立了足够的信任，是一种**”基于弱点的信任“**，或者说团队成员彼此都是**”可以交付后背的兄弟“**。

举个例子。

F哥，团队后端扛把子，有一次聊到

> 我原来也写前端，可是出来的代码被大家各种吐槽，一气之下干脆不写了，专心搞后端。

成员之间相互敞开心扉，承认自己的缺点和弱项，互相之间无惧“调戏”，建立起相互信任的基础。

## 习惯之力

团队采用Scrum作为敏捷实践框架，目前一般以两周作为一个 sprint 周期。

sprint 周期开始前，PO与SM梳理周期内的待办事项，即 sprint backlog，规划周期内需要完成的内容。其后，团队召开规划会，即 sprint planning meeting，确定 sprint 目标，对产品 backlog中的用户故事进行分解与估算，拆分为具体的开发功能点，开发领取任务。

每日站会中，团队目前可以严格控制在15分钟，成员明白到站会是为了促进信息内部共享，加深彼此信任，而不是为了进行深入问题讨论。

## 工具之力

软件开发实践中，采用的工具往往可以从侧面反映出团队的开发水平。

> 画外音，使用普通文本编辑开发出OS内核的大神不在讨论范围内

UNC 团队目前熟练使用 git/git flow/sourcetree 等进行版本控制与协同开发，通用性软件资产沉淀到 Maven 私库进行复用，应用架构方面，具备前后端分离、微服务架构开发能力，采用 Dubbo 作为 rpc 框架，对常见中间件例如 zookeeper/kafka/fastDFS/nginx/mysql 等均可熟练使用。目前开始了应用容器化、云原生架构等尝试。