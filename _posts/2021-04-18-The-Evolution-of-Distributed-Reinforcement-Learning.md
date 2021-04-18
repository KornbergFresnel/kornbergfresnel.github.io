---
title: "The Evolution of Distributed Reinforcement Learning"
date: 2021-04-18
permalink: /posts/2021/04/the_evolution_of_distributed_reinforcement_learning/
tags:
  - multi-agent reinforcement learning
  - reinforcement learning
  - distributed machine learning
---
Back in 2015, DeepMind proposed their first distributed reinforcement learning algorithm architecture, known as Gorilla (General Reinforcement Learning Architecture). Before that, works on distributed deep learning focused on massively distributed architectures that can learn from more data in parallel and therefore outperform training on a single machine. But all of them have focused on supervised and unsupervised learning, and there wasn't a distributed architecture or algorithm for (deep) reinforcement learning.

# Gorilla Deep Q-learning Network

As we know, reinforcement learning requires a lot of data to do policy learning, larger than any general supervised learning task. To meet this requirement, DeepMind proposed the first work, deploy DQN on a distributed architecture. GDQN performed better than DQN on atari games. Such a distributed trail uncovered the potential of distributed RL. Reported from the paper, it requires 100 concurrent actors on 31 machines, 100 leaners with the network model.

![Deep Q-learning Networks](/images/the_evolution_of_drl/dqn.png){:width="80%" style="display: block; margin: 0 auto"}

## Actor and Learner

There are two key roles in Gorilla, namely, actor and learner. Actor collects data by interacting with multiple environments, and Learner does parameters update (or policy learning) using collected transitions. Such a mechanism has become a consensus in distributed reinforcement learning, differences in future work are all about model sharing and distribution reweighted techniques. This blog will introduce them in later.

![Architecture: Gorilla DQN](/images/the_evolution_of_drl/gorilla_architecture.png){:width="80%" style="display: block; margin: 0 auto"}

## Stability

Actually, one biggest advantage of Gorilla DQN is that there are no concerns on the data distribution lag (or policy lag), because it is a greedy off-policy algorithm.


# Hybrid CPU/GPU A3C (GA3C)

# IMPALA: Importance Weighted Actor-Learner Architecture

(to be done ...)