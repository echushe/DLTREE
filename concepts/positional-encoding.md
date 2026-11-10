---
id: positional-encoding
type: concept
title: "Positional Encoding"
aliases: ["Position embeddings", "Sinusoidal positional encoding"]
domains: ["nlp", "time-series", "computer-vision", "generative-ai"]
---

# Positional Encoding

## What it is and why it matters

Positional encoding supplies information about where an element occurs in a sequence or grid. Token identity alone cannot distinguish different arrangements of the same items.

Without positional information or position-dependent masks and biases, self-attention is permutation equivariant: reordering the inputs reorders the outputs rather than teaching the network what sequence order means. A causal mask already imposes an ordering constraint, but explicit position representations remain a separate design choice.

## Mechanism

The original Transformer adds position vectors to token embeddings. For even model width $D$:

$$
\operatorname{PE}(p,2i)=\sin\left(p/10000^{2i/D}\right),
$$
$$
\operatorname{PE}(p,2i+1)=\cos\left(p/10000^{2i/D}\right),
\qquad i=0,\ldots,D/2-1.
$$

Position $p$ has a distinct mixture of frequencies. For $L$ tokens, the position table is $[L,D]$ and broadcasts over batch axis $B$ when added to $[B,L,D]$ token representations.

Learned absolute position vectors are another option. Relative position methods and rotations are future branches; they should receive their own nodes and milestone anchors when needed.

## Worked example

For $D=4$, position zero encodes as $[0,1,0,1]$. Position one is approximately $[0.8415,0.5403,0.0100,0.99995]$.

The same token vector receives different position additions in `dog bites man` and `man bites dog`. The model can therefore learn relationships that depend on both content and location.

## Engineering implications

- A formula defined for unseen positions does not guarantee that a trained model extrapolates well to longer sequences.
- A token index is not elapsed time. Irregularly sampled time series may require timestamps or time-gap features.
- During incremental generation, continue position indices rather than restarting each new token at zero.
- Padding and packed sequences need positions aligned with their actual content and masks.
- Image patch grids may need two-dimensional position information; a flattened index is one possible encoding convention, not the only one.

## Graph connections

- **requires:** [Embeddings](embeddings.md)
- **used_by:** [Transformer](transformer.md)
- **related_to:** [Scaled dot-product attention](scaled-dot-product-attention.md), [RNN](recurrent-neural-network.md)
- **supported_by:** [Attention Is All You Need](../papers/vaswani-2017-attention.md) — the sinusoidal construction and learned-position comparison used in this node, not the origin of all position representations.
