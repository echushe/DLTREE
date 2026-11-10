---
id: markov-decision-process
type: concept
title: "Markov Decision Process"
aliases: ["MDP"]
domains: ["foundations", "reinforcement-learning"]
---

# Markov Decision Process

## What it is and why it matters

An MDP models an agent choosing actions that influence future states and rewards. Unlike one-step supervised prediction, an action can change the data and opportunities the agent encounters later.

This node uses a finite, time-homogeneous, discounted MDP. Other formulations include finite-horizon and average-reward problems, which require different assumptions.

## Mechanism

Specify $(\mathcal S,\mathcal A,P,r,\gamma)$:

- $\mathcal S$: states; $\mathcal A$: available actions, possibly state-dependent.
- $P(s'\mid s,a)$: next-state distribution.
- $r(s,a,s')$: expected immediate reward for a transition.
- $0\le\gamma<1$: discount factor.

A policy $\pi(a\mid s)$ selects actions. Its discounted return from time $t$ is:

$$
G_t=\sum_{k=0}^{\infty}\gamma^kR_{t+k+1}.
$$

The state value is $V^\pi(s)=\mathbb E_\pi[G_t\mid S_t=s]$. Action value $Q^\pi(s,a)$ conditions on taking action $a$ first, then following $\pi$.

For a fixed stationary policy, state transitions form a chain with $P^\pi(s'\mid s)=\sum_a\pi(a\mid s)P(s'\mid s,a)$.

## Worked example

In state Ready, an agent may **finish**, earning $2$ and entering terminal state Done, or **inspect**, paying $0.1$ and returning to Ready. Done has zero future return. Let $\gamma=0.9$.

Finishing immediately returns $2$. Inspecting once and then finishing returns $-0.1+0.9(2)=1.7$. This simple task makes action consequences and reward timing explicit.

## Engineering implications

- Define rewards from the application objective carefully. Optimizing a convenient proxy may produce an unwanted policy.
- A visible observation is not necessarily a Markov state. Hidden demand or machine condition can make a task partially observable.
- Distinguish genuine episode termination from a collection time limit. They can require different bootstrapping treatment.
- Knowing the MDP's transition model permits planning. Learning from sampled transitions without that model is another route.
- Specify reset behavior, action constraints, and reward units before comparing agents.

## Graph connections

- **requires:** [Markov chain](markov-chain.md), [Markov property](markov-property.md)
- **used_by:** [Bellman equations](bellman-equations.md), [Q-learning](q-learning.md)
- **supported_by:** [Bellman's dynamic-programming review](../papers/bellman-1954-dynamic-programming.md) — a root of recursive decision optimization.
- **applied_in:** [Q-Learning](../papers/watkins-1992-q-learning.md) — a model-free learning treatment, not the invention of MDPs.
