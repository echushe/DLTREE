---
id: long-short-term-memory
type: concept
title: "Long Short-Term Memory"
aliases: ["LSTM", "LSTM cell"]
domains: ["time-series", "nlp", "reinforcement-learning"]
---

# Long Short-Term Memory

## What it is and why it matters

LSTM is a gated recurrent architecture with an explicit cell state. Gates regulate writing, retaining, and exposing information. An additive memory path addresses difficulties in learning dependencies through long chains of ordinary recurrent transformations.

The 1997 paper is the branch root. The common forget-gate formulation below includes a later extension and should not be mistaken for the exact original architecture.

## Mechanism

Let $u_t=[x_t,h_{t-1}]$ concatenate input and previous hidden state. A common modern cell is:

$$
i_t=\sigma(u_tW_i+b_i),\quad f_t=\sigma(u_tW_f+b_f),
$$
$$
o_t=\sigma(u_tW_o+b_o),\quad g_t=\tanh(u_tW_g+b_g),
$$
$$
c_t=f_t\odot c_{t-1}+i_t\odot g_t,\qquad
h_t=o_t\odot\tanh(c_t).
$$

$i,f,o$ are input, forget, and output gates; $g$ is candidate content. $\odot$ denotes elementwise multiplication. For batch size $B$ and hidden width $h$, gates, cell state, and hidden state have shape $[B,h]$.

Holding the gates' other dependencies fixed, the direct derivative along the cell-state route is $f_t$. This is not the full recurrent derivative, and repeated forget factors below one can still decay.

## Worked example

Take scalar $c_{t-1}=2$, $f_t=0.9$, $i_t=0.2$, $g_t=0.5$, and $o_t=0.8$. Then $c_t=1.9$ and $h_t=0.8\tanh(1.9)\approx0.765$.

Most old content is retained, a little new content is added, and the output gate exposes only part of the transformed memory.

## Engineering implications

- Maintain both hidden and cell states; they are different quantities.
- Gating increases parameters and computation relative to a same-width simple RNN.
- Sequence order, padding, state resets, and truncation still need careful handling.
- Longer usable memory is an architectural opportunity, not a guarantee that the model learns every long dependency.
- Check [the official implementation equations](https://docs.pytorch.org/docs/2.15/generated/torch.nn.LSTM.html) when mapping this combined-bias notation to a library's parameter layout.

## Graph connections

- **requires:** [RNN](recurrent-neural-network.md), [Activation functions](activation-functions.md)
- **uses:** [Backpropagation](backpropagation.md)
- **compares_with:** [Transformer](transformer.md)
- **introduced_in:** [Long Short-Term Memory](../papers/hochreiter-1997-long-short-term-memory.md) — the original cell and gated-memory principle, preceding the modern forget-gate form.
