---
title: "The Evolution of Distributed Reinforcement Learning"
date: 2021-04-18
permalink: /posts/2021/04/the_evolution_of_distributed_reinforcement_learning/
tags:
  - multi-agent reinforcement learning
  - reinforcement learning
  - distributed machine learning
---
In 2015, DeepMind proposed their first distributed reinforcement learning algorithm architecture, known as Gorilla (General Reinforcement Learning Architecture). Before that, works on distributed deep learning focused on massively distributed architectures that can learn from more data in parallel and outperform training on a single machine. But all of them have focused on supervised and unsupervised learning, and there wasn’t a distributed architecture or algorithm for (deep) reinforcement learning. This chapter will give a glance at the evolution of distributed reinforcement learning, covering algorithms and frameworks.

## Gorilla Deep Q-learning Network

As we know, reinforcement learning requires a lot of data to do policy learning, larger than any general supervised learning task. To meet this requirement, DeepMind proposed the first work, deploy DQN on a distributed architecture. GDQN performed better than DQN on Atari games. Such a distributed trail uncovered the potential of distributed RL.

![Deep Q-learning Networks](/images/the_evolution_of_drl/dqn.png){:width="80%" style="display: block; margin: 0 auto"}

### Actor and Learner

There are two key roles in Gorilla, namely, actor and learner. The Actor collects data by interacting with multiple environments, and the Learner does parameters update (or policy learning) using collected transitions. Such a mechanism has become a consensus in distributed reinforcement learning, differences in future work are all about model sharing and distribution reweighted techniques. This blog will introduce them later.

In Gorilla (as shown below), an Actor coordinates with a remote parameter server to pull parameters periodically, and this process ignores the ongoing _gradient apply_ operation. The learner is responsible for the policy learning; it requests collected data from the replay memory database. As introduced in the paper, the replay buffer could be locally or globally. A local replay buffer stores experience from local actors, which means actors exist in the same machine. Actually, it requires the local machine to have enough memory storage to support that. The global choice is independent of the actor number but with the cost of additional communication overhead. Actually, these two methods have their features, and it is hard to say which one is better. Users can do alternation with their practical conditions.

![Architecture: Gorilla DQN](/images/the_evolution_of_drl/gorilla_architecture.png){:width="80%" style="display: block; margin: 0 auto"}

### Parameter Server

The Parameter Server is not a fresh idea to do parameter management as a broadly used component in various distributed machine learning applications. Like DistBelief, a famous distributed machine learning architecture, the Gorilla also uses a central parameter server to maintain a distributed representation of the neural network. Though some criticism has been brought in some future works, in fact, such a design is feasible and reasonable if you want to deploy your distributed algorithms over a cluster that covers so many machines.

Actually, the advantage of Gorilla DQN is that there are no concerns about the data distribution lag (or policy lag) because it is a greedy off-policy algorithm.

## A3C: Asynchronous Advantages Actor-Critic

