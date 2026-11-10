---
id: lecun-1998-document-recognition
type: paper
title: "Gradient-Based Learning Applied to Document Recognition"
authors: ["Yann LeCun", "Léon Bottou", "Yoshua Bengio", "Patrick Haffner"]
year: 1998
venue: "Proceedings of the IEEE"
selection: "learned-vision-milestone"
---

# Gradient-Based Learning Applied to Document Recognition

[Author's publication record and full text](https://bottou.org/papers/lecun-98h)

## Why this paper is in the graph

A landmark demonstration of learned visual features and gradient-based document-recognition systems, including LeNet-5. It gives the vision branch an engineering application anchor.

## Contribution and limits

The paper connects convolutional architectures with practical recognition pipelines. It is a mature milestone rather than the first use of local receptive fields or shared weights.

Its historical architecture should not be read as a prescription for current production settings. The term "graph transformer network" in this work describes a different system from the attention-based Transformer introduced in 2017.

## Reading route

Start with the convolutional architecture and follow feature-map sizes and shared parameters. Then inspect how learned components fit into a larger recognition system.

## Graph connections

- **explains:** [CNN](../concepts/convolutional-neural-network.md)
- **uses:** [Backpropagation](../concepts/backpropagation.md)
- **related_to:** [MLP](../concepts/multi-layer-perceptron.md)
