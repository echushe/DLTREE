---
id: elman-1990-finding-structure-in-time
type: paper
title: "Finding Structure in Time"
authors: ["Jeffrey L. Elman"]
year: 1990
venue: "Cognitive Science"
selection: "recurrent-representation-milestone"
---

# Finding Structure in Time

[Publisher record and abstract](https://doi.org/10.1207/s15516709cog1402_1)

## Why this paper is in the graph

A milestone simple recurrent network that makes learned temporal state concrete. It connects sequence prediction with internal representations.

## Contribution and limits

The network feeds hidden representations back into subsequent processing, allowing current representations to depend on earlier inputs. The paper explores sequential tasks and learned structure.

It builds on earlier recurrent proposals, including Jordan's work. It is not the invention of recurrence and does not solve the general long-range credit-assignment problem.

## Reading route

Trace the hidden-state feedback route and compare it with an ordinary feedforward network. Ask what information the state must retain for the next prediction. Then continue to LSTM for explicit gated memory.

## Graph connections

- **explains:** [RNN](../concepts/recurrent-neural-network.md)
- **related_to:** [LSTM](../concepts/long-short-term-memory.md), [Embeddings](../concepts/embeddings.md)
