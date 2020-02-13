---
title: "Factorized Q-Learning for Large-Scale Multi-Agent Systems"
collection: publications
permalink: /publication/2018-09-18-Factorized-Q-Learning-for-Large-Scale-Multi-Agent-Systems
date: 2018-09-18
venue: 'Sep 18th'
author: '**Ming Zhou**, Yong Chen, Ying Wen, Yaodong Yang, Yufeng Su, Weinan Zhang, Dell Zhang, Jun Wang'
publish: 'Proceedings of the First International Conference on Distributed Artificial Intelligence'
---

### Abstract

Deep Q-learning has achieved significant success in single-agent decision making tasks. However, it is challenging to extend Q-learning to large-scale multi-agent scenarios, due to the explosion of action space resulting from the complex dynamics between the environment and the agents. In this paper, we propose to make the computation of multi-agent Q-learning tractable by treating the Q-function (w.r.t. state and joint-action) as a high-order high-dimensional tensor and then approximate it with factorized pairwise interactions. Furthermore, we utilize a composite deep neural network architecture for computing the factorized Q-function, share the model parameters among all the agents within the same group, and estimate the agents' optimal joint actions through a coordinate descent type algorithm. All these simplifications greatly reduce the model complexity and accelerate the learning process. Extensive experiments on two different multi-agent problems demonstrate the performance gain of our proposed approach in comparison with strong baselines, particularly when there are a large number of agents.

### Download Paper (PDF)

-[PAPER](https://dl.acm.org/doi/abs/10.1145/3356464.3357707)
