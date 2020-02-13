---
title: "Multi-Agent Reinforcement Learning for Order-dispatching via Order-Vehicle Distribution Matching"
collection: publications
permalink: /publication/2019-11-03-Multi-Agent-Reinforcement-Learning-for-Order-dispatching-via-Order-Vehicle-Distribution-Matching
date: 2019-11-03
venue: 'Nov 3rd'
author: '**Ming Zhou**, Jiarui Jin, Weinan Zhang, Zhiwei Qin, Yan Jiao, Chenxi Wang, Guobin Wu, Yong Yu, Jieping Ye'
publish: 'Proceedings of the 28th ACM International Conference on Information and Knowledge Management'
---

### Abstract

Improving the efficiency of dispatching orders to vehicles is a research hotspot in online ride-hailing systems. Most of the existing solutions for order-dispatching are centralized controlling, which require to consider all possible matches between available orders and vehicles. For large-scale ride-sharing platforms, there are thousands of vehicles and orders to be matched at every second which is of very high computational cost. In this paper, we propose a decentralized execution order-dispatching method based on multi-agent reinforcement learning to address the large-scale order-dispatching problem. Different from the previous cooperative multi-agent reinforcement learning algorithms, in our method, all agents work independently with the guidance from an evaluation of the joint policy since there is no need for communication or explicit cooperation between agents. Furthermore, we use KL-divergence optimization at each time step to speed up the learning process and to balance the vehicles (supply) and orders (demand). Experiments on both the explanatory environment and real-world simulator show that the proposed method outperforms the baselines in terms of accumulated driver income (ADI) and Order Response Rate (ORR) in various trac environments. Besides, with the support of the online platform of Didi Chuxing, we designed a hybrid system to deploy our model.

### Download Paper (PDF)

-[PAPER](https://arxiv.org/pdf/1910.02591.pdf)
