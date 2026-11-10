---
id: ioffe-2015-batch-normalization
type: paper
title: "Batch Normalization: Accelerating Deep Network Training by Reducing Internal Covariate Shift"
authors: ["Sergey Ioffe", "Christian Szegedy"]
year: 2015
venue: "ICML"
selection: "normalization-root"
---

# Batch Normalization: Accelerating Deep Network Training by Reducing Internal Covariate Shift

[Paper and version history](https://arxiv.org/abs/1502.03167)

## Why this paper is in the graph

The batch-normalization root paper: a reusable trainable normalization operation with broad architectural influence.

## Contribution and limits

The method normalizes intermediate values using mini-batch statistics, then learns an affine transformation. Inference uses estimated population statistics in the usual configuration.

The title records the authors' original motivation. It should not be treated as a settled, complete causal explanation for every training benefit. Reported speed and accuracy improvements belong to the paper's experimental settings.

## Reading route

Follow the normalization algorithm and the training-versus-inference distinction. Identify which axes supply statistics in dense and convolutional uses. Compare those axes with layer normalization.

## Graph connections

- **explains:** [Batch normalization](../concepts/batch-normalization.md)
- **related_to:** [Layer normalization](../concepts/layer-normalization.md), [CNN](../concepts/convolutional-neural-network.md), [Gradient descent](../concepts/gradient-descent.md)
