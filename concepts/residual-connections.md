---
id: residual-connections
type: concept
title: "Residual Connections"
aliases: ["Skip connection", "Residual block", "Shortcut connection"]
domains: ["foundations", "computer-vision", "nlp", "generative-ai"]
---

# Residual Connections

## What they are and why they matter

A residual connection adds a block's input to a learned transformation of that input. The block can learn a correction to an existing representation instead of rebuilding the representation from scratch.

ResNet made residual learning a major architecture branch. Residual routes also join attention and feedforward sublayers inside Transformers. "Skip connection" is a broader family that can include concatenation; this node focuses on additive shortcuts.

## Mechanism

For compatible shapes:

$$
y=x+F(x;\theta),\qquad
\frac{\partial y}{\partial x}=I+J_F(x),
$$

where $I$ is the identity and $J_F$ is the transformation's Jacobian. The identity route gives a direct path for the signal and its gradient. It improves the available paths but does not guarantee stable gradients through an arbitrary full network.

If shapes differ, a projection can form $y=P(x)+F(x)$. The original ResNet includes blocks with an activation after the addition, so the simple derivative above describes the addition before any subsequent activation.

## Worked example

Let $x=[2,-1]$ and $F(x)=[0.1,0.2]$. The residual output is $[2.1,-0.8]$. If the learned branch becomes zero, the additive block returns its input.

For an attention sublayer with shape $[B,L,D]$, both its output and the shortcut must be $[B,L,D]$. A projection is required if the branch changes width.

## Engineering implications

- Check shape alignment; unintended broadcasting can produce a legal but wrong addition.
- Projection shortcuts add parameters and compute and do not preserve a literal identity route.
- Normalization and activation placement matter. Original post-normalized Transformers and pre-normalized variants have different computations.
- Extremely deep residual stacks can still require careful initialization and scaling.
- Removing a branch for compression changes a trained function even though the shortcut remains. Evaluate the result rather than assuming the branch is dispensable.

## Graph connections

- **requires:** [MLP](multi-layer-perceptron.md), [Backpropagation](backpropagation.md)
- **used_by:** [CNN](convolutional-neural-network.md), [Transformer](transformer.md)
- **related_to:** [Batch normalization](batch-normalization.md), [Layer normalization](layer-normalization.md)
- **popularized_by:** [Deep Residual Learning for Image Recognition](../papers/he-2016-deep-residual-learning.md) — a milestone residual-learning framework, not the invention of every shortcut network.
- **applied_in:** [Attention Is All You Need](../papers/vaswani-2017-attention.md)
