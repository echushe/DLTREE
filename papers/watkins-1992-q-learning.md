---
id: watkins-1992-q-learning
type: paper
title: "Technical Note: Q-Learning"
authors: ["Christopher J. C. H. Watkins", "Peter Dayan"]
year: 1992
venue: "Machine Learning"
selection: "value-learning-milestone"
---

# Technical Note: Q-Learning

[Publisher record](https://doi.org/10.1023/A:1022676722315) · [Author-hosted paper](https://www.gatsby.ucl.ac.uk/~dayan/papers/cjch.pdf)

## Why this paper is in the graph

A foundational convergence treatment of model-free action-value learning. It connects Markov models, Bellman recursion, and learning from experience.

## Contribution and limits

The paper formalizes convergence for tabular Q-learning under its sampling and learning-rate conditions. The method predates this article in Watkins's 1989 work.

The theorem is not a general convergence guarantee for neural-network Q-functions, arbitrary exploration, or fixed-rate updates. This paper is an application anchor for the older Markov foundations, not their origin.

## Reading route

Read the problem definition and update rule first, then identify the proof's assumptions. Compare a nonterminal target with a terminal target using the concept node's arithmetic.

## Graph connections

- **explains:** [Q-learning](../concepts/q-learning.md)
- **uses:** [Bellman equations](../concepts/bellman-equations.md), [MDP](../concepts/markov-decision-process.md), [Markov property](../concepts/markov-property.md)
- **related_to:** [Markov chain](../concepts/markov-chain.md)
