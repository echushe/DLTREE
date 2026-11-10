---
id: activation-functions
type: concept
title: "Activation Functions"
aliases: ["Nonlinearity", "Nonlinear activation"]
domains: ["foundations"]
---

# Activation Functions

## What they are and why they matter

An activation function transforms a layer's pre-activation values. Nonlinear activations allow stacked layers to model nonlinear relationships. Their derivatives also influence whether gradients remain useful during training.

Most hidden-layer activations act independently on each scalar. Softmax is different: it couples a vector's components to produce a distribution over alternatives.

## Mechanism

For a pre-activation $z$:

| Function | Definition | Useful interpretation |
|---|---|---|
| Sigmoid | $\sigma(z)=1/(1+e^{-z})$ | A value between zero and one; useful for gates |
| Tanh | $\tanh(z)$ | A bounded, signed hidden value |
| ReLU | $\max(0,z)$ | Pass positive values; suppress negative values |

For sigmoid, $\sigma'(z)=\sigma(z)(1-\sigma(z))$, which is at most $0.25$ and approaches zero in the tails. Repeated multiplication by small derivatives can weaken a gradient. Tanh also saturates; ReLU instead has a flat negative region.

The final output transformation has a different job from a hidden activation: enforce the output's meaning. For example, a probability of one binary event must lie between zero and one, while a temperature prediction need not.

## Worked example

For $z=[-2,0,2]$:

- ReLU gives $[0,0,2]$.
- Sigmoid gives approximately $[0.119,0.5,0.881]$.
- Tanh gives approximately $[-0.964,0,0.964]$.

Three sigmoid outputs are three independent scores; they need not sum to one. Use that interpretation for multiple labels that may occur together. Mutually exclusive categories call for a joint categorical distribution instead.

## Engineering implications

- Inspect activation and gradient distributions when a model stops learning.
- A bounded activation can be appropriate for a gate even when it would impede gradient flow in a deep hidden stack.
- Do not add sigmoid or softmax before a loss that already incorporates it in a numerically stable computation.
- Activation choice interacts with initialization, normalization, and learning rate. It is not an isolated switch.

## Graph connections

- **specialized_by:** [ReLU](relu.md), [Softmax](softmax.md)
- **used_by:** [MLP](multi-layer-perceptron.md), [RNN](recurrent-neural-network.md), [LSTM](long-short-term-memory.md)
- **related_to:** [Backpropagation](backpropagation.md), [Loss functions](loss-functions.md)
- **supported_by:** [Backpropagation](../papers/rumelhart-1986-backpropagation.md) — differentiable hidden units in a foundational training treatment.
- **supported_by:** [Rectified Linear Units Improve Restricted Boltzmann Machines](../papers/nair-2010-rectified-linear-units.md) — an influential rectifier milestone, not the origin of every activation function.
