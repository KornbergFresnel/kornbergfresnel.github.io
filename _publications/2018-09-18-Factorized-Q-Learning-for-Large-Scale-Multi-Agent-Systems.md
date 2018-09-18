---
title: "Factorized Q-Learning for Large-Scale Multi-Agent Systems"
collection: publications
permalink: /publication/2018-09-18-Factorized-Q-Learning-for-Large-Scale-Multi-Agent-Systems
date: 2018-09-18
venue: 'Sep 18th'
author: 'Y Chen, **M Zhou**, Y Wen, Y Yang, Y Su, W Zhang, D Zhang, J Wang, H Liu'
publish: 'arXiv preprint arXiv:1809.03738'
---

### Abstract

Deep Q-learning has achieved a significant success in single-agent decision making tasks. However, it is challenging to extend Q-learning to large-scale multi-agent scenarios, due to the explosion of action space resulting from the complex dynamics between the environment and the agents. In this paper, we propose to make the computation of multi-agent Q-learning tractable by treating the Q-function (wrt state and joint-action) as a high-order high-dimensional tensor and then approximate it with factorized pairwise interactions. Furthermore, we utilize a composite deep neural network architecture for computing the factorized Q-function, share the model parameters among all the agents within the same group, and estimate the agents' optimal joint actions through a coordinate descent type algorithm. All these simplifications greatly reduce the model complexity and accelerate the learning process. Extensive experiments on two different multi-agent problems have demonstrated the performance gain of our proposed approach in comparison with strong baselines, particularly when there are a large number of agents.

### Download Paper (PDF)

-[PAPER](https://arxiv.org/pdf/1809.03738.pdf)
