---
id: recurrent-neural-network
type: concept
title: "Recurrent Neural Network"
aliases: ["RNN", "Simple recurrent network", "Elman network"]
domains: ["time-series", "nlp", "reinforcement-learning"]
---

# Recurrent Neural Network

## What it is and why it matters

An RNN processes a sequence by updating a hidden state at each step. The same parameters are reused across time, letting the state summarize information from earlier inputs.

This provides a compact streaming interface: receive the next observation and the previous state, then return a prediction and a new state. The summary is learned and may lose information.

## Mechanism

Using row-batch vectors:

$$
h_t=\tanh(x_tW_x+h_{t-1}W_h+b),\qquad
z_t=h_tW_o+b_o.
$$

$x_t:[B,d]$, $h_t:[B,h]$, $W_x:[d,h]$, and $W_h:[h,h]$. The recurrence itself has $dh+h^2+h$ parameters. The output projection adds its own parameters.

Training unrolls these repeated operations and backpropagates through time. Long products of recurrent Jacobians can make gradients vanish or explode. Truncating the unroll saves memory but limits temporal credit assignment.

## Worked example

For a scalar recurrence $h_t=\tanh(x_t+0.5h_{t-1})$, start at $h_0=0$ and give inputs $[1,0]$.

Then $h_1=\tanh(1)\approx0.762$ and $h_2=\tanh(0.381)\approx0.363$. The second state remains nonzero even though the second input is zero: the earlier input still influences it.

## Engineering implications

- Reset hidden state between independent examples. Carry it only when successive chunks belong to the same stream.
- Detaching state at a chunk boundary prevents gradients from flowing into earlier chunks; it does not erase the numeric memory.
- Padding needs deliberate handling so that it does not become meaningful history.
- A bidirectional RNN uses future context and is unsuitable for strictly online predictions unless that future is available.
- In a partially observed control task, recurrence can infer useful history without guaranteeing a Markov state.
- Standard recurrence creates a dependency between time steps, limiting parallel processing across those steps.

## Graph connections

- **requires:** [MLP](multi-layer-perceptron.md), [Activation functions](activation-functions.md)
- **uses:** [Backpropagation](backpropagation.md)
- **extended_by:** [LSTM](long-short-term-memory.md)
- **compares_with:** [CNN](convolutional-neural-network.md), [Transformer](transformer.md)
- **related_to:** [Markov property](markov-property.md)
- **supported_by:** [Finding Structure in Time](../papers/elman-1990-finding-structure-in-time.md) — a milestone simple recurrent architecture; recurrent networks have earlier roots.
