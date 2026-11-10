---
id: convolutional-neural-network
type: concept
title: "Convolutional Neural Network"
aliases: ["CNN", "ConvNet", "Convolution"]
domains: ["computer-vision", "time-series"]
---

# Convolutional Neural Network

## What it is and why it matters

A CNN applies learned local filters repeatedly across a grid, usually with nonlinear activations between layers. Local connectivity and shared weights make it a natural fit for images and regularly sampled signals.

Unlike a dense layer over a flattened image, a convolution uses the same detector at different locations. Stacked layers expand the receptive field: the region of the input that can influence an output.

## Mechanism

For a one-dimensional, stride-one operation with no padding:

$$
y_{t,o}=b_o+\sum_{c=1}^{C_{\mathrm{in}}}\sum_{j=0}^{K-1}
W_{o,c,j}x_{t+j,c}.
$$

This is cross-correlation, the operation commonly called convolution in neural-network libraries; mathematical convolution reverses the kernel. $K$ is kernel width, and $c,o$ index input and output channels.

For one spatial axis of length $H$, kernel size $K$, padding $p$ on each side, stride $s$, and dilation $\delta$:

$$
H_{\mathrm{out}}=\left\lfloor\frac{H+2p-\delta(K-1)-1}{s}+1\right\rfloor.
$$

For a 2D convolution, apply the same calculation independently to height and width.

## Worked example

Input $[1,2,3,4]$ and cross-correlation kernel $[1,-1]$ produce $[-1,-1,-1]$ with no padding. The filter detects adjacent differences.

A $3\times3$ convolution from $3$ to $16$ channels has $16(3\cdot3\cdot3+1)=448$ parameters including biases, independent of image width and height. A $32\times32$ input becomes $30\times30$ with stride one and no padding.

## Engineering implications

- Record axis order explicitly, for example $[B,C,H,W]$. Channel and spatial axes are easy to confuse.
- Weight sharing encourages translation equivariance, not automatic translation invariance. Padding, stride, and boundaries affect it.
- For forecasting, use causal receptive fields when future observations are unavailable. A centered filter can leak future information.
- Pooling or striding reduces resolution but can discard small or fast-changing details.
- Measure receptive field against the task's spatial or temporal scale.

## Graph connections

- **requires:** [MLP](multi-layer-perceptron.md) — a useful dense-layer comparison.
- **uses:** [Activation functions](activation-functions.md), [Backpropagation](backpropagation.md)
- **uses:** [ReLU](relu.md), [Batch normalization](batch-normalization.md), [Residual connections](residual-connections.md) — common components, not requirements of every CNN.
- **compares_with:** [RNN](recurrent-neural-network.md), [Transformer](transformer.md)
- **supported_by:** [Gradient-Based Learning Applied to Document Recognition](../papers/lecun-1998-document-recognition.md) — a landmark learned-vision system, not the origin of every convolutional architecture.
