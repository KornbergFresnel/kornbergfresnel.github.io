---
title: "RoboStriker: Hierarchical Decision-Making for Autonomous Humanoid Boxing"
collection: publications
permalink: /publication/2026-02-01-RoboStriker
date: 2026-02-01
author: 'Kangning Yin, Zhe Cao, Wentao Dong, Weishuai Zeng, Tianyi Zhang, Qiang Zhang, Jingbo Wang, Jiangmiao Pang, **Ming Zhou**, Weinan Zhang'
publish: 'arXiv:2601.22517'
---

When we think of humanoid robots, we imagine machines that can walk, balance, and navigate dynamic environments. But what happens when they face *another agent*, with opposing objectives and physical contact — like in boxing?

Most research on humanoid control focuses on imitation, stability, or simple tasks. Competitive physical interaction remains frontier territory: the challenges aren’t just in motion, but in *decision-making under duress*.

In our latest work, **[RoboStriker](https://arxiv.org/abs/2601.22517)**, we present a new approach that lets humanoid robots *learn how to box autonomously* — discovering both strategic decisions and fluid physical execution through self-play and learned motion representation.

<figure style="text-align: center;">
  <img src="https://arxiv.org/html/2601.22517v1/x1.png" alt="Real-world clips">
  <figcaption>Real-world clips of humanoid boxing using RoboStriker, showcasing agile, contact-rich punches and defenses under physical constraints.</figcaption>
</figure>

---

### The Challenge: Where Strategy Meets Physics

Boxing is deceptively complex. At its core, it’s a two-player zero-sum game: maximize your success while minimizing your opponent’s. In simulated environments, game-theoretic methods have proven powerful — yet humanoid bodies introduce hard constraints:

* **Motion instability**: Joint torques are sensitive — a small balance error, and the whole body collapses.
* **Exploration vs physical feasibility**: Aggressive exploration needed for strategy often leads to catastrophic physical failure when applied directly in the action space.
* **Non-stationary learning dynamics**: When both agents learn simultaneously, small changes in opponent behavior create large variance in physical outcomes, destabilizing training.

Traditional self-play in joint action spaces either fails to learn high-level tactics or collapses due to unstable physics.

---

### The Insight: Separate *Strategy* from *Execution*

The key idea behind RoboStriker is elegantly simple:

> Instead of learning in raw motor space, we lift strategic decisions into a *bounded latent motion space* — a learned representation where each point corresponds to a physically plausible movement.

This allows the system to:

* **Capture rich behavioral primitives** — e.g., punches, slips, steps — in a compact form.
* **Separate high-level strategy from low-level control**.
* **Enable stable exploration** during competitive learning.

By isolating the *what to do* (strategy) from *how to do it* (execution), we unlock both tactical emergence and robust physics.



<figure style="text-align: center;">
  <img src="https://arxiv.org/html/2601.22517v1/x2.png" alt="Overview of RoboStriker">
  <figcaption><b>Overview of RoboStiker.</b> <b>Stage I</b> pretrains a motion tracker to produce physically plausible humanoid behaviors; <b>Stage II</b> compresses these behaviors into a bounded latent space for high-level control; <b>Stage III(a)</b> runs warm-up training on top of Stage II, then followed with <b>Stage III(b)</b>, a NFSP over latent-space to solve the humanoid boxing task as a two-player zero-sum game.</figcaption>
</figure>

---

### How It Works

**1. Learn Physical Skills from Human Motion**

First, we train a universal **motion tracker** using human boxing motion capture data. This component produces natural, balanced actions that imitate real human behaviors — from jabs and hooks to defensive slips and footwork.

These skills form the foundation — a library of feasible movements from which higher-level decisions can be made.

**2. Compress Skills into a Latent Space**

Next, we distill this tracker into a **bounded latent action space**. This manifold encodes motion primitives so that each latent vector corresponds to a valid physical action.

By constraining the space (e.g., normalization on a sphere), we ensure exploration remains bounded — latent actions never decode into catastrophic or unnatural motions.

**3. Competitive Learning via Self-Play in Latent Space**

Finally, we perform self-play training using a variant of Neural Fictitious Self-Play (NFSP), but crucially:

> Agents *choose latent motion vectors*, not raw torques.

This means strategies evolve in a compact, stable space, while the low-level controller ensures every latent choice maps to robust physical behavior.

During early training, agents are warmed up against heuristic opponents to stabilize learning, and adversarial motion priors encourage diversity and realism.

---

### What Emerges

From this setup, humanoid agents autonomously discover:

* **Effective distance control** and engagement strategies.
* **Combination striking** patterns that adapt to opponent behavior.
* **Defensive maneuvering** — slips, guards, and repositioning.
* **Balance-preserving tactics** even under competitive pressure.

Importantly, these behaviors emerge *without explicit reward engineering* for each skill or tactic. They arise from the interaction of learned motion representations and competitive self-improvement.

---

### Why This Matters

RoboStriker marks a step forward in embodied multi-agent learning:

* It **bridges strategy and physics** by recognizing that high-level tactical reasoning need not be entangled with fragile low-level control.
* It provides a **generalizable paradigm** for other competitive or cooperative physical tasks — from robot sports to collaborative manipulation between agents.
* It demonstrates that **self-play can succeed in physically realistic humanoid environments**, not just abstract action games.

By structuring the learning problem this way, robots can now *reason about physical competition* in ways that resemble human tactical thought while grounded in real motor feasibility.

---

### Looking Ahead

Robotic competition has long been a benchmark for general intelligence — requiring perception, decision-making, and embodied execution. RoboStriker opens the door to future research in:

* Multi-robot team sports
* Human-robot interactive play
* Real-world transfer of embodied strategy learning

For details and technical insights, see the full paper: [RoboStriker — *Hierarchical Decision-Making for Autonomous Humanoid Boxing*](https://arxiv.org/abs/2601.22517).

---


### Cite

```bibtex
@misc{yin2026robostrikerhierarchicaldecisionmakingautonomous,
      title={RoboStriker: Hierarchical Decision-Making for Autonomous Humanoid Boxing}, 
      author={Kangning Yin and Zhe Cao and Wentao Dong and Weishuai Zeng and Tianyi Zhang and Qiang Zhang and Jingbo Wang and Jiangmiao Pang and Ming Zhou and Weinan Zhang},
      year={2026},
      eprint={2601.22517},
      archivePrefix={arXiv},
      primaryClass={cs.RO},
      url={https://arxiv.org/abs/2601.22517}, 
}
```