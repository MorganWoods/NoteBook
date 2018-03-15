# 简单记录一些增强学习领域文章 <br>
## 连续空间相关的文章<br>
* Continuous Control with Deep Reinforcement Learning   <br>
  > 2016年ICLR, 作者: Timothy P.Lillicrap   <br>
  
    * DDPG 算法从这里提出. AC 算法加 DQN 算法. 是 AC 的升级版. 

* Continuous Deep Q-Learning with Model-based Acceleration  <br>
  > 2016年, 作者: Shixiang Gu   <br>
  
    * 高维RL 基于 model-free 会增加采样的复杂程度,这篇文章主要降低连续空间采样复杂度.提出 NAF 可以使用 Qlearning 处理连续任务.使用 model-based 加速; model-based: 使用监督学习并且在 model 下优化出的策略.
	* 本文三个贡献: Qlearning 在连续空间的使用; learned model; 加速 model free 连续学习.
	* NAF: 不需要像 DDPG 那样训练两个网络,只需要训练一个;提出算法名字:continuous Q learning with NAF.
	* 从文章实验来看, NAF 的更稳定,并且 reward 高,与 DDPG 相比.
	* 为什么这个 NAF 的 Qlearning 可以在连续空间运用?
	[![NAF](http://coach.nervanasys.com/algorithms/design_imgs/naf.png "NAF")](http://coach.nervanasys.com/algorithms/design_imgs/naf.png "NAF")
