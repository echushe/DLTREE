---
id: vaswani-2017-attention
type: paper
title: "Attention Is All You Need"
authors: ["Ashish Vaswani", "Noam Shazeer", "Niki Parmar", "Jakob Uszkoreit", "Llion Jones", "Aidan N. Gomez", "Łukasz Kaiser", "Illia Polosukhin"]
year: 2017
venue: "NIPS"
selection: "transformer-root"
---

# Attention Is All You Need

[Paper and version history](https://arxiv.org/abs/1706.03762)

## Why this paper is in the graph

The Transformer branch root. One paper connects attention, positional information, normalization, residual paths, and feedforward blocks into an enduring architecture.

## Contribution and limits

The original encoder-decoder replaces recurrence with attention-based sequence processing. Scaled dot-product and multi-head attention are central constructions.

Attention itself predates the paper. It also reuses existing normalization and residual ideas. Decoder-only language models are descendants, not the exact architecture evaluated here.

## Reading route

Follow the architecture diagram and trace query, key, value, and residual tensor shapes. Then examine decoder visibility and positional information. Keep architectural contributions separate from task-specific training settings.

## Graph connections

- **explains:** [Transformer](../concepts/transformer.md), [Scaled dot-product attention](../concepts/scaled-dot-product-attention.md), [Multi-head attention](../concepts/multi-head-attention.md), [Positional encoding](../concepts/positional-encoding.md)
- **uses:** [Embeddings](../concepts/embeddings.md), [MLP](../concepts/multi-layer-perceptron.md), [Residual connections](../concepts/residual-connections.md), [Layer normalization](../concepts/layer-normalization.md), [Softmax](../concepts/softmax.md)
