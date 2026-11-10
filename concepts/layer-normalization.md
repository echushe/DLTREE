---
id: layer-normalization
type: concept
title: "Layer Normalization"
aliases: ["LayerNorm", "LN"]
domains: ["foundations", "nlp", "time-series", "generative-ai"]
---

# Layer Normalization

## What it is and why it matters

Layer normalization computes statistics within an individual example's feature group, then applies learned scales and offsets. It avoids dependence on other examples in the batch and fits recurrent and Transformer representations naturally.

"Layer" does not mean that every axis in a tensor is necessarily normalized. The configured feature axes define the actual group.

## Mechanism

For a feature vector $x\in\mathbb R^D$:

$$
\mu=\frac1D\sum_jx_j,\qquad
\sigma^2=\frac1D\sum_j(x_j-\mu)^2,
$$
$$
y_j=\gamma_j\frac{x_j-\mu}{\sqrt{\sigma^2+\epsilon}}+\beta_j.
$$

In a typical Transformer tensor $[B,L,D]$, normalization is over $D$ independently for each batch item and token position. The parameters $\gamma,\beta$ have shape $[D]$ and are shared across those items and positions.

The operation uses the same per-example statistics at training and evaluation; it does not require batch running averages. Other parts of the model, such as dropout, can still behave differently between modes.

## Worked example

For $x=[1,3]$, mean $2$, variance $1$, unit scale, zero offset, and negligible epsilon, output is $[-1,1]$.

If another example in the same batch is $[100,104]$, it normalizes independently to approximately $[-1,1]$ using its own mean $102$ and variance $4$. Its presence does not change the first example's result.

## Engineering implications

- Specify normalized axes explicitly. Accidentally including the sequence axis changes the model and can expose future information.
- Very small feature variance makes epsilon and arithmetic precision especially relevant.
- Learned affine parameters mean the final output need not have zero mean or unit variance.
- Batch normalization and layer normalization differ in both axes and inference state; swapping them is an architectural change.
- Placement relative to residual addition matters. For example, $\operatorname{LN}(x+F(x))$ and $x+F(\operatorname{LN}(x))$ are different blocks.

## Graph connections

- **used_by:** [Transformer](transformer.md), [RNN](recurrent-neural-network.md)
- **compares_with:** [Batch normalization](batch-normalization.md)
- **related_to:** [Residual connections](residual-connections.md), [LSTM](long-short-term-memory.md)
- **introduced_in:** [Layer Normalization](../papers/ba-2016-layer-normalization.md)
- **applied_in:** [Attention Is All You Need](../papers/vaswani-2017-attention.md)
