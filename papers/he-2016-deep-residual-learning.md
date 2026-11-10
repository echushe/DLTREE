---
id: he-2016-deep-residual-learning
type: paper
title: "Deep Residual Learning for Image Recognition"
authors: ["Kaiming He", "Xiangyu Zhang", "Shaoqing Ren", "Jian Sun"]
year: 2016
preprint_year: 2015
venue: "CVPR"
selection: "residual-learning-milestone"
---

# Deep Residual Learning for Image Recognition

[Author-submitted paper](https://arxiv.org/abs/1512.03385)

## Why this paper is in the graph

A milestone residual-learning framework that made substantially deeper visual networks practical to optimize. This node uses the 2016 conference year; the preprint appeared in 2015.

## Contribution and limits

ResNet trains residual transformations around shortcut paths and demonstrates their usefulness in deep image-recognition systems.

The original blocks include details such as normalization, projection shortcuts, and activation placement. An isolated $x+F(x)$ equation is their core pattern, not a complete model specification. Earlier shortcut architectures existed.

## Reading route

Start with the degradation problem and residual block diagrams. Compare identity and projection shortcuts, then trace where activation occurs relative to addition.

## Graph connections

- **explains:** [Residual connections](../concepts/residual-connections.md)
- **uses:** [CNN](../concepts/convolutional-neural-network.md), [Batch normalization](../concepts/batch-normalization.md)
- **related_to:** [Backpropagation](../concepts/backpropagation.md)
