---
id: scaled-dot-product-attention
type: concept
title: "Scaled Dot-Product Attention"
aliases: ["SDPA", "Query-key-value attention"]
domains: ["nlp", "computer-vision", "time-series", "generative-ai"]
---

# Scaled Dot-Product Attention

## What it is and why it matters

Attention lets a query combine information from a collection of values according to its compatibility with their keys. The weights depend on the current input, providing a content-dependent route between positions.

Scaled dot-product attention is one specific attention mechanism. Attention as a broader idea predates the Transformer paper.

## Mechanism

$$
\operatorname{Attention}(Q,K,V)=
\operatorname{softmax}\left(\frac{QK^T}{\sqrt{d_k}}+M\right)V.
$$

Ignoring batch and head axes, $Q:[L_q,d_k]$, $K:[L_k,d_k]$, and $V:[L_k,d_v]$. Scores and weights are $[L_q,L_k]$; the result is $[L_q,d_v]$. Softmax runs over key positions for each query. $M$ is an additive mask: zero for allowed positions and negative infinity for forbidden ones in the mathematical definition.

For independent, zero-mean, unit-variance query and key components, an unscaled dot product has variance $d_k$. Dividing by $\sqrt{d_k}$ controls its scale under those assumptions, helping avoid overly concentrated softmax weights. Learned components need not satisfy them exactly.

Self-attention gets queries, keys, and values from one sequence. Cross-attention gets queries from one source and keys/values from another.

## Worked example

Let $q=[1,0]$, $k_1=[\sqrt2,0]$, $k_2=[0,0]$, $v_1=[10,0]$, and $v_2=[0,20]$.

With $d_k=2$, scaled scores are $[1,0]$, so weights are approximately $[0.731,0.269]$. Their value blend is $[7.31,5.38]$. Masking the second key gives weights $[1,0]$ and output $[10,0]$.

## Engineering implications

- Check transpose axes and mask orientation carefully; shape-valid code can still attend to the wrong positions.
- Apply causal and padding masks before softmax. Handle rows with no allowed keys explicitly.
- Ordinary full self-attention has quadratic pairwise work in sequence length. Materializing all weights also uses quadratic memory; optimized execution can avoid storing that full matrix.
- Attention weights describe a mixing operation, not a complete explanation of model behavior.

## Graph connections

- **requires:** [Softmax](softmax.md)
- **used_by:** [Multi-head attention](multi-head-attention.md), [Transformer](transformer.md)
- **related_to:** [Embeddings](embeddings.md), [Positional encoding](positional-encoding.md)
- **introduced_in:** [Attention Is All You Need](../papers/vaswani-2017-attention.md) — this scaled formulation and its Transformer role, not attention in general.
