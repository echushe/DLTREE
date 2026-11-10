---
id: backpropagation
type: concept
title: "Backpropagation"
aliases: ["Backprop", "Reverse-mode differentiation in neural networks"]
domains: ["foundations"]
---

# Backpropagation

## What it is and why it matters

Backpropagation efficiently computes derivatives of a scalar loss with respect to a network's parameters by applying the chain rule backward through its computation graph. It makes learning many parameters feasible without separately perturbing each one.

It computes gradients. It does not choose a loss, learning rate, or parameter update rule.

## Mechanism

For $a=f(x)$ and $L=g(a)$:

$$
\frac{\partial L}{\partial x}=\frac{\partial L}{\partial a}\frac{\partial a}{\partial x}.
$$

At an operation with several outgoing paths, gradient contributions add. Shared parameters likewise receive the sum of contributions from every use.

For row-batch affine operation $Z=XW+b$ and upstream gradient $G=\partial L/\partial Z$:

$$
\frac{\partial L}{\partial W}=X^TG,\quad
\frac{\partial L}{\partial X}=GW^T,\quad
\frac{\partial L}{\partial b}=\sum_{n=1}^B G_{n,:}.
$$

With $X:[B,d]$ and $W:[d,h]$, these derivatives have the same shapes as their respective variables. A reverse pass reuses forward values or recomputes them, creating a memory-versus-compute tradeoff.

## Worked example

Let $z=wx$, $h=\operatorname{ReLU}(z)$, and $L=(h-y)^2$. For $x=2$, $w=1$, and $y=3$, the forward values are $z=h=2$ and $L=1$.

The backward values are $\partial L/\partial h=-2$, $\partial h/\partial z=1$, and $\partial z/\partial w=2$. Multiplying gives $\partial L/\partial w=-4$. Gradient descent with rate $0.1$ would then change $w$ to $1.4$.

## Engineering implications

- Check a small smooth computation against finite differences when implementing a custom derivative. Avoid nondifferentiable points in that check.
- Discrete selection, detached tensors, and unsupported operations can break a gradient path.
- Backpropagation through a recurrent network unrolls the computation across time. Truncating that history limits which dependencies receive credit.
- Vanishing or exploding gradients reflect products along paths; residual routes, gating, initialization, and clipping address different aspects of this problem.

## Graph connections

- **requires:** [MLP](multi-layer-perceptron.md), [Loss functions](loss-functions.md)
- **used_by:** [Gradient descent](gradient-descent.md), [RNN](recurrent-neural-network.md), [Neural-network pruning](neural-network-pruning.md)
- **related_to:** [Residual connections](residual-connections.md), [LSTM](long-short-term-memory.md)
- **popularized_by:** [Learning representations by back-propagating errors](../papers/rumelhart-1986-backpropagation.md) — influential dissemination and representation-learning results, not a claim of sole invention.
