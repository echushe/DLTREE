---
id: softmax
type: concept
title: "Softmax"
aliases: ["Normalized exponential"]
domains: ["foundations", "nlp", "generative-ai"]
---

# Softmax

## What it is and why it matters

Softmax converts a vector of real scores, called logits, into positive weights summing to one. It is useful for mutually exclusive classes and for attention weights over candidate positions.

The output expresses a relative distribution. A high softmax value does not by itself establish calibrated confidence or correctness.

## Mechanism

$$
p_i=\frac{\exp(z_i/\tau)}{\sum_j\exp(z_j/\tau)}, \qquad \tau>0.
$$

$z_i$ is the score for alternative $i$; $\tau$ is a temperature. Lower temperatures concentrate mass on the largest scores. Higher temperatures flatten the distribution. The standard definition uses $\tau=1$.

Subtracting the largest logit before exponentiating leaves the mathematical result unchanged and avoids overflow:

$$
p_i=\frac{\exp((z_i-m)/\tau)}{\sum_j\exp((z_j-m)/\tau)}, \qquad m=\max_j z_j.
$$

The derivative couples alternatives: $\partial p_i/\partial z_j=p_i(\delta_{ij}-p_j)$ when $\tau=1$, where $\delta_{ij}$ is one for equal indices and zero otherwise.

## Worked example

Scores $[0,\log 2]$ produce probabilities $[1/3,2/3]$. Adding $1000$ to both scores gives the same answer after stable subtraction.

For a correct second class, cross-entropy is $-\log(2/3)\approx0.405$. In attention, the same weights would blend the second value twice as strongly as the first.

## Engineering implications

- Specify the axis. Classification usually normalizes over classes; attention normalizes over key positions for each query.
- Use stable log-softmax or a fused cross-entropy operation when computing log probabilities.
- Apply attention masks before softmax so forbidden positions receive no mass. A completely masked row needs explicit handling; subtracting infinities can produce undefined values.
- Use independent sigmoid outputs for labels that can coexist.
- Temperature scaling changes probabilities, but positive temperature does not change the highest-scoring category.

## Graph connections

- **specialization_of:** [Activation functions](activation-functions.md)
- **used_by:** [Loss functions](loss-functions.md), [Scaled dot-product attention](scaled-dot-product-attention.md)
- **related_to:** [Transformer](transformer.md)
- **supported_by:** [Attention Is All You Need](../papers/vaswani-2017-attention.md) — a milestone application of softmax in attention, not its historical origin.
