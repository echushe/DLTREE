---
id: nair-2010-rectified-linear-units
type: paper
title: "Rectified Linear Units Improve Restricted Boltzmann Machines"
authors: ["Vinod Nair", "Geoffrey E. Hinton"]
year: 2010
venue: "ICML"
selection: "activation-milestone"
---

# Rectified Linear Units Improve Restricted Boltzmann Machines

[Conference paper](https://icml.cc/2010/papers/432.pdf)

## Why this paper is in the graph

An influential rectifier milestone connecting activation design with useful learned representations.

## Contribution and limits

The paper develops noisy rectified units in restricted Boltzmann machines and compares their learned features with binary-unit alternatives. This is a specific probabilistic-model setting. The deterministic ReLU in a feedforward network is related but should not be confused with every detail of those stochastic units.

It does not establish the first historical use of rectification or a universal ranking of activation functions.

## Reading route

Start with the motivation for replacing binary units and the rectified-unit approximation. Read the experiments as evidence for the studied setting. Use the concept node for a separate deterministic derivative example.

## Graph connections

- **explains:** [ReLU](../concepts/relu.md)
- **related_to:** [Activation functions](../concepts/activation-functions.md), [MLP](../concepts/multi-layer-perceptron.md)
