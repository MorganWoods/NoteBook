# Reinforcement Learning知识点笔记 
[TOC]

## 文章收集笔记
	改进目标Q值计算：Deep Reinforcement Learning with Double Q-learning
	改进随机采样：Prioritized Experience Replay
	改进网络结构，评估单独动作价值：Dueling Network Architectures for Deep Reinforcement Learning ( 本文为ICML最佳论文之一）
	改进探索状态空间方式：（1）Deep Exploration via Bootstrapped DQN （2）Incentivizing Exploration In Reinforcement Learning With Deep Predictive Models
	改变网络结构，增加RNN：Deep Recurrent Q-Learning for Partially Observable MDPs（非DeepMind出品，效果很一般，谈不上改进，本文也不考虑讲解）
	实现DQN训练的迁移学习：（1）Policy Distillation （2） Actor-Mimic: Deep Multitask and Transfer Reinforcement Learning
	解决高难度游戏Montezuma‘s Revenge：Unifying Count-Based Exploration and Intrinsic Motivation
	加快DQN训练速度：Asynchronous Methods for Deep Reinforcement Learning （这篇文章还引出了可以替代DQN的A3C算法，效果4倍Nature DQN）
	改变DQN使之能够应用在连续控制上面：Continuous Deep Q-Learning with Model-based Acceleration

## 增强学习笔记

* Actor-Critc 网络

  这是 on policy 的. 运行流程: A 根据 state 选出一个 action :arrow_right: C 根据 state 和 action 对 A 的表现打分 :arrow_right: A根据 C 的打分,调整自己的策略(网络参数) :arrow_right: C 根据系统的 reward 和 C 的 target 调整自己打分策略(网络参数)
  一开始 A 与 C 都是随机的,但是由于 reward 的存在,二者策略越来越准; A 调整参数根据 C 的打分,迎合 C.

* Policy: maps state to action,optimization is to find an optimal mapping.

* episodic tasks - 情节性任务。指（强化学习的问题）会在有限步骤下结束。
  continuing tasks - 连续性任务。指（强化学习的问题）有无限步骤。
  episode - 情节。指从起始状态（或者当前状态）到结束的所有步骤。
  tabular method - 列表方法。指使用了数组或者表格存储每个状态（或者状态-行动）的信息（比如：其价值）。

  planning method - 计划性方法。需要一个模型，在模型里，可以获得状态价值。比如： 动态规划。
  learning method - 学习性方法。不需要模型，通过模拟（或者体验），来计算状态价值。比如：蒙特卡洛方法，时序差分方法。

  on-policy method - on-policy方法。评估的策略和优化的策略是同一个。
  off-policy method - off-policy方法。评估的策略和优化的策略不是同一个。意味着优化策略使用来自外部的样本数据。
  target policy - 目标策略。off-policy方法中需要优化的策略。
  behavior policy - 行为策略μ。off-policy方法中提供样本数据的策略。
  importance sampling - 行为策略μ的样本数据。
  importance sampling rate - 由于目标策略π和行为策略μ不同，导致样本数据在使用上的加权值。
  ordinary importance sampling - 无偏见的计算策略价值的方法。
  weighted importance sampling - 有偏见的计算策略价值的方法。
  MSE(mean square error) - 平均平方误差。
  MDP(markov decision process) - 马尔科夫决策过程

* ≐ - 定义上的等价关系。
  E[X] - X的期望值。
  Pr{X=x} - 变量X值为x的概率。
  v↦g - v渐近g。:ear:
  v≈g - v约等于g。
  R - 实数集合。
  Rn - n个元素的实数向量。
  maxa∈A F(a) - 在所有的行动中，求最大值F(a)。
  argmaxc F(c) - 求当F(c)为最大值时，参数c的值。

* unbiased estimate :无偏估计,用样本统计量来估计总体参数时的一种无偏推断.估计量的数学期望等于被估计参数的真实值,具有无偏性,是一种用于评价估计量优良性的准则.

## 增强算法的技术

experience repaly	soft target update	generalized Advantage estimate	NAF		Double Q learning		attention 机制	reward 方程参数化(可以考虑对 reward 下手)

## 一些网站收藏

* 使用 DDPG,keras 玩 TORCS 赛车游戏,有源码

  https://yanpanlau.github.io/2016/10/11/Torcs-Keras.html

* 两个检索论文与相对应的 code 的网页

  http://www.gitxiv.com

  https://paperswithcode.com

  

## 常用公式汇总

> Todo: 完成论文后汇总一下公式到此处

discounted return :   ${ R }_{ t }=\sum _{ k=0 }^{ \infty  }{ { \gamma  }^{ k }{ r }_{ t+k } } $ 

state-value function:   ${ V }^{ \pi  }(s)=\mathbb{ E }[R|s,\pi ]$  

state-action-value  :   ${ Q }^{ \pi  }(s,a)=\mathbb{ E }[R|s,a,\pi ]$    

​		其动态编程的计算式 :  ${Q}^{\pi}(s,a)=\mathbb{E}_{{s}^{\prime}}[r+\gamma\mathbb{E}_{{a}^{\prime}\sim{\pi}({s}^{\prime})}[{Q}^{\ast}({s}^{\prime},{a}^{\prime})]|s,a,\pi]$    

Advantage function:  ${ A }^{ \pi  }(s,a)={ Q }^{ \pi  }(s,a)-{ V }^{ \pi  }(s)$     

## 期刊与会议相关的总结

### 期刊

相关记录

OA 是开源的意思,供大家随意下载.

> 从 letpup 网页摘录下来的信息.  只记录和我水平与方向相关的 SCI 期刊

| 期刊名                                       | 影响因子 | 分区(大/小) | 印象 | 时间  |
| -------------------------------------------- | -------- | ----------- | ---- | ----- |
| Neurocomputing                               | 3.317    | 2/3         | ✅    | 6m    |
| Artificial Intelligence                      | 4.797    | 2/2         | ✅    | 9m    |
| Neural Networks                              | 5.287    | 2/2         |      | 12m   |
| Machine Learning                             | 1.848    | 3/3         |      | 6-12w |
| Autonomous Robots                            | 2.706    | 3/3         |      | 6-12w |
| Neural Computation                           | 1.938    | 3/3         | ✅    | 3m    |
| Knowledge based systems                      | 4.529    | 2/2         | ✅    | 3-6m  |
| ieee intelligent Systems                     | 2.374    | 2/2         |      |       |
| artificial intelligence review               | 2.627    | 3/3         |      | 5.3m  |
| ieee computational intelligence magazin      | 6.343    | 2/2         | 很难 | 10m   |
| international journal of neural systems      | 6.33     | 1/1         | 挺难 |       |
| journal of machine learning research         | 5        | 2/2         |      |       |
| international journal of intelligent systems | 2.9      | 3/3         |      |       |
|                                              |          |             |      |       |



__Neurocomputing__

文章类型:神经计算机理论,实践,应用;神经网络,学习系统,结构,方法,网络动态分析,学习理论,自组织,生物神经建模,人工智能,认知科学, fuzzy logic, 基因算法,信息理论,机器学习,神经生物学.模式识别.应用方面包括: 软件硬件的进步,软件环境仿真,数字模拟神经芯片.信号传输,语音识别,图像处理,机器视觉,控制,机器人学,优化,规划,金融预测.

__投稿知识__

corresponding author 通讯作者.

Highlights files 是主要成果和结论和亮点.方便快速了解内容.通常包裹3-5点,每一条字符不超过85,介绍文中最重要的东西.     where applicable : 在适用的情况下

graphical abstracts 是图文摘要.

competing interests statement: 利益冲突声明, 文章末尾有类似的句子需要说明一下和一些公司组织没有利益冲突

__本期刊的说明文件摘录__

do not just refer to 'the text'. Any subsection may be given a brief heading. Each heading should appear on its own separate line. 

Introduction : State the objectives of the work and provide an adequate background, avoiding a detailed literature survey or a summary of the results.





[期刊] ⬇️

PAMI

NEURAL COMPUTATION

ARTIFICIAL INTELLIGENCE

TKDE: IEEE TRANSACTIONS ON KNOWLEDGE AND DATA ENGINEERING

PR: PATTERN RECOGNITION

> 投稿经验记录
>
> https://blog.csdn.net/u013467442/article/details/46447349     这个链接很不错,可以反复多看一看.
>
> 摘要是引人入胜的"药引子",要留悬念;而结论是你论文得出的有证据的东西,要简单明了(很多人写了一大堆,把推测的结果都写上,这种论文质量很差); 另外,很多人认为数据越多, 发表的可能性越大,但经过读一些论文, 发现很多人的论文很烂, 感觉就是数据的简单堆积,所以,论文的重点应该在观点上,保证一篇论文一个新观点,已经足够了.
>
> 英语不好没关系，是人都知道我们英语没英国和美国人地道，但只要能表达清楚你要表达的意思就好了，而且等审稿人提出来时，一定要从头到尾改一遍，你会发现，这样多次发论文后，你的英语写作水平在一天天提高，拿两年前的论文过来，自己都感觉写得很烂
>
> 『注意』：论文的讨论部分很重要，不要说空话。平时做实验室就要留心，多想想出现的现象，问题应该怎么解释。
>
> 『注意』：不要乱写参考文献，只要引用的都要要注明，没有引用的不要往里面写。把有价值的东西做好“读书笔记”，节约写论文中编排参考文献的时间。 
>
> 『注意』：a 参考文献最好有1／3甚至1／2以上是近5年内的文献，这样的论文会让人感觉有水平些。b 其次，最好找一手的文献，不要那种二手的文献。
>
>  
>
> # 英文投稿的一点经验【转载】
>
>  
>
> 1. 首先一定要注意杂志的发表范围, 超出范围的千万别投,要不就是浪费时间;另外，每个杂志都有他们的具体格式要求，一定要按照他们的要求把论文写好，免得浪费时间，前些时候，我的一个同事向一个著名的英文杂志投稿，由于格式问题，人家过两个星期就退回来了，而且说了很多难听的话，说投稿前首先就应该看清楚他们的格式要求；
> 2. 论文写作一定要言简意赅,特别是摘要,引言和结论部分,特别是摘要和结论不能重复,发现有很多论文这两部分没有差别, 个人认为, 摘要是引人入胜的"药引子",要留悬念;而结论是你论文得出的有证据的东西,要简单明了(很多人写了一大堆,把推测的结果都写上,这种论文质量很差); 另外,很多人认为数据越多, 发表的可能性越大,但经过读一些论文, 发现很多人的论文很烂, 感觉就是数据的简单堆积,所以,论文的重点应该在观点上,保证一篇论文一个新观点,已经足够了. 
> 3. 投稿时,一定要找和你做研究内容相近领域的专家作评阅人,最好是国外的,不是说国内的不好,但就怕有人和你(或你老板)有过节,而且国内的很多所谓专家水平一般,且小心眼; 
> 4. cover letter要简单介绍你的工作的创新性,这样便于论文的快速发表, 当然也应该客气几句,让编辑感到心里舒服,主要是夸杂志好之类的话; 有人写coverletter，就是写上题目、然后说很荣幸投稿之类地话，也有人干脆把摘要全写上，这样个人认为不好，一定用两到三句话说明你论文“新”在哪，这个非常重要。
> 5. 前些时候看到论坛上很多人说不能写信催编辑,个人认为没关系,必要催信能够让人重视你的论文,一定要让人感到,你的论文在这发不了,好多地方在等着发呢(但很多牛杂志,可不吃这套哟，人家不缺稿，嘿嘿). 当然写信的时候要客气,说一些快速发表对于学术讨论和促进工作等方面的重要性之类的话; 
> 6. 能写英文,就不投中文稿, 特别是不投中文杂志英文版, 好不容易憋了篇英文,还投到低水平的杂志,很不甘心; 最重要的是国内杂志要钱，而国外很多不要。自从国内某杂志告诉我他们之所以收我很高的版面费是为了他们的生存时，我发誓包括以后我的学生就不再投中文杂志了（如果要投，对做材料的人，个人认为金属学报不错，目前收费低）；
> 7. 坚持就是胜利, 按照审稿人的建议好好改你的论文, 只要坚持投稿, 就一定能够被接收的, 如果论文被某杂志拒稿, 但不提倡降低杂志质量再投（应该根据审稿人意见修改后找合适的杂志）;有人认为低影响因子的杂志一定中的几率高, 我也这么认为,但一般低影响因子的杂志论文出稿比较慢!英语不好没关系，是人都知道我们英语没英国和美国人地道，但只要能表达清楚你要表达的意思就好了，而且等审稿人提出来时，一定要从头到尾改一遍，你会发现，这样多次发论文后，你的英语写作水平在一天天提高，拿两年前的论文过来，自己都感觉写得很烂。哈哈。（有好几次，一些审稿人总说我英语不好，这肯定是母语为英语的审稿人，但回信中，我只能说俺英语不好，地球人都知道，但个人认为英语在科技论文里主要是能让人懂我们的思想就够了，而且我也没有太多的钱去让某些改论文的公司帮我做这些事）。 
> 8.  再加两封催稿信!英语不好，但意思表达到了。 第一封,客气点! Dear Prof. Dr. Editor *** I submitted our latest work to your journal *** last November. I want to know the review process. If there are some reponses from the reviewers. Would you please tell me the results so that I can deal with it as early as possible? Please understand me that fast publication of our work is important for me. I appreciate your contribution to the publication of the high quality papers. Kind thanks to you for your care.  Best Regards Yours sincerely  
> 9. 第二封, 很不客气了,他们刚开始说他们的审稿周期很短,但近四个月了,也没消息,所以打算投别的地方.Dear Dr. Prof. ***  I am sorry to make you in trouble. It takes too long for reviewing my manuscript (***) which was submitted to Journal "***". Generally, only about two months are necessary for the reviewing process on my usual submissions to other Journals. Hence, I decide to withdraw this submission.  I am sorry to make this decision. Please understand my condition because the rapid publication of my work is important for me and our group.  I hope that I have chance to get a rapid publication in this Journal in future.  Thank you for your attention and kind help.  Best Regards Yours sincerelyfrom:http://chl033.woku.com/article/2721025.html1、
> 10. 对于我们工科的学生，要想写出论文来，必须有充足的数据及结论作为支撑，这里所说的数据不一定要很多，主要看你这些数据是否可以证明你论文中的结论。 
> 11. 2、在写论文时，不要把实验数据或图表往论文上面一放，只有描述而没有解释，这是编辑或审稿人最不想看到的文章，如果论文属于这一类，评论信中多半会说这样的论文为实验报告，其实编辑和审稿人他们有时也想知道你是如何做出来的，为什么，也在学习。
> 12.  3、在做实验前，就要考虑写论文了，不要等到作了很多试验，到头来全是：无用！那就惨了。我的经验就是，在试验前，你要考虑为什么要做这试验（实验背景及目的），怎么来做（实验步骤），根据自己的经验猜测可能会得到什么样的结果（结论），通过这样考虑之后，一篇论文的结构基本上出来了，就等着看结果到底如何了，如果和自己猜想的一样，自然可以写论文按照预先设好的步骤。一旦结果不一样，那就要恭喜你了，因为其中有很多东西需要你更深入的研究，可能还会有更大地创新内容。 
> 13. 4、对于写文章，文笔也相当重要，有很好的数据结论但是表达不清楚也不行，应为编辑和审稿人必须为他们的杂志前途着想，他们想让更多的人来读他们的杂志从而提高影响力，所以表达必须很清楚，能够让专业人士和相关学科的人都能够看明白你的论文意思。如果你的文笔不是很好，那就先看一看和你论文类似的文章，档次越高越好，看看别人如何表达的，相似的地方可以模仿。
> 14.  5、在论文经过自己几次修改后，放他一两天，再回过头来看看，如果自己觉得没有问题，那就给自己课题组有经验的老师或同学看看，看他们给你提出的意见（自己要判断是否可取了）。
> 15.  6、选择期刊很重要，要不然你投出去后，好消息的就几天退回，怀消息就是几个月退回说不符合杂志范围。选择期刊要根据自己论文的内容，是否和期刊的作者指南相符，此时你最好选者几个不同档次的期刊，从高到低排列，预备被退稿。选择好期刊后，严格按照期刊的投稿要求对论文进行排版，否则你的论文会被编辑退回（这样的论文不在少数），然后大胆地投出去，不管它中不中。
> 16.  7、等待，特别是第一篇，等待是一个难熬的日子，总是希望投稿后很快就能够收到消息，我曾经也经历过，这也是一个成长过程。
> 17.  8、收到消息有三种情况，一、接收，恭喜！二、拒绝，不要气馁，你可以认为编辑或审稿人不识货，当然要认真看拒绝信，看编辑或审稿人给你的评论，这就是你论文向能够发表前进了一步（一定要坚持，成为“拒无霸”就差不多了），修改后投向预先选好的档次低一点的杂志，命中率就提高了。三、修改后再看，这就是一种无定性条件，这种情况一定要认真对待，认真修改，有条件叫有经验的老师帮助。
> 18.  9、如果你的论文曾经被一个期刊发表过，接下来所作的工作继续投向这个期刊，命中率就大多了。 我写出来我的经验，仅供大家参考，结合自己的情况进行处理。













### 会议

18-19__会议__查询总结 (时间由近到远)     ✅标记是可以考虑的

考虑中的会议 AAAI,

人工智能：IJCAI, AAAI; （期刊AI）

机器学习顶级会议: NIPS,ICML (前俩最牛的), UAI,AISTATS; IJCAI (International Joint Conference on Artificial Intelligence)和 AAAI (American Association for Artificial Intelligence)轮流开.

> 可以参考的几个网站: CCF : 等级排名
>
> https://aideadlin.es/?sub=ML,CV,NLP,RO,SP,GR 截止日期排名

* AAAI 2019 , Jan27. 2019 , Hawaii , 美国人工智能年会 ✅
   Abstract Registration Due : Sep.1.2018
   	Submission Deadline: Sep 15 ,2018
   	Notification Due: Nov1,2018
   	Final Version Due : Nov14,2018

* ICLR 2019, Dec30,2019 , 21st  international conference on learning robots (19年的已经截止投稿了)

  ​	Submission Deadline: May31 ,2018 

* ICRA 2019, May20,2019, Robotics and Automation, at Canada.

  ​	30 April 2019 - Deadline for Advance Registration
  	28 February 2019 - Submission of Final Papers

* CVPR 2019, June15, at USA,

  ​	Deadline (I infer): Nov 1 ,2018

* ICML 2019, June 15, USA

    Deadline (infer) : Jan15, 2019

* IJCAI 2019, July15(infered), Macao,China, International joint conference on AI,

  ​	Deadline infered: Jan15,2019

* ACL 2019, July28, Association for computational Linguistics, Italy

  ​	Deadline infered: Feb 20, 2019

* IROS 2019, Nov3, Intelligent Robots and Systems. Macau,China

  ​	Deadline infered: April,1 ,2019

* NIPS 2019, Dec(infer) ,Neural Information Processing Systems,

  ​	Deadline infered : May31,2019

* Australasian AI 2018, Dec11, Austrialia (c➕)✅ 今年2018的来得及  考虑中....  周志华分类为三类会议

  ​	Deadline: July1,2018  

* ✅  ACCV 2018 还有17天截止 (c➕)

* 

* 几个截止日期远的,今年的

  icmla, ausdm, wi,icdm,kes

* 明年的可以考虑  AAMAS2019   ECAI2019









### 写作提纲

- 一篇__斯坦福__大学的写期刊文章各个章节内容的样板.

> https://cs.stanford.edu/people/widom/paper-writing.html

> **Paper Title**  ✅
>
> Titles can be long and descriptive:
>
> - *Linear-Time External Multipass Sorting with Approximation Guarantees*
>
> or short and sweet:
>
> - *Approximate External Sort*
>
> Here’s a middle-of-the-road length, plus a cute name that sticks in people’s minds:
>
> - Floosh: *A Linear-Time Algorithm for Approximate External Sort*
>
>  **The Abstract**  ✅
>
> State the problem, your approach and solution, and the main contributions of the paper. Include little if any background and motivation. Be factual but comprehensive. The material in the abstract should not be repeated later word for word in the paper.
> (**Exercise**: Write an abstract for the multiway sort example.)
>
> **The Introduction** ✅
>
> The Introduction is crucially important. By the time a referee has finished the Introduction, he’s probably made an initial decision about whether to accept or reject the paper — he’ll read the rest of the paper looking for evidence to support his decision. A casual reader will continue on if the Introduction captivated him, and will set the paper aside otherwise. Again, *the Introduction is crucially important*.
>
> Here is the Stanford InfoLab’s patented five-point structure for Introductions. Unless there’s a good argument against it, the Introduction should consist of five paragraphs answering the following five questions:
>
> 1. What is the problem?
> 2. Why is it interesting and important?
> 3. Why is it hard? (E.g., why do naive approaches fail?)
> 4. Why hasn’t it been solved before? (Or, what’s wrong with previous proposed solutions? How does mine differ?)
> 5. What are the key components of my approach and results? Also include any specific limitations.
>
> (**Exercise**: Answer these questions for the multiway sort example.)
>
> Then have a final paragraph or subsection: “Summary of Contributions”. It should list the major contributions in bullet form, mentioning in which sections they can be found. This material doubles as an outline of the rest of the paper, saving space and eliminating redundancy.
>
> (**Exercise**: Write the bullet list for the multiway sort example.)
>
> **Related Work** ✅ 我没写这部分
>
> The perennial(永恒的) question: Should related work be covered near the beginning of the paper or near the end?
>
> - **Beginning**, if it can be short yet detailed enough, or if it’s critical to take a strong defensive stance(立场) about previous work right away. In this case Related Work can be either a subsection at the end of the Introduction, or its own Section 2.
> - **End**, if it can be summarized quickly early on (in the Introduction or Preliminaries), or if sufficient comparisons require the technical content of the paper. In this case Related Work should appear just before the Conclusions, possibly in a more general section “Discussion and Related Work”.
>
> **The Body**  ✅ ...
>
> - **Guideline #1**: A clear new important technical contribution should have been articulated by the time the reader finishes page 3 (i.e., a quarter of the way through the paper).
> - **Guideline #2**: Every section of the paper should tell a story. (Don’t, however, fall into the common trap of telling the entire story of how you arrived at your results. Just tell the story of the results themselves.) The story should be linear, keeping the reader engaged at every step and looking forward to the next step. There should be no significant interruptions — those can go in the Appendix; see below.
>
> Aside from these guidelines, which apply to every paper, the structure of the body varies a lot depending on content. Important components are:
>
> - **Running Example**:When possible, use a running example throughout the paper. It can be introduced either as a subsection at the end of the Introduction, or its own Section 2 or 3 (depending on Related Work).
>
> - **Preliminaries**: This section, which follows the Introduction and possibly Related Work and/or Running Example, sets up notation and terminology that is not part of the technical contribution. One important function of this section is to delineate material that’s not original but is needed for the paper. Be concise — remember Guideline #1.
> - **Content**: The meat of the paper includes algorithms, system descriptions, new language constructs, analyses, etc. Whenever possible use a “top-down” description: readers should be able to see where the material is going, and they should be able to skip ahead and still get the idea.
>
> **Performance Experiments**
>
> We could have an entire treatise on this topic alone and I am surely not the expert. Here are some random thoughts:
>
> - Many conferences expect experiments.
> - It’s easy to do “hokey” or meaningless experiments, and many papers do.
> - It’s easy to craft experiments to show your work in its best light, and most papers do.
> - What should performance experiments measure? Possiblities:
> - Pure running time
> - Sensitivity to important parameters
> - Scalability in various aspects: data size, problem complexity, …
> - Others?
> - What should performance experiments show? Possibilities:
> - Absolute performance (i.e., it’s acceptable/usable)
> - Relative performance to naive approaches
> - Relative performance to previous approaches
> - Relative performance among different proposed approaches
> - Others?
>
> **The Conclusions**
>
> In general a short summarizing paragraph will do, and under no circumstances should the paragraph simply repeat material from the Abstract or Introduction. In some cases it’s possible to now make the original claims more concrete, e.g., by referring to quantitative performance results.
>
> **Future Work**
>
> This material is important — part of the value of a paper is showing how the work sets new research directions. I like bullet lists here. (Actually I like them in general.) A couple of things to keep in mind:
>
> - If you’re actively engaged in follow-up work, say so. E.g.: “We are currently extending the algorithm to… blah blah, and preliminary results are encouraging.” This statement serves to mark your territory.
> - Conversely, be aware that some researchers look to Future Work sections for research topics. My opinion is that there’s nothing wrong with that — consider it a compliment.
>
> **The Acknowledgements**
>
> Don’t forget them or you’ll have people with hurt feelings. Acknowledge anyone who contributed in any way: through discussions, feedback on drafts, implementation, etc. If in doubt about whether to include someone, include them.
>
> **Citations**
>
> Spend the effort to make all citations complete and consistent. Do not just copy random inconsistent BibTex (or other) entries from the web and call it a day. Check over your final bibliography carefully and make sure every entry looks right.
>
>  **Appendices**
>
> Appendices should contain detailed proofs and algorithms only. Appendices can be crucial for overlength papers, but are still useful otherwise. Think of appendices as random-access substantiation of underlying gory details. As a rule of thumb:
>
> - Appendices should not contain any material necessary for understanding the contributions of the paper.
> - Appendices should contain all material that most readers would not be interested in.
>
> **Grammar and Small-Scale Presentation Issues**
>
> In general everyone writing papers is strongly encouraged to read the short and very useful The Elements of Style by Strunk and White. Here’s a random list of pet peeves.
>
> - Just like a program, all “variables” (terminology and notation) in the paper should be defined before being used, and should be defined only once. (Exception: Sometimes after a long hiatus it’s useful to remind the reader of a definition.) Global definitions should be grouped into the Preliminaries section; other definitions should be given just before their first use.
> - Do not use “etc.” unless the remaining items are completely obvious.
>   Acceptable: *We shall number the phases 1, 3, 5, 7, etc.*
>   Unacceptable: *We measure performance factors such as volatility, scalability, etc.*
>
> (**Exercise**: The above rule is violated at least once in this document. Find the violations.)
>
> - Never say “for various reasons”. (Example: We decided not to consider the alternative, for various reasons.) Tell the reader the reasons!
> - Avoid nonreferential use of “this”, “that”, “these”, “it”, and so on (Ullman pet peeve). Requiring explicit identification of what “this” refers to enforces clarity of writing. Here is a typical example of nonreferential “this”: *Our experiments test several different environments and the algorithm does well in some but not all of them. This is important because …*
>
> (**Exercise**: The above rule is violated at least once in this document. Find the violations.)
>
> - Italics are for definitions or quotes, not for emphasis (Gries pet peeve). Your writing should be constructed such that context alone provides sufficient emphasis.
>
> (**Exercise**: The above rule is violated at least once in this document. Find the violations.)
>
> - People frequently use “which” versus “that” incorrectly. “That” is defining; “which” is nondefining. Examples of correct use:
> - *The algorithms that are easy to implement all run in linear time.*
>
> **Mechanics**
>
> - Always run a spelling checker on your final paper, no excuses.
> - For drafts and technical reports use 11 point font, generous spacing, 1″ margins, and single-column format. There’s no need to torture your casual readers with the tiny fonts and tight spacing used in conference proceedings these days.
> - In drafts and final camera-ready, fonts in figures should be approximately the same font size as used for the text in the body of the paper.
>   Tables, figures, graphs, and algorithms should always be placed on the top of a page or column, not in the body of the text unless it is very small and fits into the flow of the paper.
> - Every table, figure, graph, or algorithm should appear on the same page as its first reference, or on the following page (LaTex willing…).
> - Before final submission or publication of your paper, print it once and take a look — you might be quite surprised how different it looks on paper from how it looked on your screen (if you even bothered to look at it after you ran Latex the last time…).
>
> **Versions and Distribution**
>
> - Many papers have a submitted (and later published) conference version, along with a “full paper” technical report on the web. It’s important to manage versions carefully, both in content and proliferation. My recommendation is, whenever possible, for the full paper to consist of simply the conference version plus appendices. The full paper should be the only public one aside from conference proceedings, it should be coordinated with latest (final) conference version, and modifications to the full paper should always overwrite all publicly accessible previous versions of it.
> - I believe in putting papers on the web the minute they’re finished. They should be dated and can be referenced as technical reports — it’s not necessary to have an actual technical report number. Never, ever put up a paper with a conference copyright notice when it’s only been submitted, and never, ever reference a paper as “submitted to conference X.” You’re only asking for embarrassment when the paper is finally published in conference Y a year or two later.





