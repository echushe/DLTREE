---
id: gradient-descent
type: concept
title: "Gradient Descent"
aliases: ["GD"]
domains: ["foundations"]
---

# Gradient Descent

## What it is and why it matters

Gradient descent updates parameters in the direction that locally reduces a differentiable objective. Backpropagation computes the gradient; the optimizer decides how to use it.

Full-batch gradient descent uses all training examples per update. Stochastic and mini-batch variants estimate the gradient from one or several examples, making frequent updates practical on large datasets. They are related variants, not identical update schedules.

## Mechanism

$$
\theta_{t+1}=\theta_t-\eta_t\nabla_\theta L_t(\theta_t).
$$

$\theta$ collects learned parameters, $L_t$ is the objective evaluated for this update, and $\eta_t>0$ is the learning rate. For randomly sampled examples under suitable sampling, the mini-batch gradient estimates the full-data gradient. Its noise depends on batch size and the data.

The local downhill direction is not a guarantee that a finite step reduces loss. Curvature and step size matter, and deep-network objectives need not be convex.

## Worked example

Let $L(w)=(w-3)^2$, so $dL/dw=2(w-3)$. From $w=0$ with learning rate $0.1$:

$$
w_{\mathrm{new}}=0-0.1(-6)=0.6.
$$

The loss falls from $9$ to $5.76$. With learning rate $1.1$, the update is $6.6$ and the loss becomes $12.96$: a downhill direction with too large a step can make things worse.

## Engineering implications

- Treat learning rate as a central training setting. Monitor both training and validation behavior.
- Clear accumulated gradients before an independent update, unless accumulation is intentional.
- Keep the effective loss scale consistent when changing batch size or masking strategy.
- Record optimizer settings, schedules, data order, and seeds for reproducibility.
- Momentum and adaptive optimizers are future nodes; do not interpret every optimizer as this exact update rule.
- Gradient clipping limits an update's input magnitude; it does not repair a wrong objective or missing gradient path.

## Graph connections

- **requires:** [Loss functions](loss-functions.md)
- **uses:** [Backpropagation](backpropagation.md) — for neural-network gradient computation.
- **used_by:** [MLP](multi-layer-perceptron.md), [Embeddings](embeddings.md)
- **related_to:** [Regularization](regularization.md)
- **supported_by:** [Backpropagation](../papers/rumelhart-1986-backpropagation.md) — a milestone neural-network application, not the invention of gradient descent.
