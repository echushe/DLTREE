---
id: neural-network-pruning
type: concept
title: "Neural-Network Pruning"
aliases: ["Network pruning", "Weight pruning", "Model pruning"]
domains: ["foundations", "model-efficiency", "computer-vision", "generative-ai"]
---

# Neural-Network Pruning

## What it is and why it matters

Pruning removes weights or larger structures from a network while trying to preserve useful predictions. It opens a model-efficiency branch connecting training objectives, parameter importance, sparsity, storage, and hardware execution.

Unstructured pruning removes individual connections. Structured pruning removes units, channels, heads, or blocks. These choices produce different runtime opportunities even at similar parameter counts.

## Mechanism: Optimal Brain Damage

Approximate the loss around a trained parameter vector $w$:

$$
\Delta L\approx g^T\Delta w+\frac12\Delta w^TH\Delta w,
$$

where $g$ is the gradient and $H$ is the Hessian of second derivatives. Near a stationary point, neglect the first term. Under a diagonal-Hessian approximation, deleting parameter $w_i$ means $\Delta w_i=-w_i$ and gives saliency:

$$
s_i\approx\frac12 H_{ii}w_i^2.
$$

Small estimated saliency suggests a lower-cost deletion. Re-estimating importance and retraining after pruning can matter because the approximation is local and ignores parameter interactions.

## Worked example

Consider two weights near a local minimum:

| Weight | Value | Diagonal curvature | Estimated deletion cost |
|---|---:|---:|---:|
| A | $0.1$ | $100$ | $0.5$ |
| B | $0.5$ | $1$ | $0.125$ |

Magnitude pruning would remove A first. The curvature estimate prefers B. These numbers illustrate the approximation; actual loss changes need measurement.

## Engineering implications

- A dense tensor containing many zeros usually retains its original storage layout and dense compute cost.
- To obtain speedups, use a sparse format and compatible kernels, or physically reduce structured dimensions.
- Measure latency, memory, and task quality on the intended hardware. Fewer parameters alone do not establish faster inference.
- Track the full cost of importance estimation and recovery training as well as inference savings.
- OBD's stationary-point and diagonal-curvature assumptions can fail. Its name does not imply globally optimal pruning.

## Graph connections

- **requires:** [MLP](multi-layer-perceptron.md), [Loss functions](loss-functions.md)
- **uses:** [Backpropagation](backpropagation.md), [Gradient descent](gradient-descent.md) — for training and recovery; curvature requires additional computation.
- **compares_with:** [Regularization](regularization.md)
- **related_to:** [CNN](convolutional-neural-network.md), [Multi-head attention](multi-head-attention.md)
- **supported_by:** [Optimal Brain Damage](../papers/lecun-1989-optimal-brain-damage.md) — a root milestone for curvature-based connection pruning, not the first conceivable pruning method.
