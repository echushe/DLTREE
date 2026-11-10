---
id: rumelhart-1986-backpropagation
type: paper
title: "Learning representations by back-propagating errors"
authors: ["David E. Rumelhart", "Geoffrey E. Hinton", "Ronald J. Williams"]
year: 1986
venue: "Nature"
selection: "training-milestone"
---

# Learning representations by back-propagating errors

[Publisher record](https://www.nature.com/articles/323533a0) · [Author-hosted paper](https://www.cs.toronto.edu/~hinton/absps/naturebp.pdf)

## Why this paper is in the graph

A milestone in establishing gradient-trained hidden representations as a practical neural-network approach. It anchors several basic concepts without adding a separate paper for every training operation.

## Contribution and limits

The paper presents backward error propagation for adjusting network weights and learning internal features. It is an influential dissemination and demonstration, not the sole invention of the chain rule, reverse-mode differentiation, gradient descent, or multilayer networks.

## Reading route

Read the forward computation and backward weight derivatives together. Reproduce the scalar example in the concept node before studying the representation-learning demonstrations. Distinguish gradient computation from the subsequent weight update.

## Graph connections

- **explains:** [Backpropagation](../concepts/backpropagation.md), [MLP](../concepts/multi-layer-perceptron.md)
- **related_to:** [Activation functions](../concepts/activation-functions.md), [Loss functions](../concepts/loss-functions.md), [Gradient descent](../concepts/gradient-descent.md)
