# 简单记录一些增强学习领域文章 <br>
## 连续空间相关的文章<br>
- Learning Continuous Control Policies by Stochastic Value Gradients (SVG) <br>

	> Nicolas Heess, DeepMind ,2015
  - 提出框架使用反向传播学习连续动作空间策略. 通过在 bellman 等式的确定性函数中增加噪声来增加策略随机性.
  - 本文提出的方法是 SVG, 通过 re-parameterization 把噪声引入到策略和 model 中.

* Asynchronous Methods for Deep Reinforcement Learning (A3C) <br>
	> Volodymyr Mnih.  2016. DeepMind
	* 异步梯度下降优化深度神经网络,提出了许多异步变体. 表现最好的变体是应用在 actor critic 上的并且超过 Atari 上的最新水平.使用多核 CPU 运行程序.
	* 解决 AC 算法不收敛问题.同时创建多个并行环境,多个 agent 隔离运行.主结构的参数更新受到副结构提交更新的不连续性干扰.更新相关度降低,收敛性提高.
	* DRL 基于 experience replay, 但他的缺点是:每次交互需要计算,需要离策略学习算法.本文使用多线程取代了 experience replay.
	* 本文提出的算法: asynchronous one-step Q-learning; Asynchronous advantage actor-critic;
	
* Deterministic Policy Gradient Algorithms (DPG)    <br>
	> 2014, David Silver ,DeepMind <br>
	
	* DDPG 算法在这个 DPG 基础上完成.
	* 本文证明了 policy Gradient.
	
* Continuous Control with Deep Reinforcement Learning (DDPG)  <br>
  > 2016年ICLR, 作者: Timothy P.Lillicrap   <br> 
  
  * DDPG 算法从这里提出. AC 算法加 DQN 算法. 是 AC 的升级版. 

* Continuous Deep Q-Learning with Model-based Acceleration (NAF)<br>
	> 2016年, 作者: Shixiang Gu   <br>
	
    * 高维RL 基于 model-free 会增加采样的复杂程度,这篇文章主要降低连续空间采样复杂度.提出 NAF 可以使用 Qlearning 处理连续任务.使用 model-based 加速; model-based: 使用监督学习并且在 model 下优化出的策略.
	* 本文三个贡献: Qlearning 在连续空间的使用; learned model; 加速 model free 连续学习.
	* NAF: 不需要像 DDPG 那样训练两个网络,只需要训练一个;提出算法名字:continuous Q learning with NAF.
	* 从文章实验来看, NAF 的更稳定,并且 reward 高,与 DDPG 相比.
	* 为什么这个 NAF 的 Qlearning 可以在连续空间运用? ❓ 怎么选择动作的? 选择动作的网络如何更新? 和 DQN 的更新方式有区别么?

## Advantage相关文章
* Dueling Network Architectures for Deep Reinforcement Learning  (Dueling) <br>
	> 2016, Ziyu Wang, DeepMind <br>
	
	* 对于 model free RL 提出了一个新的神经网络: 一个为状态价值函数,一个为运动利益方程.在价值与利益两方面去耦合.
	* 这个 Dueling network 是一个 Q 网络有两个输出流而不是一个.分别估计 state value function(V<sup>π</sup>) 和 advantage function(A<sup>π</sup>)
	* 实验证明这种结构可以更快的找到正确动作. 我们发现当可用动作越高, 学习难度就越大, 不过 Dueling DQN 还是会比 Natural DQN 学习得更快. 收敛效果更好.
	* 因为 Dueling 网络输出是 Q 函数,所以可以使用很多已经存在的算法训练,如 DDQN,SARSA.此外,也可以利用很多存在的提升方法,包括:better replay memories, better exploration policies, intrinsic motivation 等等.

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
