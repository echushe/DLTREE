---
id: markov-property
type: concept
title: "Markov Property"
aliases: ["Markov assumption", "Memoryless property"]
domains: ["foundations", "time-series", "reinforcement-learning"]
---

# Markov Property

## What it is and why it matters

The Markov property says that the current state contains the information from the past needed to predict the next state. It is a statement about a chosen state representation and process, not a claim that the real world has no history.

This is the bridge from modeling sequences to modeling decisions. A reinforcement-learning algorithm can behave poorly when the observation it treats as a state omits important history.

## Mechanism

For states $S_0,\ldots,S_t$:

$$
P(S_{t+1}\mid S_t,S_{t-1},\ldots,S_0)=P(S_{t+1}\mid S_t).
$$

For a controlled process with action $A_t$, the corresponding condition concerns the joint next state and reward:

$$
P(S_{t+1},R_{t+1}\mid \text{history},A_t)
=P(S_{t+1},R_{t+1}\mid S_t,A_t).
$$

Time homogeneity is a separate assumption: it says this conditional transition rule does not change with the time index. A process can be Markov while its transition probabilities vary over time.

## Worked example

Suppose a moving object has position $x_t$ and velocity $v_t$, with $x_{t+1}=x_t+v_t\Delta t$. Position alone does not determine the next position: two objects at the same position can be moving in opposite directions.

If velocity is constant, the state $(x_t,v_t)$ suffices to determine the next state. Adding a relevant variable has made the state Markov for this toy model. With hidden forces, this pair may no longer suffice.

## Engineering implications

- Ask what determines the next outcome: velocity, inventory, outstanding requests, or remaining time may belong in the state.
- A finite-horizon task may require the remaining time as part of the state if you want a time-independent policy and value representation.
- Stacking observations or using an RNN may help infer hidden information. Neither guarantees a sufficient state.
- Avoid confusing the Markov property with independence: neighboring states can be strongly dependent.
- A model's successful fit does not prove that its state representation satisfies the property.

## Graph connections

- **used_by:** [Markov chain](markov-chain.md), [Markov decision process](markov-decision-process.md)
- **related_to:** [RNN](recurrent-neural-network.md), [LSTM](long-short-term-memory.md)
- **applied_in:** [Q-Learning](../papers/watkins-1992-q-learning.md) — a foundational controlled-Markov learning application, not the origin of the Markov property.
