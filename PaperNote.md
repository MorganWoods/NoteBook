# Reinforcement Learning领域文章相关笔记 
[TOC]

## 综述类

* Deep Reinforcement Learning: An Overview

  > Yuxi Li, 2017

  * 以排山蹈海的方式全面地介绍了 DRL.

  

## Continuous control 领域

* Actor critic 算法记录

  * 策略函数作为 actor 选择动作;价值函数作为 critic 对策略函数进行评估;根据 critic 的输出更新价值网络和策略网络.

* Asynchronous Methods for Deep Reinforcement Learning  (A3C) 

  > Volodymyr Mnih. DeepMind. 2016. 
  * 异步梯度下降优化深度神经网络,提出了许多异步变体. 表现最好的变体是应用在 actor critic 上的并且超过 Atari 上的最新水平.使用多核 CPU 运行程序.
    解决 AC 算法不收敛问题.同时创建多个并行环境,多个 agent 隔离运行.主结构的参数更新受到副结构提交更新的不连续性干扰.更新相关度降低,收敛性提高.
  * DRL 基于 experience replay, 但他的缺点是:每次交互需要计算,需要离策略学习算法.本文使用__多线程取代了 experience replay.__
    本文提出的算法: asynchronous one-step Q-learning; Asynchronous advantage actor-critic;

* Benchmarking Deep Reinforcement Learning for Continuous Control  

  > Yan Duan, OpenAI . 2016

  - 一份 Benchmark. 文中列举的算法有: Reinforce;__TNPG__;RWR;REPS;__TRPO__;CEM;CMA-ES; __DDPG__
  - 其中, TRPO 与 TNPG 效果优秀. 本文介绍了参数的选取与微调.
  - 对 DDPG 的评价: 某些任务收敛快,由于样本的高效率.但是不稳定.并且训练过程中 policy 表现降级.对 reward 的范围较敏感,本文实验把 reward 设置为0.1,似乎提高了稳定性.
  - TNPG 和 TRPO: 此二者表现尤其突出,证明了限制 policy 分布的改变可以提高学习的稳定性.
  - 文末补充材料中有实验细节,可以作为参考.

* Combining Deep Q-Learning and Advantage Actor-Critic for Continuous Control (A2S)

  > Rae C.Jeong, Waterloo,2018
  >
  >  源码 https://github.com/raejeong/RaeboSchool

  * 本文代码与 DDPG 的唯一区别是在选择最优动作方面: DDPG 是 PG 网络( actor)直接选择动作并执行, DQN 网络(critic)进行价值评估; 此文是根据 policy 网络分布选择几个候选动作,再用 DQN 网络价值评估,存储价值最高动作. 并执行.(把确定性多做策略改为不确定性动作策略)
  * 实验效果优于 A2C

* Combining Policy Gradient And Q-Learning  (PGQL)

  > Brendan O'Donoghue,ICLR,2017

  * 与 DDPG 齐名的 PGQL; 结合 PG 与离策略 Q-Learning,
  * Q 更新方程做了改变.

* Continuous Control with Deep Reinforcement Learning (DDPG)  
  > 2016年ICLR, 作者: Timothy P.Lillicrap   

  * DDPG 算法从这里提出. AC 算法加 DQN 算法. 是 AC 的升级版. 

* Continuous Deep Q-Learning with Model-based Acceleration (NAF)       
  > 2016年, Cambridge, 作者: Shixiang Gu  

    * 高维RL 基于 model-free 会增加采样的复杂程度,这篇文章主要降低连续空间采样复杂度.提出 NAF 可以使用 Qlearning 处理连续任务.使用 model-based 加速; model-based: 使用监督学习并且在 model 下优化出的策略.
  * 本文三个贡献: Qlearning 在连续空间的使用; learned model; 加速 model free 连续学习.
  * NAF: 不需要像 DDPG 那样训练两个网络,只需要训练一个;提出算法名字:continuous Q learning with NAF.
  * 从文章实验来看, NAF 的更稳定,并且 reward 高,与 DDPG 相比.
  * 为什么这个 NAF 的 Qlearning 可以在连续空间运用? ❓ 怎么选择动作的? 选择动作的网络如何更新? 和 DQN 的更新方式有区别么?

