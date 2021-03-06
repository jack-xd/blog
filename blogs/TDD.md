# 又在写bug？Bug free！老子用了TDD

>当我们从无到有地写下一行行代码时，中间的任意一个时刻，程序都是运行不起来的，至少是达不到设计效果的，从另一个角度看，完全等效于一堆bug。

## 结缘TDD

新年伊始，我司研发体系大哥发了个广告：

>敏捷开发实战营，名额有限，参加从速。你将获得
>
>1. 应用到工作的测试驱动开发方法
>2. 精准框定需求，实践重构
>3. 编写失败的测试，驱动产品代码
>4. 识别“坏”代码味道

**开发**、**实战**，看着和以往的培训都不太一样，兄弟想着“加个技能点傍身”，赶紧报了名。

### 实战营Day1

到点，群里发链接，直播上课。敢情和B站差不多啊？不急，且听听再说。

老师上来就放了地图炮：

> 客气点讲，我们行业里 80% 的人写代码都不合格；不是针对在座的谁，你有相当大的概率，也是个“不太合格”的程序员；

接下来，老师抛出一个问题，

>**怎么叫合格的程序员？**程序员真正的日常工作，**是把大块需求拆解成小块任务，再把小块的任务实现成代码。**这两件事做得又好又快，就是程序员的基本功。

最后，”今天是第一次跟大家视频上课，也是最后一次，祝练有所成！下课。“

 ### 实战营DayN

正如老师 Day1 说的，后续再没有直播讲课了，取而代之的，是每日任务+编程练习+打卡考核+提交作业。

实战营有严格的纪律，未按时完成任务，第 1 次提醒，第 2 次踢出群。（课程刚过半，群内人数从最初的 201 人下降到 100 人）

兄弟入了坑，只能努力跟上进度。回顾21天的实战营，收获了下面几个技能点：

- **TDD 的基本节奏**
  - 没有失败的测试就不能写代码。
  - 只允许写刚好让测试通过的代码。
  - 红-绿-红-绿，小步快跑式迭代，直至完成功能。
- **用测试用例描述沟通开发需求**
  - 客户到底要的是什么，以什么优先级要？
  - 动手开发前，首先弄清需求的范围和优先级，并用测试的形式记录下来。
- **从机器的角度来思考问题**
  - 程序员的工作，是要告诉机器，如何正确的做事情。
  - 机器的思考是线性的，输入->处理->输出。（江湖人称冯.诺伊曼体系）
  - 锻炼将大问题分解为几个子问题，再通过输入/输出关联起子问题的能力。
- **欲善其事，先利其器**
  - 开发的工作离不开一个趁手的 IDE。
  - 测试一下自己的熟悉度？全键盘，采用 TDD 方法实现FizzBuzz，掐表，10 分钟内完成。
- **重构**
  - 开发中随时进行，目标：新需求/变更需求到来时，依然容易实现
  - 识别代码中的“坏味道”，按照既有套路进行重构

## TDD拯救DM

### 那个下午

隔壁团队最近出了版本问题，有一定影响，生产安全又又又被老板关注了。

照例，层层召开安全生产专项会议。老板在台上语重心长，兄弟在台下，一边听着，一边想着手上管的一堆系统：

- 系统A，服务互联网客户，前后端分离+微服务，分成了12个应用，平均每个月投产2次；
- 系统B，硬件管理，放着各路厂家的异构后台；
- 系统C，新上的大数据平台；
- 系统D，系统E，系统F。。。

不想不知道，一想吓一跳，怎么接了这么多系统啊？？！！

"安全第一要务，各自排查问题根源，深刻反省！"老板的话掷地有声，兄弟头上已经微微冒汗了。

![时间不多了](https://mmbiz.qpic.cn/mmbiz_jpg/0DaCuZzGibSSVIVtJI2lAad4COJLfglGGS8ChoGpxAQkBUrkvuaYUupRm7vJfoJ67sMZibBDGHXYt3HmHib5f5BlA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

### 开发经理的烦恼

**情景一**

系统经理：“生产告警，怎么回事啊？？”

开发经理：“马上看”

开发经理：“没有业务影响” （内心os：别建单别建单）

**情景二**

业务经理：“需求开发太慢了，等系统上线了，市场机会早就错过了”

开发经理：“增加人手，加快推进。”（内心os：甲方爸爸，需求上周才到的啊～）

**情景三**

骨干小王：“世界这么大，我想去看看”

开发经理：“这两年多亏有你，交接一下，祝前程似锦”（内心os：又走一个骨干，人员什么时候能稳定点）

![都是泪](https://mmbiz.qpic.cn/mmbiz_jpg/0DaCuZzGibSSVIVtJI2lAad4COJLfglGG1SIviaYB8kMooOia9CSCL5icIOXpOOTIteEiaPdQW4GUR0pOuBJdRIzCKQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

### 再次思考TDD

设想一下，当我们从无到有地写下一行行代码时，中间的任意一个时刻，程序都是运行不起来的，至少是达不到设计效果的，从另一个角度看，完全等效于一堆bug。

你可能会说，只是功能还没实现，并没有 bug 。

事实上，从用户的角度看，缺失某个功能和包含一个有故障的功能，程序都是无用的。

TDD，全称Test Driven Developmeng，测试驱动开发。测试是用来**驱动**开发的，测试就是一个模拟的客户。

- 测试不通过，ok，至少我们明确知道客户期待有什么功能；
- 测试跑过了，bravo，对模拟客户来说，这就是一个 bug free program！

### TDD能救我吗

> There's no siver bullet!

**要不要用TDD呢？**

兄弟认为，工具从来只是手段，不是目的。正如上文描述，开发团队面临很多挑战，产保安全，需求快上线，输出要稳定；引入 TDD，就有可能成为团队其中一个挑战。

究竟要不要用？兄弟想可以用民主的方法：团队表决，少数服从多数。

简单来说，工作不是我们的目的，如果大部分团队成员觉得，TDD能够让自己早点下班，深夜不用爬起来处理告警，生活更加幸福，咱们就用。

**决定要干，怎么引入TDD呢？**

兄弟实践中，欢迎各位多联系多交流。