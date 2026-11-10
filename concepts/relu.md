---
id: relu
type: concept
title: "Rectified Linear Unit"
aliases: ["ReLU", "Rectifier"]
domains: ["foundations", "computer-vision"]
---

# Rectified Linear Unit

## What it is and why it matters

ReLU keeps positive inputs and sets negative inputs to zero. It is a simple hidden-layer nonlinearity with a constant derivative on its positive side. It avoids positive-side saturation of sigmoid and tanh, although it does not eliminate all gradient problems.

Rectifiers form a useful branch point for understanding sparse activations, initialization, and later activation variants.

## Mechanism

$$
\operatorname{ReLU}(z)=\max(0,z), \qquad
\frac{d\operatorname{ReLU}}{dz}=
\begin{cases}0 & z<0\\1 & z>0.\end{cases}
$$

The derivative is undefined exactly at zero; implementations choose a convention, commonly zero. A gradient flowing through an active unit passes unchanged through this local operation. The surrounding weight matrices can still amplify or shrink it.

A unit that stays negative for all relevant inputs receives no gradient through the ReLU path. This is the familiar inactive or "dead ReLU" failure mode.

## Worked example

For $z=[-3,0,2]$, the output is $[0,0,2]$. If the incoming gradient is $[5,5,5]$ and the derivative at zero is taken as zero, the gradient with respect to $z$ is $[0,0,5]$.

This illustrates both the benefit and the cost: active values preserve a gradient, while inactive ones block it.

## Engineering implications

- ReLU is a reasonable starting point for a small MLP or convolutional block; evaluate it in the actual task rather than assuming it is universally best.
- Watch the fraction of units that remain inactive across many batches. Excessively large updates or poorly scaled inputs can contribute to persistent inactivity.
- An unbounded positive output can still produce large activations. Initialization and normalization remain relevant.
- Zero activations do not automatically make dense matrix multiplication faster. Runtime savings require suitable sparse execution.
- Smooth or leaky variants are future expansion nodes when their tradeoffs become relevant.

## Graph connections

- **specialization_of:** [Activation functions](activation-functions.md)
- **used_by:** [MLP](multi-layer-perceptron.md), [CNN](convolutional-neural-network.md)
- **related_to:** [Backpropagation](backpropagation.md), [Batch normalization](batch-normalization.md)
- **popularized_by:** [Rectified Linear Units Improve Restricted Boltzmann Machines](../papers/nair-2010-rectified-linear-units.md) — studies noisy rectifiers in RBMs; it is not a claim that this paper invented the mathematical function or evaluated every feedforward use.