Following the pace of Gorilla, DeepMind proposed another async/distributed architecture in 2016: [Asynchronous Methods for Deep Reinforcement Learning](http://proceedings.mlr.press/v48/mniha16.html). As claimed in their paper, the proposed framework aims to solve two main issues: (1) off-policy algorithms require a significant memory usage, like GDQN, (2) to improve the performance of on-policy algorithms like A2C, Sarsa, and $n$-step methods. In reinforcement learning, there is still a solved-required problem, data efficiency. In the era of tabular-based learning, users can solve such a problem easier. However, it is a big problem when researchers want to use reinforcement learning methods to solve other practical tasks. This is a platitudinal question in our research area, so I would not introduce it further here. Readers can get more details with Google search.

**Lightweight design**.
Unlike Gorilla, A3C uses multiple CPU threads on a single machine, but instead of using separate machines and a parameter server. Keeping all things on one machine will largely reduce the communication cost of gradients and parameters.

**Optimization.**
In asynchronous frameworks, do policy gradient apply is not so directly than the sync mode. There is some question we need to handle, especially for the on policy algorithm. One straightforward method could be aggregating gradients from different threads in summation, like Gorilla. But one question is that we need to concern the outdated data problem. In this paper, the authors tested some different aggregation methods, like SGD with momentum, RMSProp without/with shared statistics.

$$
g=\alpha g + (1 - \alpha)\Delta \theta^2 \text{ and } \theta \leftarrow \theta - \eta \frac{\Delta \theta}{\sqrt{g + \epsilon}}.
$$

With an asynchronous execution in multiple environments, agents can collect experiences with higher diversity, which is a very straightforward approach to decorrelates the agents' data into a stationary process. Stand on this point, and we could say that such a data collecting manner can improve not only the on-policy cases but also the off-policy.

**Hybrid GPU/CPU A3C.**
In the next year, Nvidia proposed enhancing A3C, named GA3C (hybrid CPU/GPU implementation of A3C). As reported in their paper ([Reinforcement learning through asynchronous advantage actor-critic on a GPU](https://arxiv.org/abs/1611.06256)), GA3C generates and consumes training data substantially faster than its CPU counterpart. Experiments on 16-core CPU show GA3C achieved higher scores than previously published methods run for the same amount of time on a GPU up to ~6x faster for small DNNs and ~45x for larger DNNs.

![Architecture comparison: A3C and GA3C](/images/the_evolution_of_drl/ga3c.png){:width="80%" style="display: block; margin: 0 auto"}

The above figure shows the comparison of A3C and GA3C architectures. We could find that the latter's biggest difference is that the latter remove model sync operation and replace it with a unique GPU-based DNN model. Trainer, Predictor, and Agent perform more like stateless interfaces in their architecture. Dive into this implementation. We could find that such an implementation is to perform more like an off-policy manner since data collected from different agents have no guarantee in real-time, so we need to use extra techniques (like [important sampling](https://en.wikipedia.org/wiki/Importance_sampling)) to solve this problem, then improve the utilization of sampled data. Some reweighted techniques. However, any reweighted method has its border. Important sampling will bring big variance when it meets big distribution (policy) differences, and such an issue will result in poor and non-stationary performance.

**Performance mertrics & Trade-offs.**
Another problem in this architecture is the trade-off between these three types of processes. The authors found that the number of agents $N_A$ should at least match the available CPU cores, with two predictors and two trainers $N_P = N_T = 2$. Therefore, the authors propose an annealing process to configure the system dynamically. Every minute, the dynamic searching module randomly changes $N_P$, $N_T$, or $N_A$ by ±1, monitoring alterations in TPS to accept or reject the new setting. The optimal configuration is then automatically identified in a reasonable time for different environments or systems.

![Dynamic adjustment](/images/the_evolution_of_drl/ga3c_dynamic_adjustment.png){:width="90%" style="display: block; margin: 0 auto"}

## IMPALA & SEED RL

[todo]


## Sample Factory: An Architecture for High-throughput RL on Single Machine

Different from previous work, Sample Factory focuses on the computational efficiency of a single machine. To improve the efficiency of a computing cluster, the single node's computational efficiency could also be critical, especially for those tasks which have no tremendous communication across multiple computing nodes. Stand on this view, Sample Factory gives its solution, in one sentence, focused on making all key computations fully asynchronous and minimizing the latency and the cost of communication between components, taking full advantage of fast local messaging. Here shows the architecture of Sample Factory.

![Architecture: Sample Factory](/images/the_evolution_of_drl/sample_factory.png){:width="90%" style="display: block; margin: 0 auto"}

**Vector Environments.**
Each rollout worker maintains multiple environments which work in series, easily to make them run in parallel with multi-core CPUs. The most important is to reduce the idle time in sampling to improve the sample efficiency. To meet this requirement, the authors proposed two strategies: (1) multiple policy workers to reduce the waiting time of action outputs from policy workers to rollout workers, (2) and for the rollout worker, use buffered environments do sampling to utilize the waiting time (environment stepping and communication stage of policy worker and rollout worker). Another problem is the communication cost between components. We could further reduce the communication cost with shared memory and send only the indices of these tensors through FIFO queues.

## Conclusion

Many algorithms/frameworks on distributed reinforcement learning were published in recent years to handle big practical tasks. Most of them claimed that they bring new ideas on resources management. However, I don't think it is a very critical problem to be solved. In my opinion, the key is how to resolve the policy lag, reuse outdated data, and async parameter update.

## References

1. Espeholt, Lasse, et al. "Impala: Scalable distributed deep-rl with importance weighted actor-learner architectures." International Conference on Machine Learning. PMLR, 2018.
2. Mnih, Volodymyr, et al. "Asynchronous methods for deep reinforcement learning." International conference on machine learning. PMLR, 2016.
3. Nair, Arun, et al. "Massively parallel methods for deep reinforcement learning." arXiv preprint arXiv:1507.04296 (2015).
4. Babaeizadeh, Mohammad, et al. "Reinforcement learning through asynchronous advantage actor-critic on a gpu." arXiv preprint arXiv:1611.06256 (2016).
5. Petrenko, Aleksei, et al. "Sample Factory: Egocentric 3D Control from Pixels at 100000 FPS with Asynchronous Reinforcement Learning." International Conference on Machine Learning. PMLR, 2020.
6. Espeholt, Lasse, et al. "Seed rl: Scalable and efficient deep-rl with accelerated central inference." arXiv preprint arXiv:1910.06591 (2019).
7. Sun, Peng, et al. "TLeague: A Framework for Competitive Self-Play based Distributed Multi-Agent Reinforcement Learning." arXiv preprint arXiv:2011.12895 (2020).
8. Hoffman, Matt, et al. "Acme: A research framework for distributed reinforcement learning." arXiv preprint arXiv:2006.00979 (2020).
9. Dean, Jeffrey, et al. "Large scale distributed deep networks." (2012).
10. Niu, Feng, et al. "Hogwild!: A lock-free approach to parallelizing stochastic gradient descent." arXiv preprint arXiv:1106.5730 (2011).
11. Zhang, Huan, Cho-Jui Hsieh, and Venkatesh Akella. "Hogwild++: A new mechanism for decentralized asynchronous stochastic gradient descent." 2016 IEEE 16th International Conference on Data Mining (ICDM). IEEE, 2016. 
