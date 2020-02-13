---
title: "CoRide: Joint Order Dispatching and Fleet Management for Multi-Scale Ride-Hailing Platforms"
collection: publications
permalink: /publication/2019-11-03-CoRide-Joint-Order-Dispatching-and-Fleet-Management-for-Multi-Scale-Ride-Hailing-Platforms
date: 2019-11-03
venue: 'Nov 3rd'
author: 'Jiarui Jin, **Ming Zhou**, Weinan Zhang, Minne Li, Zilong Guo, Zhiwei Qin, Yan Jiao, Xiaocheng Tang, Chenxi Wang, Jun Wang, Guobin Wu, Jieping Ye'
publish: 'Proceedings of the 28th ACM International Conference on Information and Knowledge Management'
---

### Abstract

How to optimally dispatch orders to vehicles and how to trade off between immediate and future returns are fundamental questions for a typical ride-hailing platform. We model ride-hailing as a large-scale parallel ranking problem and study the joint decisionmaking task of order dispatching and fleet management in online ride-hailing platforms. This task brings unique challenges in the following four aspects. First, to facilitate a huge number of vehicles to act and learn efficiently and robustly, we treat each region cell as an agent and build a multi-agent reinforcement learning framework. Second, to coordinate the agents from different regions to achieve long-term benefits, we leverage the geographical hierarchy of the region grids to perform hierarchical reinforcement learning. Third, to deal with the heterogeneous and variant action space for joint order dispatching and fleet management, we design the action as the ranking weight vector to rank and select the specific order or the fleet management destination in a unified formulation. Fourth, to achieve the multi-scale ride-hailing platform, we conduct the decision-making process in a hierarchical way where a multihead attention mechanism is utilized to incorporate the impacts of neighbor agents and capture the key agent in each scale. The whole novel framework is named as CoRide. Extensive experiments based on multiple cities real-world data as well as analytic synthetic data demonstrate that CoRide provides superior performance in terms of platform revenue and user experience in the task of citywide hybrid order dispatching and fleet management over strong baselines.

### Download Paper (PDF)

-[PAPER](https://arxiv.org/pdf/1905.11353.pdf)
