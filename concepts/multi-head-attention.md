---
id: multi-head-attention
type: concept
title: "Multi-Head Attention"
aliases: ["MHA", "Attention heads"]
domains: ["nlp", "computer-vision", "time-series", "generative-ai"]
---

# Multi-Head Attention

## What it is and why it matters

Multi-head attention runs several attention operations using separate learned query, key, and value projections, then mixes their outputs. Heads can represent different compatibility and value transformations instead of sharing one weighted combination.

This creates capacity for different relationships, but does not guarantee that each head learns a distinct or easily named linguistic role.

## Mechanism

For $H$ heads:

$$
\mathrm{head}_i=\operatorname{Attention}(QW_i^Q,KW_i^K,VW_i^V),
$$
$$
\operatorname{MHA}(Q,K,V)=\operatorname{Concat}(\mathrm{head}_1,\ldots,\mathrm{head}_H)W^O.
$$

In a common self-attention configuration with model width $D$, each head has width $d_k=d_v=D/H$. Input $X:[B,L,D]$ becomes projected tensors $[B,H,L,D/H]$. Scores are $[B,H,L,L]$. Concatenated outputs return to $[B,L,D]$ before the output projection.

The four dense projections together have about $4D^2$ weights, ignoring biases. Increasing head count at fixed total width does not multiply that projection parameter count by the number of heads.

## Worked example

With $B=2$, $L=3$, $D=8$, and $H=2$, each head uses width $4$. Query and value tensors have shape $[2,2,3,4]$ and attention weights have shape $[2,2,3,3]$.

If the two heads output $[1,2]$ and $[3,4]$ for one position in a smaller width-four example, concatenation yields $[1,2,3,4]$. A learned output matrix can combine coordinates across heads.

## Engineering implications

- Ensure total width is divisible by head count in implementations that require equal-width heads.
- Increasing heads at fixed width reduces the dimensions available to each head. More heads is not an automatic quality improvement.
- Keep masks broadcastable across batch and head axes and consistent with the permitted query-key relationships.
- Multi-head attention is not an ensemble of independently trained models; heads are trained jointly and mixed.
- Head pruning is a structured compression option, but requires evaluation and shape-aware changes to projections.

## Graph connections

- **requires:** [Scaled dot-product attention](scaled-dot-product-attention.md)
- **used_by:** [Transformer](transformer.md)
- **related_to:** [Embeddings](embeddings.md), [Neural-network pruning](neural-network-pruning.md)
- **introduced_in:** [Attention Is All You Need](../papers/vaswani-2017-attention.md) — the multi-head construction used here.
