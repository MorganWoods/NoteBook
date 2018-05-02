# RL的环境与平台

[TOC]

## Gym

* 使用环境

  ```shell
  import gym
  env = gym.make('CartPole-v0')
  env.reset()
  for i_episode in range(20):
      observation = env.reset()
      for t in range(100):
          env.render() #显示模拟界面
          print(observation)
          action = env.action_space.sample()
          observation, reward, done, info = env.step(action)
          if done:
              print("Episode finished after {} timesteps".format(t+1))
              break
  ```

* 环境汇总

  > https://gym.openai.com/envs/#classic_control      This is the birds-eye view 

  ​

* 常用函数介绍

  ```shell
  step()# 返回四个值,是 observation,reward,done,info; 其中 info 是调试用的,不能参考这个值来学习.
  reset()# 返回初始的 observation.

  '''显示动作空间维数和观测空间维数'''
  print(env.action_space)   # 对于 cartpole 的空间
  #> Discrete(2)
  print(env.observation_space) 
  #> Box(4,)

  '''有效的观测是4个数的数组,可以查看 box 的边界'''
  print(env.observation_space.high)
  #> array([ 2.4       ,         inf,  0.20943951,         inf])
  print(env.observation_space.low)
  #> array([-2.4       ,        -inf, -0.20943951,        -inf])
  ```

  ​