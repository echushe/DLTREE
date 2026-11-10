---
id: batch-normalization
type: concept
title: "Batch Normalization"
aliases: ["BatchNorm", "BN"]
domains: ["foundations", "computer-vision"]
---

# Batch Normalization

## What it is and why it matters

Batch normalization normalizes activations using statistics estimated from a collection of training examples, then applies a learned scale and offset. It is a reusable component for training networks, particularly convolutional architectures.

The normalized axes determine the operation. It is not interchangeable with normalizing each feature vector independently.

## Mechanism

For one channel's $m$ values in a training normalization group:

$$
\mu_B=\frac1m\sum_i x_i,\qquad
\sigma_B^2=\frac1m\sum_i(x_i-\mu_B)^2,
$$
$$
y_i=\gamma\frac{x_i-\mu_B}{\sqrt{\sigma_B^2+\epsilon}}+\beta.
$$

$\gamma$ and $\beta$ are learned per-channel parameters; $\epsilon>0$ stabilizes division. For dense features $[B,C]$, statistics are per channel across $B$. For a common 2D CNN layout $[B,C,H,W]$, statistics are per channel across $B,H,W$.

In the usual running-statistics configuration, training also updates estimates of mean and variance. Evaluation uses those stored estimates instead of the current batch. Exact running updates and variance-estimator conventions depend on the implementation.

## Worked example

For one channel with training values $[1,3]$, the mean is $2$ and the variance in the formula above is $1$. With $\gamma=1$, $\beta=0$, and negligible epsilon, outputs are $[-1,1]$.

If evaluation instead uses stored mean $0$ and variance $4$, those same inputs produce approximately $[0.5,1.5]$. This hypothetical mismatch shows why correct training/evaluation state and representative running statistics matter.

## Engineering implications

- Small or strongly correlated normalization groups can produce noisy or unrepresentative statistics. Batch size alone does not describe effective sample diversity.
- A single training example's output can depend on the other examples in its batch.
- In forecasting, normalization over future positions may leak unavailable information. Choose axes consistent with the prediction setting.
- Evaluate with the intended inference mode and consider distribution changes that invalidate stored statistics.
- The original paper's internal-covariate-shift motivation is historical context, not a complete proof of why the method works in every setting.

## Graph connections

- **used_by:** [CNN](convolutional-neural-network.md), [MLP](multi-layer-perceptron.md)
- **compares_with:** [Layer normalization](layer-normalization.md)
- **related_to:** [Gradient descent](gradient-descent.md), [Regularization](regularization.md), [Residual connections](residual-connections.md)
- **introduced_in:** [Batch Normalization](../papers/ioffe-2015-batch-normalization.md)
