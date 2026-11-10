---
id: q-learning
type: concept
title: "Q-Learning"
aliases: ["Tabular Q-learning", "Off-policy TD control"]
domains: ["reinforcement-learning"]
---

# Q-Learning

## What it is and why it matters

Q-learning estimates optimal action values from sampled transitions without needing a transition model. Its tabular form provides a small, inspectable starting point for value-based reinforcement learning and later deep Q-networks.

It is off-policy: the action used to gather experience may differ from the greedy action used in the learning target.

## Mechanism

Given a transition $(s,a,r,s')$:

$$
y=r+\gamma\max_{a'}Q(s',a'),\qquad
Q(s,a)\leftarrow Q(s,a)+\alpha\,[y-Q(s,a)].
$$

$\alpha$ is a learning rate and $y-Q(s,a)$ is a temporal-difference error. For a true terminal transition, use $y=r$ instead. A behavior policy, such as an epsilon-greedy policy, determines which actions are explored.

In a finite discounted MDP with bounded rewards, classical tabular convergence requires sufficient state-action visitation and suitable diminishing learning rates: for each pair, the sum of step sizes diverges while the sum of their squares converges. A fixed learning rate or a neural approximator does not inherit that exact theorem.

## Worked example

Let $Q(s,a)=2$, observed reward $r=1$, next-state maximum $4$, $\gamma=0.9$, and $\alpha=0.1$. The target is $4.6$, so:

$$
Q_{\mathrm{new}}=2+0.1(4.6-2)=2.26.
$$

If the same reward ends the episode, the target is $1$ and the new estimate is $1.9$. Accidentally bootstrapping from a terminal state changes the learning problem.

## Engineering implications

- Start with a small environment where transitions, returns, and an optimal policy can be checked by hand.
- Separate exploration policy, update rule, and evaluation policy in the implementation.
- State discretization can make a continuous problem manageable, but may discard information or produce an enormous table.
- Distinguish termination from time-limit truncation; a truncated continuing task may still need a future-value estimate.
- Replacing the table with an MLP is a major change. Deep Q-learning needs its own stability mechanisms and milestone paper when that branch is added.

## Graph connections

- **requires:** [Bellman equations](bellman-equations.md), [Markov decision process](markov-decision-process.md)
- **related_to:** [MLP](multi-layer-perceptron.md) — a future route to function approximation, not part of the tabular update above.
- **supported_by:** [Q-Learning](../papers/watkins-1992-q-learning.md) — the convergence milestone; the method predates this article in Watkins's 1989 thesis.
