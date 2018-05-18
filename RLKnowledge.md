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

## 常用公式汇总

> Todo: 完成论文后汇总一下公式到此处

discounted return :   ${ R }_{ t }=\sum _{ k=0 }^{ \infty  }{ { \gamma  }^{ k }{ r }_{ t+k } } $ 

state-value function:   ${ V }^{ \pi  }(s)=\mathbb{ E }[R|s,\pi ]$  

state-action-value  :   ${ Q }^{ \pi  }(s,a)=\mathbb{ E }[R|s,a,\pi ]$    

​		其动态编程的计算式 :  ${Q}^{\pi}(s,a)=\mathbb{E}_{{s}^{\prime}}[r+\gamma\mathbb{E}_{{a}^{\prime}\sim{\pi}({s}^{\prime})}[{Q}^{\ast}({s}^{\prime},{a}^{\prime})]|s,a,\pi]$    

Advantage function:  ${ A }^{ \pi  }(s,a)={ Q }^{ \pi  }(s,a)-{ V }^{ \pi  }(s)$     

## 期刊与会议总结

人工智能：IJCAI, AAAI; （期刊AI）

机器学习顶级会议: NIPS,ICML (前俩最牛的), UAI,AISTATS; IJCAI (International Joint Conference on Artificial Intelligence)和 AAAI (American Association for Artificial Intelligence)轮流开.

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



