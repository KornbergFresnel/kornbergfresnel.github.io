---
title: "Signal Instructed Coordination in Team Competition"
collection: publications
permalink: /publication/2019-09-10-Signal-Instructed-Coordination-in-Team-Competition
date: 2019-09-10
venue: 'Sep 10th'
author: 'Liheng Chen, Hongyi Guo, Haifeng Zhang, Fei Fang, Yaoming Zhu, **Ming Zhou**, Weinan Zhang, Qing Wang, Yong Yu'
publish: 'arXiv preprint arXiv:1909.04224'
---

### Abstract

In many real-world problems, a team of agents need to collaborate to maximize the common reward. Although existing works formulate this problem into a centralized learning with decentralized execution framework, which avoids the non-stationary problem in training, their decentralized execution paradigm limits the agents’ capability to coordinate. Inspired by the concept of correlated equilibrium, we propose to introduce a coordination signal to address this limitation, and theoretically show that following mild conditions, decentralized agents with the coordination signal can coordinate their individual policies as manipulated by a centralized controller. The idea of introducing coordination signal is to encapsulate coordinated strategies into the signals, and use the signals to instruct the collaboration in decentralized execution. To encourage agents to learn to exploit the coordination signal, we propose Signal Instructed Coordination (SIC), a novel coordination module that can be integrated with most existing MARL frameworks. SIC casts a common signal sampled from a pre-defined distribution to all agents, and introduces an information-theoretic regularization to facilitate the consistency between the observed signal and agents' policies. Our experiments show that SIC consistently improves performance over well-recognized MARL models in both matrix games and a predator-prey game with high-dimensional strategy space.


### Download Paper (PDF)

-[PAPER](https://arxiv.org/pdf/1909.04224.pdf)
