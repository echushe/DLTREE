---
id: regularization
type: concept
title: "Regularization"
aliases: ["Regularisation", "Training regularization"]
domains: ["foundations", "computer-vision", "nlp", "time-series"]
---

# Regularization

## What it is and why it matters

Regularization changes training to favor solutions expected to generalize beyond the training examples. It includes objective penalties, stochastic interventions such as dropout, and constraints on learning. It is a family of techniques, not one algorithm.

A model that memorizes training data may fail on new inputs. Regularization can help, but cannot compensate for leakage, a mismatched evaluation split, or a task that changes after deployment.

## Mechanism

An L2-penalized objective is:

$$
J(\theta)=L_{\mathrm{data}}(\theta)+\frac\lambda2\|\theta\|_2^2.
$$

For ordinary SGD this contributes $\lambda\theta$ to the gradient. With adaptive optimizers, an L2 objective penalty and a separately applied weight-decay update generally differ.

For inverted dropout, each activation $h_i$ is independently retained with probability $q$:

$$
\tilde h_i=\frac{m_i}{q}h_i, \qquad m_i\sim\operatorname{Bernoulli}(q).
$$

Then $\mathbb E[\tilde h_i\mid h_i]=h_i$. Training samples masks; evaluation uses the unmasked activations. This preserves the activation expectation, not exact equality of an entire nonlinear network's expected predictions.

## Worked example

For $h=[2,4]$, keep probability $q=0.5$, and sampled mask $[1,0]$, inverted dropout produces $[4,0]$. Another draw might produce $[0,8]$. Averaging all possible mask outcomes recovers $[2,4]$ at this layer.

For a scalar parameter $w=2$ with $\lambda=0.1$, the L2 penalty adds $0.2$ to its gradient under the convention above.

## Engineering implications

- Tune strength using validation data. Too much regularization can cause underfitting.
- Set training and evaluation modes explicitly when using dropout or batch normalization.
- Early stopping chooses a checkpoint using validation behavior; repeatedly tuning against the test set destroys its independence.
- Data augmentation should preserve the target semantics. A time-series transformation that uses future information can invalidate evaluation.
- Pruning may act as capacity control, but its usual engineering goal also includes storage or execution cost.

## Graph connections

- **requires:** [Loss functions](loss-functions.md), [Gradient descent](gradient-descent.md)
- **used_by:** [MLP](multi-layer-perceptron.md), [Transformer](transformer.md)
- **compares_with:** [Neural-network pruning](neural-network-pruning.md)
- **related_to:** [Batch normalization](batch-normalization.md)
- **supported_by:** [Dropout](../papers/srivastava-2014-dropout.md) — a milestone stochastic regularization method, not the origin of regularization as a whole.
