---
author: Ari Gestetner
aliases: 
tags: 
draft: true
img:
desc:
title: Week 1
dateCreated: 07-02-2026
lastModified: 07-02-2026
---

# Week 1

## *Chapter 1: Decisions and Uncertainty*

*   *The Ubiquity of Uncertainty:* Sequential decision-making under uncertainty is a universal challenge across personal, medical, investment, and professional domains [1, 2]. 
*   *The Need for a Unified Framework:* Many specialized fields have developed *fragile* tools that break down when problem characteristics change slightly; this book proposes a *universal formulation* to allow for cross-disciplinary insights [3-5].
*   *The Five Elements of Modeling:* Every sequential decision problem consists of:
    1.  *State Variables ($S_t$):* All information needed to model the system from time $t$ onward, including the physical state $R_t$, information state $I_t$, and the belief or *knowledge state* $B_t$ [6-8].
    2.  *Decision Variables ($x_t$ / $a_t$ / $u_t$):* Controllable variables determined by a policy [9, 10].
    3.  *Exogenous Information ($W_{t+1}$):* New information that arrives after a decision is made, such as random demand or price changes [11, 12].
    4.  *Transition Function ($S_{t+1} = S^M(S_t, x_t, W_{t+1})$):* The equations describing how the system state evolves over time [12, 13].
    5.  *Objective Function:* The metric to be minimized or maximized, often expressed as an expectation: $\max_{\pi} \mathbb{E} \sum_{t=0}^T C(S_t, X^\pi(S_t), W_{t+1})$ [14-16].
*   *The Four Classes of Policies:* All solution strategies for sequential decisions fall into one of these categories:
    1.  *Policy Function Approximations (PFAs):* Analytical functions mapping states directly to actions (e.g., *if $S_t < \theta$, buy*) [17-19].
    2.  *Cost Function Approximations (CFAs):* Policies that optimize a modified objective or constraints to provide a buffer against uncertainty [17-19].
    3.  *Value Function Approximations (VFAs):* Policies based on an estimate of the *value* of being in a future state [17-19].
    4.  *Direct Lookahead (DLA):* Policies that plan explicitly over a future horizon (e.g., decision trees or deterministic forecasts) [17-19].

## *Chapter 2: Canonical Problems and Applications*

*   *Stochastic Search:* A fundamental problem focused on finding a deterministic decision $x$ to maximize an expectation: $\max_x \mathbb{E} F(x, W)$ [20].
*   *Final vs. Cumulative Rewards:* *Final-reward* (offline) formulations care only about the quality of the final design after $N$ experiments, whereas *cumulative-reward* (online) formulations focus on the total reward earned during the learning process [21-23].
*   *Multiarmed Bandit Problem:* A classic online learning challenge that requires balancing *exploration* (trying uncertain options) and *exploitation* (choosing what currently appears best) [24, 25].
*   *Markov Decision Processes (MDPs):* Systems with discrete states and actions where we calculate the value $V(s)$ of being in a state; these often suffer from the *curse of dimensionality* as state space grows exponentially [26-28].
*   *Bellman's Optimality Equation:* The foundational equation for MDPs: $V_t(S_t) = \max_a [r(S_t, a) + \sum P(s'|S_t, a) V_{t+1}(s')]$ [29].

## *Chapter 3: Learning in Stochastic Optimization*

*   *Recursive vs. Batch Learning:* While many fields use *batch* datasets, stochastic optimization relies on *recursive learning* to update estimates as information arrives sequentially [30, 31].
*   *Stochastic Gradient Updates:* The most common adaptive learning method is exponential smoothing: $\bar{\mu}_{n+1} = (1 - \alpha_n)\bar{\mu}_n + \alpha_n W_{n+1},$ where $\alpha_n$ is the *stepsize* [32, 33].
*   *Bayesian Belief Models:* These models start with a *prior distribution* of belief and update it with data, which is highly efficient for expensive observations [34-36].
*   *Correlated Beliefs:* A powerful tool where an observation of one alternative informs our belief about similar alternatives through a covariance matrix $\Sigma$ [37, 38].
*   *Linear Parametric Models:* Functions approximated as a linear combination of *basis functions* or *features*: $V(S|\theta) = \sum_{f \in \mathcal{F}} \theta_f \phi_f(S)$ [39, 40].
*   *Recursive Least Squares (RLS):* An algorithm for updating linear models without requiring expensive matrix inversions at every step [41, 42].
*   *Hierarchical Aggregation:* A method to overcome the curse of dimensionality by estimating functions at different levels of detail simultaneously and weighting them based on the amount of data available [43-45].
*   *Bias-Variance Tradeoff:* A critical consideration in learning that manages errors from oversimplified models (*bias*) versus errors from noisy data (*variance*) [46, 47].
