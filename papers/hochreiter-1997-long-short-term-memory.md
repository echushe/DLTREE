---
id: hochreiter-1997-long-short-term-memory
type: paper
title: "Long Short-Term Memory"
authors: ["Sepp Hochreiter", "Jürgen Schmidhuber"]
year: 1997
venue: "Neural Computation"
selection: "gated-memory-root"
---

# Long Short-Term Memory

[Publisher record](https://doi.org/10.1162/neco.1997.9.8.1735) · [Author-hosted paper](https://www.bioinf.jku.at/publications/older/2604.pdf)

## Why this paper is in the graph

The root paper for LSTM's gated memory-cell approach to learning long temporal dependencies.

## Contribution and limits

The architecture creates a controlled memory route intended to preserve error signals across time. Gates regulate access to that memory.

The original architecture predates the forget gate used in common later implementations. The concept node explicitly labels its modern equations. Results on studied long-delay tasks do not imply unlimited memory or reliable learning of arbitrary sequence dependencies.

## Reading route

Start with the gradient-decay motivation and the memory-cell construction. Separate the direct memory route from the full recurrent computation. Use the concept node to understand a present-day cell before comparing it with the historical formulation.

## Graph connections

- **explains:** [LSTM](../concepts/long-short-term-memory.md)
- **extends:** [RNN](../concepts/recurrent-neural-network.md)
- **related_to:** [Backpropagation](../concepts/backpropagation.md), [Activation functions](../concepts/activation-functions.md)