- Deterministic Policy Gradient Algorithms (DPG)    

  > 2014, David Silver ,DeepMind 

  - DDPG 算法在这个 DPG 基础上完成.
  - 本文证明了 policy Gradient: 策略梯度,其想法是沿着使目标函数(累积奖赏$$ J(π_θ)$$函数)变大的方向调整策略的参数.

- Equivalence Between Policy Gradients and Soft Q-Learning 

- High-Dimensional Continuous Control Using Generalized Advantage Estimation (GAE)

  > John Schulman, ICLR, 2016

  * Policy Gradient 方法对于 RL的两个挑战:需要大量的样本数据;尽管输入数据不稳定,但是也很难得到稳定的和持续的提高. 解决前者使用 value function 减少方差; 解决后者使用 __trust region optimization__.

  * 使用二足四足机器人做实验, model free 的.

  * 本文贡献: 提出 GAE 来纠正和提高 PG 的 variance reduction 的有效性;提出对于 Value function 使用 TRO 方法,健壮有效来训练神经网络;结合上二者,获得了在连续控制任务中有效的策略.

  * 一个可能的未来工作是如何自适应或自动调节估计参数 $\gamma, \lambda.$

  * > 摘自 [天津包子馅](https://zhuanlan.zhihu.com/p/29486661) : 基线函数的引用可以减小 PG 的方差. A( 优势函数)是动作值函数相对于值函数的优势, 若动作值函数比值函数大,那么又是函数为正,反之亦反; 对于 PG,优势函数为正时，其幅值为正，则参数沿着使得该轨迹概率增大的方向更新；优势函数为负时，策略梯度的幅值为负，则参数沿着使得该轨迹减小的方向更新。因此，采用优势函数时，算法的收敛速度更快。
    >
    > 然而，根据优势函数定义 ![A^{\pi}\left(s_t,a_t\right)=Q\left(s_t,a_t\right)-V\left(s_t\right)](https://www.zhihu.com/equation?tex=A%5E%7B%5Cpi%7D%5Cleft%28s_t%2Ca_t%5Cright%29%3DQ%5Cleft%28s_t%2Ca_t%5Cright%29-V%5Cleft%28s_t%5Cright%29) ，优势函数中的值函数常常利用逼近算法近似计算，因此往往会引入偏差。
    >
    > 优势函数的一步估计可写为：
    >
    > 从优势函数的一步估计中我们看到， ![V\left(s_t\right)](https://www.zhihu.com/equation?tex=V%5Cleft%28s_t%5Cright%29) 和 ![V\left(s_{t+1}\right)](https://www.zhihu.com/equation?tex=V%5Cleft%28s_%7Bt%2B1%7D%5Cright%29) 的真实值都是未知的，而是用到了估计值，因此优势函数存在偏差。
    >
    > GAE的方法是改进对优势函数的估计，将偏差控制到一定的范围内。其方法是对优势函数进行多步估计，并将这些多步估计利用衰减因子进行组合
    >
    > Shulman 提出广义优势函数估计 ![GAE\left(\gamma ,\lambda\right)](https://www.zhihu.com/equation?tex=GAE%5Cleft%28%5Cgamma+%2C%5Clambda%5Cright%29) ，利用指数加权平均从1步到无穷步的优势函数估计
    >
    > 该方法很好的评价了偏差和方差. 利用代替AC方法中的Critic会产生更好的效果? ? ?

- Learning Continuous Control Policies by Stochastic Value Gradients  (SVG) 

  > Nicolas Heess, DeepMind ,2015

  - 提出框架使用反向传播学习连续动作空间策略. 通过在 bellman 等式的确定性函数中增加噪声来增加策略随机性.
  - 本文提出的方法是 SVG, 通过 re-parameterization 把噪声引入到策略和 model 中.

- Policy Gradient Methods for Reinforcement Learning with Function Approximation (PG)

  > Richard S.Sutton, 1999

  - 证明了 PG 可以收敛到全局最优点. 优化函数是 RL 必要的环节, 但是标准的方法优化价值函数和决定策略从理论上难以证明.这篇文章中我们探索了一个可供替代的方法,策略可以明确地用他自己的函数近似者表明, 独立于价值函数,并且根据关于策略参数的梯度期望来更新.我们主要的结果表明梯度可以写成适应于近似动作值和利益方程的形式.使用这个结果,我们首次证明使用任意的微分近似方程的策略迭代可以收敛到全局最优策略.

- Q-prop: Sample-Efficent Policy Gradient With An Off-Policy Critic (Q-Prop)

  > Shixiang Gu, Cambridge, ICLR, 2017

  * 在面向现实实验中, model free DRL 会面对一个高采样复杂度. Batch PG 方法可以稳定学习,但是 cost 高方差,需要大量的 batches; TD 方法如 AC 和 QL, 采样多但是有偏差. 这篇文章提出方法: __结合 PG 的稳定性与 off policy RL 的效率__.提出了 Q prop 方法,他既有采样效率也有稳定性. 降低梯度估计的方差并且不引入偏置.
  * 核心想法: 使用 critic 的 first-order Taylor expansion (一阶泰勒展开) 作为控制变量.解析梯度项评价过程,它既可以被看做使用off-policy的评价过程来减小策略梯度方法带来的方差，又被看作使用on-policy蒙特卡洛方法来修正评价梯度方法带来的偏差。
  * PG 除了高方差,另一问题在于他需要 on-policy 样本,这使得他对样本敏感. Q prop 用来估计 PG 的. 
  * 通过使用确定性有偏估计作为控制变量的独特形式对于 MC PG 估计器,我们可以有效地使用两种形式的梯度信息来建造一个新估计器在实践中提高样本效率通过包含 off policy 采样同时保留 on policy MC PG 的稳定性.

- Trust Region Policy Optimization (TRPO)

  > John Schulman, University of  California, 2015

  ![imag](https://pic3.zhimg.com/80/v2-e519a12e0617dd0eb66de29db96af429_hd.jpg)

  * 在策略梯度方法中还有很多有意思的课题，比如相容函数法，自然梯度法等等。但Shulman在博士论文中已证明，这些方法其实都是TRPO弱化的特例，说这些是再次强调TRPO的强大之处。策略梯度算法的硬伤就在更新步长 $\alpha$，当步长不合适时，更新的参数所对应的策略是一个更不好的策略，当利用这个更不好的策略进行采样学习时，再次更新的参数会更差，因此很容易导致越学越差，最后崩溃。所以，合适的步长对于强化学习非常关键。所谓合适的步长是指当策略更新后，回报函数的值不能更差。如何选择这个步长？或者说，如何找到新的策略使得新的回报函数的值单调增，或单调不减。这是TRPO要解决的问题。

    ![优势函数示意图](https://pic2.zhimg.com/80/v2-05a037b139af7efc98e97e7b13bb7882_hd.jpg)

    值函数 ![V(s)](https://www.zhihu.com/equation?tex=V%28s%29) 可以理解为在该状态下所有可能动作所对应的动作值函数乘以采取该动作的概率的和。更通俗的讲，值函数 ![V(s)](https://www.zhihu.com/equation?tex=V%28s%29) 是该状态下所有动作值函数关于动作概率的平均值。而动作值函数 ![Q(s,a)](https://www.zhihu.com/equation?tex=Q%28s%2Ca%29) 是单个动作所对应的值函数，$Q-V$能评价当前动作值函数相对于平均值的大小。所以，这里的优势指的是动作值函数相比于当前状态的值函数的优势。如果优势函数大于零，则说明该动作比平均动作好，如果优势函数小于零，则说明当前动作还不如平均动作好。

    ​

  * 优化控制策略的方法,可以保证单调递增.对有优化大量非线性策略很有效(如神经网络).不需要大量调试超参数.

  * 许多策略优化算法分类为三个:policy iteration; policy gradient;derivative-free optimization 如 cross entropy 方法(CEM) 和 covariance matrix adaptation(CMA), 它把 cost 视为黑盒; 对于连续控制,如 CMA 的方法很成功; 本文,第一次提出最小化一个固定的替代 loss 函数保证策略提高通过 non-trivial step size, 还描述了两种变体,1 ,single-path 方法,这种可以应用于 model-free 环境, 2 , vine 方法(滕树),需要系统在特定的状态保存,仅仅在仿真时候适用.

  * MDP$(\mathcal{S} ,\mathcal{A} ,P,c,{\rho}_{0},\gamma)$, 其中,$c$是 cost function, ${\rho}_{0}$是初始状态${s}_{0}$的分布,$\pi$是随机策略,${\eta}_{\pi}$是__期望衰减 cost__. 然后是 Q,V,A, 与其他的不同,这里都是用 cost 代替了前人的 reward. $\tilde{\pi}$是另一个策略关注 $\pi$的Advantage; 提出$\rho_{\pi}(s)$是非正规化的衰减 visitation 频率:$\rho_{\pi}(s)=(P(s_{0}=s)+\gamma P(s_{1}=s)+\gamma^{2} P(s_{2}=s)+...)  $.

  * TRPO 的后身是 PPO, 分布式是 DPPO.

- Reinforcement Learning with Deep Energy-Based Policies (soft Q learning)

  > Tuomas Haarnoja, 2017

  * ​

- Soft-Robust Actor-Critic Policy-Gradient (SR-AC)

  > Esther Derman, Technion Israel institute, Google deepmind, 2018

  * MDPs 有些不确定性, 有个 Robust MDPs 解决这个问题. 但是它带来了过分谨慎的结果 ;  本文集中学习一个 soft robust policy 通过吸收 soft robustness 和 online ac 算法  ;  本文的贡献: 1, 一个 soft-robust 衍生的 目标函数 为了 PG. 2. SRAC 算法使用随机优化来学习 . 3. 收敛证明. 4. 实验,展示了其效率.
  * PG 方法一般的目标函数时最大化平均 reward function.
  * soft-robust 目标函数…

## Advantage相关文章
* 对于解耦 Q 成为 A 和 V 的来源基础记录:

  * 把 Q 拆成 A 和 V 最早是baird, leemon, Advantage updating,1993 ,从 NAF文章摘出.

* Dueling Network Architectures for Deep Reinforcement Learning  (Dueling) 

  > 2016, Ziyu Wang, DeepMind <br>

  * 对于 model free RL 提出了一个新的神经网络: 一个为状态价值函数,一个为运动利益方程.在价值与利益两方面去耦合.
  * 这个 Dueling network 是一个 Q 网络有两个输出流而不是一个.分别估计 state value function(${V}_{\pi}$) 和 advantage function(${A}_{\pi}$)
  * 实验证明这种结构可以更快的找到正确动作. 我们发现当可用动作越高, 学习难度就越大, 不过 Dueling DQN 还是会比 Natural DQN 学习得更快. 收敛效果更好.
  * 因为 Dueling 网络输出是 Q 函数,所以可以使用很多已经存在的算法训练,如 DDQN,SARSA.此外,也可以利用很多存在的提升方法,包括:better replay memories, better exploration policies, intrinsic motivation 等等.

* Continuous Deep Q learning with model-based Acceleration (NAF)

  > 2016, Shixiang Gu
  >
  > 参考此文:   https://blog.csdn.net/u013236946/article/details/73243310

  *  提出算法降低 model free 采样复杂度, NAF - normalized Advantage functions; 和 iLQG;   model based 算法可以提高效率,但是限制策略只能是一个学到的模型;  本 NAF 算法避免了 actor 网络或 policy 函数,是一个简化的算法, 简化优化目标从而提高采样效率.

  * $Q(x,u|θ^{Q})=V(x|θ^{V})+A(x,u|θ^{A})$ ,  A 值表示動作 u 在狀態 x 下的優勢. 算法的目標是使策略網絡輸出的動作 u 對應的 Q 值最大. 本文的方法是讓 A 恒≤ 0 ,則 Q 恒≤ V , 在某一狀態下最優的動作的優勢函數為0. 所以最優的動作的值函數 是 Q = V.

  * $A(x,u|θ^{A})=−\cfrac{1}{2}(u−μ(x|θ^{μ}))^{T}P(x|θ^{P})(u−μ(x|θ^{μ}))$ , P是一个关于状态的正定矩阵，因为正定矩阵可以进行楚列斯基（Cholesky）分解，即 $P(x|θ^{P})=L(x|θ^{P})L(x|θ^{P})^{T}$ ,其中,L(x|θP)是对角线都是正数的下三角矩阵，且是唯一的。最终算法的Loss Function为 

    $L(θ^{Q})=E[(TargetQ−Q(x_{t},u_{t}|θ^{Q}))^{2}]$

    $TargetQ=r_{t}+γV′(x_{t+1}|θ^{Q′})$

    $Q(x_{t},u_{t}|θ^{Q})=V(x_{t}|θ^{V})+A(x_{t},v_{t}|θ^{A}) $

    使用DQN的训练方式训练。

    ![这里写图片描述](https://img-blog.csdn.net/20170614200213254?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdTAxMzIzNjk0Ng==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

## Value based method

* Parameter Space Noise for Exploration

  > Matthias Plappert, Open AI, 2018

  - DRL generally inject noise exploration in the action space. 一种可替代的方法是直接向参数中加入噪声.这样可以使得探索更加一致性并且得到丰富的表现集合.  他验证了这种方法结合传统的 RL 无论在策略离策略 DQN,DDPG,TRPO 离散或连续动作空间都表现很好.

* Universal Value Function Approximators (UVFA)

  > Tom Schaul, David Silver, Google DeepMind, 2015

  * 引入一个 universal value function approximator$V(s,g;\theta)$, 不仅概括了状态 s 还有 goals g, 建立了一个有效的监督学习技术, 通过因式分解已观测的 values 为不同的向量为 state 和 goal. 然后学习 mapping 从 s 到 g 对这些分解的嵌入的向量. 最终结果 UVFA 可以成功generalise(概括,推广,普及)之前没见过的 goals.
  * 看不懂了,

* Value Iteration Networks (VIN)

  > Aviv Tamar, UC Berkeley, NIPS 最佳论文 ,2016
  >
  > https://github.com/avivt/VIN
  > https://github.com/TheAbhiKumar/tensorflow-value-iteration-networks

  - 把一个规划程序嵌入到神经网络结构中提高泛化能力.

  - 将奖励函数和转移函数参数化能求导,在策略求解中引入 __attention__ 机制

    


## Navigation 相关的论文

* A Deep-Network Solution Towards Model-less Obstacle Avoidance

  * 这俩人专门研究 DRL机器人避障的.挺专业的

* Building Generalizable Agents with a Realistic and Rich 3D Environment

  > Yi Wu , UC Berkeley , yuxin wu, Facebook AI, ICLR , 2018

  - 建立了一个 House3D 的东西, 基于 SUNCG 数据库. 用于室内导航的. 大量采集的图像形成各 library

* Control of Memory, Active perception, and Action in Minecraft

  * 利用外部记忆结构(类似 NTM,DNC,MemNN)通过将记忆存入外部记忆结构,提高 Agnet 的迁移能力,导航能力泛化到没见过的场景. 作者是密歇根大学博士生,

* Deep Reinforcement Learning in a 3-D Blockworld Environment

  * 使用CNNs 与 DQN 网络来提取图像深度信息. 使用Minecraft 环境, 开源的. 视觉输入,估计距离.

* Learning Sample-Efficient Target Reaching for Mobile Robots 

  > Arbaaz Khan , 2018

  * 机器人寻找目标导航. 雷达扫描距离; 可以参考本文写作,很好.
  * 使用 gym-gazebo 仿真环境测试.并且进行了实物测试.

* LEARNING TO NAVIGATE IN COMPLEX ENVIRONMENTS

  * 类似微软屏幕保护的迷宫环境. 此文追求累积奖励最大化与辅助任务 loss 降低,达到提高数据效率和训练效果的目标.此文顺便做了 slam 的工作. agent 需要有长短的记忆来存储环境中的动态因素. 本文目标是找到东西,辅助任务是对输入的图像给出深度信息有利于路径规划,另一个是知道 slam 的 loop closure, 就是知道这个地方我曾经来过;
    文中模型: A3C, LSTM , stacked LSTM. NavA3C; 本文中的环境是开源的.

* Towards cognitive exploration through deep Reinforcement learning

  >Lei Tai , Ming Liu , 2016

  * 使用图像输入的深度信息探测距离,避障功能.使用了卷积神经网络.并且在生活中做了实验. 可以参考一下. 从图像信息中提取深度信息.




## Reward 上做的文章

* Deep Successor Reinforcement Learning

  > Tejas D.Kulkarni, Harvard, NIPS 2016
  >
  > 参考此文总结: http://swarma.blog.caixin.com/archives/164137

  * 《Curiosity-driven Exploration by Self-supervised Prediction》 by UCB. ICML 2017. 
    《Learning to Act by Predicting the Future》 by IntelLab. ICLR 2017 (oral).
    《Deep Successor Reinforcement Learning》 by MIT & Harvard. NIPS 2016 workshop.
    这三篇都是解决 reward 稀疏的问题, 先收藏保留. 有的思想是奖励分成过程奖励与结果奖励.
  * 本文用SR 方法求解 RL. 思路是将 value function 拆成两部分,一个是通过预测任务学习型到的表达,另一个是表达紧密相关激励函数
    reward shaping 对 RL 训练的好处,稳定性提高,收敛加快.



## 其他笔记

http://www.voidcn.com/article/p-rlbfnjbt-gc.html    这个网页列出增强学习文章与分类列表,很有参考价值,分类详细.

	改进目标Q值计算：Deep Reinforcement Learning with Double Q-learning
	改进随机采样：Prioritized Experience Replay
	改进网络结构，评估单独动作价值：Dueling Network Architectures for Deep Reinforcement Learning ( 本文为ICML最佳论文之一）
	改进探索状态空间方式：（1）Deep Exploration via Bootstrapped DQN （2）Incentivizing Exploration In Reinforcement Learning With Deep Predictive Models
	改变网络结构，增加RNN：Deep Recurrent Q-Learning for Partially Observable MDPs（非DeepMind出品，效果很一般，谈不上改进，本文也不考虑讲解）
	实现DQN训练的迁移学习：（1）Policy Distillation （2） Actor-Mimic: Deep Multitask and Transfer Reinforcement Learning
	解决高难度游戏Montezuma‘s Revenge：Unifying Count-Based Exploration and Intrinsic Motivation
	加快DQN训练速度：Asynchronous Methods for Deep Reinforcement Learning （这篇文章还引出了可以替代DQN的A3C算法，效果4倍Nature DQN）
	改变DQN使之能够应用在连续控制上面：Continuous Deep Q-Learning with Model-based Acceleration

