---
id: ba-2016-layer-normalization
type: paper
title: "Layer Normalization"
authors: ["Jimmy Lei Ba", "Jamie Ryan Kiros", "Geoffrey E. Hinton"]
year: 2016
venue: "arXiv:1607.06450"
selection: "normalization-root"
---

# Layer Normalization

[Paper and version history](https://arxiv.org/abs/1607.06450)

## Why this paper is in the graph

The root of a normalization approach based on individual examples rather than batch composition. It forms a bridge from recurrent networks to Transformers.

## Contribution and limits

The paper computes normalization statistics across a layer's features for a single training case, with learned gains and biases. This avoids the usual batch-statistics dependence and applies naturally within recurrent processing.

A modern tensor library may permit several normalized axes. Those settings need to be specified explicitly; the method's name alone does not define a tensor operation.

## Reading route

Compare the statistics group with batch normalization. Then trace independent normalization of different time steps or tokens. Read the recurrent experiments as the original application context, preceding Transformer use.

## Graph connections

- **explains:** [Layer normalization](../concepts/layer-normalization.md)
- **compares_with:** [Batch normalization](../concepts/batch-normalization.md)
- **related_to:** [RNN](../concepts/recurrent-neural-network.md), [Transformer](../concepts/transformer.md)
