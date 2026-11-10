---
id: lecun-1989-optimal-brain-damage
type: paper
title: "Optimal Brain Damage"
authors: ["Yann LeCun", "John S. Denker", "Sara A. Solla"]
year: 1989
venue: "NIPS 1989; Advances in Neural Information Processing Systems 2"
selection: "curvature-pruning-root"
---

# Optimal Brain Damage

[Conference record](https://proceedings.neurips.cc/paper/1989/hash/6c9882bbac1c7093bd25041881277658-Abstract.html) · [Full paper](https://proceedings.neurips.cc/paper_files/paper/1989/file/6c9882bbac1c7093bd25041881277658-Paper.pdf)

## Why this paper is in the graph

A root milestone for curvature-aware connection pruning. This node uses the proceedings site's conference-year convention, NIPS 1989.

## Contribution and limits

OBD estimates the loss cost of deleting a parameter using diagonal second derivatives, then alternates deletion and further training. Its importance criterion differs from removing the smallest weights.

The estimate assumes a local quadratic approximation, near-stationarity, and neglected cross-parameter curvature. "Optimal" does not mean a globally optimal architecture or guaranteed speedup on any execution system.

## Reading route

Read the Taylor approximation and pruning recipe first. Reproduce the two-weight ranking example in the concept node, then examine how retraining and approximation error affect the experiments.

## Graph connections

- **explains:** [Neural-network pruning](../concepts/neural-network-pruning.md)
- **uses:** [Loss functions](../concepts/loss-functions.md), [Backpropagation](../concepts/backpropagation.md)
- **related_to:** [Regularization](../concepts/regularization.md), [MLP](../concepts/multi-layer-perceptron.md)
