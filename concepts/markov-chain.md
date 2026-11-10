---
id: markov-chain
type: concept
title: "Markov Chain"
aliases: ["Discrete-time Markov chain", "DTMC"]
domains: ["foundations", "time-series", "reinforcement-learning"]
---

# Markov Chain

## What it is and why it matters

A Markov chain describes stochastic transitions between states satisfying the Markov property. This node focuses on finite states and discrete time. It supplies the transition-model foundation for Markov decision processes.

A chain has no agent choosing actions. It describes what happens under a given transition rule. Adding actions, rewards, and a decision objective leads to a different model: an MDP.

## Mechanism

For a time-homogeneous chain, define a row-stochastic transition matrix:

$$
P_{ij}=P(S_{t+1}=j\mid S_t=i),\qquad
P_{ij}\ge0,\qquad\sum_jP_{ij}=1.
$$

With a row-vector state distribution $p_t$, the next distribution is $p_{t+1}=p_tP$, and $p_{t+n}=p_tP^n$.

A stationary distribution $\pi$ satisfies $\pi P=\pi$. For a finite irreducible chain it is unique. Aperiodicity additionally gives convergence toward it from any starting distribution. An arbitrary chain need not converge to one common distribution.

## Worked example

For states Sunny and Rainy, let:

$$
P=\begin{bmatrix}0.8&0.2\\0.4&0.6\end{bmatrix}.
$$

Starting with $p_0=[1,0]$, we get $p_1=[0.8,0.2]$ and $p_2=[0.72,0.28]$. The stationary distribution is $[2/3,1/3]$.

These are distributions across possible trajectories, not a deterministic prediction that a specific day is two-thirds sunny. The weather interpretation is a toy assumption, not an assertion that real weather has this two-state memory.

## Engineering implications

- Fix a row-versus-column convention and verify the matrix sums along the correct axis.
- Estimate transition probabilities from counts only after deciding what constitutes a useful state and sampling interval.
- Check rare or unseen transitions and whether the process changes over time.
- A stationary distribution is not the same as a stationary dataset or a guarantee of convergence.
- A fixed stationary policy in an MDP induces a Markov chain, providing a direct connection to policy evaluation.

## Graph connections

- **requires:** [Markov property](markov-property.md)
- **extended_by:** [Markov decision process](markov-decision-process.md)
- **related_to:** [Bellman equations](bellman-equations.md)
- **applied_in:** [Q-Learning](../papers/watkins-1992-q-learning.md) — its controlled process reduces to a chain under a fixed stationary policy; this is an application anchor, not the historical origin of chains.
