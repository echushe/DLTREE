---
id: transformer
type: concept
title: "Transformer"
aliases: ["Transformer architecture", "Attention-based sequence model"]
domains: ["nlp", "generative-ai", "computer-vision", "time-series"]
---

# Transformer

## What it is and why it matters

A Transformer builds representations using attention and position-wise feedforward blocks, joined by residual connections and normalization. It provides a common architecture foundation for language, image-patch, and time-series models.

The original 2017 model is an encoder-decoder for sequence transduction. Encoder-only and decoder-only systems are important descendants; "Transformer" does not specify one training objective or one attention mask.

## Mechanism

Start with embeddings plus positional information, giving $X:[B,L,D]$. An original-style, post-normalized encoder block has:

$$
U=\operatorname{LN}(X+\operatorname{MHA}(X,X,X)),
$$
$$
Y=\operatorname{LN}(U+\operatorname{FFN}(U)).
$$

Dropout is omitted here for clarity. The feedforward network is an MLP applied independently at each position with shared weights, for example $\operatorname{ReLU}(uW_1+b_1)W_2+b_2$. Attention mixes positions; the MLP mixes feature coordinates within each position.

The original decoder adds causal self-attention and cross-attention to encoder outputs. A decoder-only model instead uses causal self-attention without that encoder cross-attention. Pre-normalized blocks reorder layer normalization and are different from the equations above.

## Worked example

For a toy decoder-only next-token task, tokens `we build models` can produce inputs `[BOS, we, build]` and targets `[we, build, models]`.

The first input position attends only to itself; the second to positions one and two; the third to all three. Training computes these positions in parallel with a causal mask. Generation must obtain the next token before using it as a subsequent input.

With $B=2$, $L=3$, $D=8$, and vocabulary size $V=100$, a vocabulary projection maps hidden states $[2,3,8]$ to logits $[2,3,100]$.

## Engineering implications

- Choose architecture, visibility mask, and objective together. Bidirectional encoding and autoregressive generation permit different information.
- Right-shift next-token targets correctly; otherwise the model may learn to copy the answer it can already see.
- Full attention's pairwise work grows quadratically with sequence length; include length in memory and latency estimates.
- Image patches or time-series windows need suitable input representations and evaluation protocols; changing the input modality is more than renaming tokens.
- A language model's next-token objective does not by itself implement retrieval, tool use, or application-level reliability.

## Graph connections

- **requires:** [Multi-head attention](multi-head-attention.md), [Positional encoding](positional-encoding.md), [MLP](multi-layer-perceptron.md), [Residual connections](residual-connections.md), [Layer normalization](layer-normalization.md)
- **uses:** [Embeddings](embeddings.md), [Softmax](softmax.md), [Loss functions](loss-functions.md), [Regularization](regularization.md)
- **compares_with:** [RNN](recurrent-neural-network.md), [CNN](convolutional-neural-network.md)
- **introduced_in:** [Attention Is All You Need](../papers/vaswani-2017-attention.md)
