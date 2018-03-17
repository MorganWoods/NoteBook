# 简单记录一些增强学习领域文章 <br>
## 连续空间相关的文章<br>
* Deterministic Policy Gradient Algorithms (DPG)  <br>  
  	> 2014, David Silver ,DeepMind
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
	* 为什么这个 NAF 的 Qlearning 可以在连续空间运用?

## Advantage相关文章
* Dueling Network Architectures for Deep Reinforcement Learning  (Dueling) <br>
  	> 2016, Ziyu Wang, DeepMind

	* 对于 model free RL 提出了一个新的神经网络: 一个为状态价值函数,一个为运动利益方程.在价值与利益两方面去耦合.
	* 这个 Dueling network 是一个 Q 网络有两个输出流而不是一个.分别估计 state value function(V<sup>π</sup>) 和 advantage function(A<sup>π</sup>)
	* 实验证明这种结构可以更快的找到正确动作. 我们发现当可用动作越高, 学习难度就越大, 不过 Dueling DQN 还是会比 Natural DQN 学习得更快. 收敛效果更好.
	* 因为 Dueling 网络输出是 Q 函数,所以可以使用很多已经存在的算法训练,如 DDQN,SARSA.此外,也可以利用很多存在的提升方法,包括:better replay memories, better exploration policies, intrinsic motivation 等等.
