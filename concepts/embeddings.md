---
id: embeddings
type: concept
title: "Embeddings"
aliases: ["Embedding layer", "Learned vector representation", "Word embeddings"]
domains: ["foundations", "nlp", "generative-ai", "recommendation"]
---

# Embeddings

## What they are and why they matter

An embedding represents an item as a vector. A learned lookup table maps discrete IDs, such as tokens, products, or categories, to trainable vectors. More broadly, an encoder can embed an entire input into a vector space.

Vectors make it possible to learn similarities and interactions without treating an arbitrary integer ID as a meaningful numeric magnitude.

## Mechanism

For vocabulary size $V$ and width $d$, an embedding table is $E\in\mathbb R^{V\times d}$. Item $i$ maps to row $E_{i,:}$. This equals multiplying its one-hot row vector by $E$, but a lookup avoids constructing that vector.

For token IDs of shape $[B,L]$, the output is $[B,L,d]$. Training updates rows through the surrounding objective; embeddings do not acquire useful semantics simply by being initialized.

Word2vec's CBOW and skip-gram are landmark predictive ways to learn static word vectors. A contextual representation, such as a Transformer's hidden output, additionally depends on surrounding input. The lookup vector for a token and its contextual hidden representation are different objects.

## Worked example

Let the vocabulary be `cat=0`, `dog=1`, `car=2`, and:

$$
E=\begin{bmatrix}1&0\\0.8&0.2\\0&1\end{bmatrix}.
$$

IDs $[1,0]$ produce vectors $[[0.8,0.2],[1,0]]$. These invented values make dog and cat closer than dog and car under Euclidean distance. A different objective could learn a different geometry.

A table with $10{,}000$ items and width $128$ has $1{,}280{,}000$ learned values, which can dominate a small model's parameter budget.

## Engineering implications

- Version the vocabulary and ID mapping with the weights. An ID mismatch silently changes the model's meaning.
- Plan for unseen items and distinguish padding from ordinary content.
- Similarity depends on the training objective and metric. Do not assume every vector space is suitable for cosine retrieval.
- A lookup table has no sequence-order information by itself.
- Avoid assigning fixed human meanings to individual dimensions without evidence; representations can rotate while preserving useful relationships.

## Graph connections

- **uses:** [Gradient descent](gradient-descent.md), [Loss functions](loss-functions.md)
- **used_by:** [RNN](recurrent-neural-network.md), [Transformer](transformer.md)
- **related_to:** [Positional encoding](positional-encoding.md), [Scaled dot-product attention](scaled-dot-product-attention.md)
- **popularized_by:** [Efficient Estimation of Word Representations in Vector Space](../papers/mikolov-2013-word-representations.md) — efficient static word embeddings, not the invention of learned vector representations.
