---
id: srivastava-2014-dropout
type: paper
title: "Dropout: A Simple Way to Prevent Neural Networks from Overfitting"
authors: ["Nitish Srivastava", "Geoffrey Hinton", "Alex Krizhevsky", "Ilya Sutskever", "Ruslan Salakhutdinov"]
year: 2014
venue: "Journal of Machine Learning Research"
selection: "stochastic-regularization-milestone"
---

# Dropout: A Simple Way to Prevent Neural Networks from Overfitting

[Journal paper and full text](https://jmlr.org/papers/v15/srivastava14a.html)

## Why this paper is in the graph

An enduring stochastic regularization milestone. The journal treatment consolidates an idea already described in earlier work; the graph does not date its first appearance to 2014.

## Contribution and limits

Training randomly removes units and their connections, encouraging useful predictions across many sampled subnetworks. Evaluation uses a deterministic scaling convention rather than explicitly running every possible subnetwork.

The concept node uses inverted dropout, which moves the scaling into training. The ensemble interpretation is an approximation for nonlinear networks, not exact averaging of all their predictions.

## Reading route

Trace one sampled mask and compare training and evaluation computations. Distinguish temporary stochastic removal during training from permanent pruning for deployment.

## Graph connections

- **explains:** [Regularization](../concepts/regularization.md)
- **compares_with:** [Neural-network pruning](../concepts/neural-network-pruning.md)
- **related_to:** [MLP](../concepts/multi-layer-perceptron.md)
