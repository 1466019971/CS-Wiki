# 💫 策略梯度 Policy Gradient

---

> 💡 **Policy Gradient** 属于 Value-Free、Policy-Based

对比起以值为基础的方法, Policy Gradients 根据概率直接输出动作的最大好处就是, **它能在一个连续区间内挑选动作**, 而 Value-Based 的比如 Q-learning 无法很好的处理连续动作

## 1. Policy Gradient 核心思想

如图所示, 观测的信息通过神经网络分析, 选出了左边的行为, 我们直接进行反向传递, 使之下次被选的可能性增加, 但是奖惩信息却告诉我们, 这次的行为是不好的, 那我们的动作可能性增加的幅度 随之被减低. 这样就能**靠奖励来左右我们的神经网络反向传递**. 

![](https://gitee.com/veal98/images/raw/master/img/20201102094845.png)

假如这次的观测信息让神经网络选择了右边的行为, 右边的行为随之想要进行反向传递, 使右边的行为下次被多选一点, 这时, 奖惩信息也来了, 告诉我们这是好行为, 那我们就在这次反向传递的时候加大力度, 让它下次被多选的幅度更猛烈。这就是 Policy Gradients 的核心思想.

Policy gradient 同样也要接受环境信息 (observation), **不同的是他要输出不是 action 的 value, 而是具体的那一个 action**, 这样 policy gradient 就跳过了 value 这个阶段

也就是说 Policy Gradient 网络的输入也是状态(State)，输出是每个动作的概率，例如 `[0.7, 0.3]` ，这意味着有70% 的几率会选择动作 0，30% 的几率选择动作 1

## 2. Policy Gradient 整体算法

我们介绍的 policy gradient 的基础算法是一种基于 **整条回合数据** 的更新, 也叫 **REINFORCE** 方法. 这种方法是 policy gradient 的最基本方法

θ 就是我们需要不断更新的神经网络参数

![](https://gitee.com/veal98/images/raw/master/img/20201102095848.png)

> 💡 $\pi$ 表示 Policy，$\pi(s,a)$ 表示在状态 s 下选择动作 a 的概率 
>
> **`Policy` 输出某个状态下所有可能动作的执行概率，它其实是一个函数，把输入的状态变成行为**。假设你是用 deep learning 的技术来做 reinforcement learning 的话，**`policy` 就是一个神经网络**，神经网络里面有一堆参数， <u>我们用 θ 来代表 π 的参数</u>：
>
> <img src="https://gitee.com/veal98/images/raw/master/img/20201026173154.png" style="zoom:40%;" />

<img src="https://gitee.com/veal98/images/raw/master/img/20201102095924.png" style="zoom:67%;" /> 表示在 状态 `s` 对所选动作 `a` 的吃惊度, 如果 $\pi(s,a)$ 概率越小, 反向的 $log\pi(s,a)$ 反而越大. 如果在 $\pi(s,a)$ 很小的情况下, 拿到了一个大的 `R`, 也就是 大的 `V`, 那 $log\pi(s,a)V$ 就更大, 表示更吃惊

👍 **通俗来说，我选了一个不常选的动作（概率小）, 却发现原来它能得到了一个好的 reward, 那我就得对这次的参数进行一个大幅修改. 这就是吃惊度的物理意义**

## 3. 代码实现

> ✅ TODO

## 📚 References

- [Bilibili - 李宏毅《深度强化学习》](https://www.bilibili.com/video/BV1MW411w79n)
- [Github - LeeDeepRL - Notes](https://datawhalechina.github.io/leedeeprl-notes/)
- [CSDN - 李宏毅深度强化学习笔记 - jessie](https://blog.csdn.net/cindy_1102/article/details/87904928)
- [强化学习纲要](https://github.com/zhoubolei/introRL)