---
id: mikolov-2013-word-representations
type: paper
title: "Efficient Estimation of Word Representations in Vector Space"
authors: ["Tomas Mikolov", "Kai Chen", "Greg Corrado", "Jeffrey Dean"]
year: 2013
venue: "ICLR Workshop; arXiv:1301.3781"
selection: "embedding-milestone"
---

# Efficient Estimation of Word Representations in Vector Space

[Paper and version history](https://arxiv.org/abs/1301.3781)

## Why this paper is in the graph

A milestone in efficient, widely usable static word representations. It anchors the embedding branch without implying that embeddings began in 2013.

## Contribution and limits

The paper presents continuous bag-of-words and skip-gram architectures for predictive word-vector learning. Their simplified computations make large-corpus training practical.

The resulting vectors are static: one lookup vector does not change with each word occurrence's context. Neural language models and distributed representations predate this work. The later word2vec paper's negative-sampling contribution should not be attributed to this first paper.

## Reading route

Compare the direction of prediction in CBOW and skip-gram. Identify which learned matrix supplies the vectors, then distinguish training an embedding from looking one up.

## Graph connections

- **explains:** [Embeddings](../concepts/embeddings.md)
- **uses:** [Gradient descent](../concepts/gradient-descent.md), [Loss functions](../concepts/loss-functions.md)
- **related_to:** [Transformer](../concepts/transformer.md)
