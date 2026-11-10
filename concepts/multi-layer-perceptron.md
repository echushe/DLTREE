---
id: multi-layer-perceptron
type: concept
title: "Multi-Layer Perceptron"
aliases: ["MLP", "Dense neural network", "Feedforward neural network"]
domains: ["foundations", "computer-vision", "time-series", "nlp", "generative-ai", "reinforcement-learning"]
---

# Multi-Layer Perceptron

## What it is and why it matters

An MLP maps an input vector to an output through learned affine transformations and nonlinear activation functions. It is a useful baseline for fixed-size features and a reusable component inside larger architectures. The feedforward block inside a Transformer is an MLP applied separately to each token.

One dense layer lets every output feature depend on every input feature. Nonlinear hidden layers let the network express interactions that a single linear transformation cannot.

## Mechanism

For a batch of row vectors:

$$
H = \phi(XW_1+b_1), \qquad Z=HW_2+b_2.
$$

Here $X$ has shape $[B,d]$, $W_1$ is $[d,h]$, $H$ is $[B,h]$, and $W_2$ is $[h,k]$. Bias vectors broadcast across the batch. $\phi$ is a nonlinear activation. $Z$ contains predictions or raw classification scores, depending on the task.

Two affine layers without a nonlinear operation between them collapse into one affine layer. Depth alone does not produce this extra expressive power.

## Worked example

For input $x=[2,-1]$, choose $W_1$ as the $2\times2$ identity, $b_1=0$, and ReLU as the activation. The hidden vector is $[2,0]$. With output weights $[3,-2]^T$ and output bias $1$, the scalar prediction is $7$.

A $10\rightarrow32\rightarrow3$ MLP has $10(32)+32+32(3)+3=451$ learned parameters. This gives a quick check on an implementation's parameter count.

## Engineering implications

- Start with an MLP when each example is naturally a fixed-length feature vector. Compare its validation results with a simple linear baseline.
- Normalize continuous input features using training-set statistics. Feature scales affect optimization.
- Preserve spatial or temporal structure when it matters: flattening an image or a long sequence discards useful architectural assumptions.
- Choose the output and loss together. Multiclass cross-entropy generally consumes logits; scalar regression often uses an unconstrained output.
- Training requires a loss, gradient computation, and an optimizer. The architecture does not specify these by itself.

## Graph connections

- **requires:** [Activation functions](activation-functions.md)
- **uses:** [Loss functions](loss-functions.md), [Backpropagation](backpropagation.md), [Gradient descent](gradient-descent.md)
- **uses:** [Regularization](regularization.md)
- **used_by:** [Transformer](transformer.md)
- **compares_with:** [CNN](convolutional-neural-network.md), [RNN](recurrent-neural-network.md)
- **supported_by:** [Learning representations by back-propagating errors](../papers/rumelhart-1986-backpropagation.md) — a milestone in training hidden representations, not the origin of all multilayer networks.
