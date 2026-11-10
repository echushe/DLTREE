---
id: bellman-equations
type: concept
title: "Bellman Equations"
aliases: ["Bellman expectation equation", "Bellman optimality equation", "Dynamic programming"]
domains: ["foundations", "reinforcement-learning"]
---

# Bellman Equations

## What they are and why they matter

Bellman equations express long-term value using immediate reward and the value of the next state. This recursive decomposition underlies planning, policy evaluation, and many reinforcement-learning updates.

Policy evaluation asks how good a specified policy is. Optimal control asks which choices yield the greatest expected return. Their equations are related but different.

## Mechanism

For a fixed policy in the finite discounted MDP defined in the prerequisite node:

$$
V^\pi(s)=\sum_a\pi(a\mid s)\sum_{s'}P(s'\mid s,a)
\left[r(s,a,s')+\gamma V^\pi(s')\right].
$$

The optimal action-value equation is:

$$
Q^*(s,a)=\sum_{s'}P(s'\mid s,a)
\left[r(s,a,s')+\gamma\max_{a'}Q^*(s',a')\right].
$$

The expectation averages random outcomes; the maximum selects the best next action. Terminal states contribute zero future value under this convention. For bounded rewards and $\gamma<1$, the corresponding finite-MDP Bellman operators are contractions in the maximum norm, giving unique fixed points.

These are modern discounted-MDP formulations. The historical anchor establishes the recursive optimization branch, not an assertion that every notation above appears verbatim in that paper.

## Worked example

Use Ready and Done from the MDP node. At the optimum:

$$
V^*(\mathrm{Ready})=\max\{2,\;-0.1+0.9V^*(\mathrm{Ready})\}.
$$

Setting $V^*(\mathrm{Ready})=2$ gives alternatives $2$ and $1.7$, confirming the fixed point. A policy that always inspects instead has $V=-0.1+0.9V$, so its value is $-1$.

## Engineering implications

- Keep policy expectation and optimality updates distinct. A maximum changes the question being answered.
- With a known model, compute the expectation explicitly. With samples, estimate it through repeated updates.
- Discounting changes the objective; it is more than a numerical convenience.
- A small Bellman error on sampled data does not by itself establish a good policy under function approximation or distribution shift.
- Contraction guarantees here depend on the stated tabular, discounted setting and do not automatically transfer to neural-network training.

## Graph connections

- **requires:** [Markov decision process](markov-decision-process.md)
- **used_by:** [Q-learning](q-learning.md)
- **supported_by:** [Bellman's dynamic-programming review](../papers/bellman-1954-dynamic-programming.md) — historical foundation.
- **supported_by:** [Q-Learning](../papers/watkins-1992-q-learning.md) — the sampled optimal-action-value learning connection.
