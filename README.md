---
id: dltree
type: hub
title: "DLTREE: Deep Learning and Reinforcement Learning Knowledge Graph"
aliases: ["DLTREE"]
domains: ["foundations", "computer-vision", "time-series", "nlp", "generative-ai", "reinforcement-learning", "model-efficiency"]
---

# DLTREE

A practical knowledge graph of deep learning and reinforcement learning for a software engineer with some AI background. Start with mechanisms, small calculations, and implementation tradeoffs; follow the links into selected research when deeper understanding is useful.

The initial graph contains **25 concept nodes, 14 paper nodes, and this entry node**. It covers the shared foundations first. Task-specific vision, forecasting, language, generative-model, and deep-RL branches will grow around actual needs.

## Paper selection policy

Prefer a small number of papers that establish a lasting idea or open a technology branch. A new paper earns a node when it introduces a useful mechanism, establishes a foundational result, or becomes a durable milestone with broad architectural influence.

- Prioritize branch roots and milestones over publication volume, recency, or benchmark improvements alone.
- Reuse a relevant milestone across concepts. A new concept does not automatically require another paper.
- Normally give a concept one or two research anchors; add more only for a distinct contribution or necessary qualification.
- Prefer publisher, conference, arXiv, and author-hosted sources. Record what a paper contributes and where its evidence stops.
- Distinguish **introduced in**, **popularized by**, **supported by**, and **applied in**. An influential paper is not necessarily the first historical source.
- Do not force an origin claim for broad foundations. Markov-chain nodes use the Q-learning paper as a relevant application anchor, explicitly not as their origin.

Two guiding examples are [Optimal Brain Damage](papers/lecun-1989-optimal-brain-damage.md), opening curvature-aware pruning, and [Attention Is All You Need](papers/vaswani-2017-attention.md), opening the Transformer branch. This seed deliberately avoids a survey of the latest papers.

## The 25 concept nodes

| Group | Nodes |
|---|---|
| Neural-network foundations · 7 | [MLP](concepts/multi-layer-perceptron.md), [Activation functions](concepts/activation-functions.md), [ReLU](concepts/relu.md), [Softmax](concepts/softmax.md), [Loss functions](concepts/loss-functions.md), [Gradient descent](concepts/gradient-descent.md), [Backpropagation](concepts/backpropagation.md) |
| Training stability and efficiency · 5 | [Regularization](concepts/regularization.md), [Residual connections](concepts/residual-connections.md), [Batch normalization](concepts/batch-normalization.md), [Layer normalization](concepts/layer-normalization.md), [Neural-network pruning](concepts/neural-network-pruning.md) |
| Spatial and recurrent architectures · 3 | [CNN](concepts/convolutional-neural-network.md), [RNN](concepts/recurrent-neural-network.md), [LSTM](concepts/long-short-term-memory.md) |
| Representations and attention · 5 | [Embeddings](concepts/embeddings.md), [Scaled dot-product attention](concepts/scaled-dot-product-attention.md), [Multi-head attention](concepts/multi-head-attention.md), [Positional encoding](concepts/positional-encoding.md), [Transformer](concepts/transformer.md) |
| Reinforcement-learning foundations · 5 | [Markov property](concepts/markov-property.md), [Markov chain](concepts/markov-chain.md), [MDP](concepts/markov-decision-process.md), [Bellman equations](concepts/bellman-equations.md), [Q-learning](concepts/q-learning.md) |

## Suggested reading routes

These arrows give reading order, not a claim that each method historically evolved from its neighbor. Follow a node's **requires** links when you need background.

1. **Understand neural-network training:** [Activation functions](concepts/activation-functions.md) → [MLP](concepts/multi-layer-perceptron.md) → [Loss functions](concepts/loss-functions.md) → [Gradient descent](concepts/gradient-descent.md) → [Backpropagation](concepts/backpropagation.md).
2. **Start with vision:** [CNN](concepts/convolutional-neural-network.md) → [ReLU](concepts/relu.md) → [Batch normalization](concepts/batch-normalization.md) → [Residual connections](concepts/residual-connections.md).
3. **Understand sequence state:** [RNN](concepts/recurrent-neural-network.md) → [LSTM](concepts/long-short-term-memory.md), then compare with attention. For forecasting, keep causal inputs and chronological evaluation in view throughout.
4. **Build up to Transformers:** [Embeddings](concepts/embeddings.md) → [Softmax](concepts/softmax.md) → [Scaled dot-product attention](concepts/scaled-dot-product-attention.md) → [Multi-head attention](concepts/multi-head-attention.md) → [Positional encoding](concepts/positional-encoding.md) → [Layer normalization](concepts/layer-normalization.md) → [Transformer](concepts/transformer.md).
5. **Learn sequential decisions:** [Markov property](concepts/markov-property.md) → [Markov chain](concepts/markov-chain.md) → [MDP](concepts/markov-decision-process.md) → [Bellman equations](concepts/bellman-equations.md) → [Q-learning](concepts/q-learning.md).
6. **Explore model efficiency:** [Regularization](concepts/regularization.md) → [Neural-network pruning](concepts/neural-network-pruning.md) → [Optimal Brain Damage](papers/lecun-1989-optimal-brain-damage.md).

## Selected paper nodes

| Year | Paper | Why it is here |
|---|---|---|
| 1954 | [Bellman's dynamic-programming review](papers/bellman-1954-dynamic-programming.md) | Recursive decision optimization |
| 1986 | [Learning representations by back-propagating errors](papers/rumelhart-1986-backpropagation.md) | Training hidden representations |
| 1989 | [Optimal Brain Damage](papers/lecun-1989-optimal-brain-damage.md) | Curvature-aware pruning; conference-year convention |
| 1990 | [Finding Structure in Time](papers/elman-1990-finding-structure-in-time.md) | Recurrent state and learned temporal structure |
| 1992 | [Q-Learning](papers/watkins-1992-q-learning.md) | Tabular action-value convergence |
| 1997 | [Long Short-Term Memory](papers/hochreiter-1997-long-short-term-memory.md) | Gated memory-cell branch |
| 1998 | [Gradient-Based Learning Applied to Document Recognition](papers/lecun-1998-document-recognition.md) | Learned visual recognition systems |
| 2010 | [Rectified Linear Units Improve Restricted Boltzmann Machines](papers/nair-2010-rectified-linear-units.md) | Influential rectifier treatment |
| 2013 | [Efficient Estimation of Word Representations in Vector Space](papers/mikolov-2013-word-representations.md) | Efficient static embeddings |
| 2014 | [Dropout](papers/srivastava-2014-dropout.md) | Stochastic regularization milestone |
| 2015 | [Batch Normalization](papers/ioffe-2015-batch-normalization.md) | Batch-statistics normalization |
| 2016 | [Deep Residual Learning for Image Recognition](papers/he-2016-deep-residual-learning.md) | Residual-learning framework; 2015 preprint |
| 2016 | [Layer Normalization](papers/ba-2016-layer-normalization.md) | Within-example normalization |
| 2017 | [Attention Is All You Need](papers/vaswani-2017-attention.md) | Transformer branch root |

## Graph conventions

- **One Markdown file, one node.** Graph files are this entry node, `concepts/**/*.md`, and `papers/**/*.md`. Keep mathematical prerequisites inside a relevant node until they warrant their own concept.
- **One canonical concept across domains.** Use metadata tags instead of duplicating attention or normalization in several folders.
- **Stable identity.** A node's `id` equals its filename without `.md`; this entry node is the exception. Keep IDs stable when changing display titles.
- **Portable links.** Use ordinary relative inline Markdown links. Every link to a local Markdown node creates a directed edge from the containing node to the target. Untyped links have relation `related_to`.
- **Explicit relationships.** A line such as `- **requires:** [Softmax](softmax.md)` marks every node link on that line with that relation. Repeated identical source/relation/target triples collapse into one exported edge.
- **Research provenance.** External paper and documentation URLs are source attributes, not additional local concept nodes. Paper nodes hold the primary research links; implementation documentation may appear where needed.
- **No dangling placeholders.** Mention future topics as plain text until their files exist. Every concept must reach a paper through concept/paper edges without relying on this index.
- **Cycles are normal in the full graph.** Comparisons and backlinks can be reciprocal. The `requires` subgraph alone must remain acyclic so a learning route does not require itself.

The current relation vocabulary is `requires`, `uses`, `used_by`, `specialization_of`, `specialized_by`, `extends`, `extended_by`, `compares_with`, `related_to`, `introduced_in`, `popularized_by`, `supported_by`, `applied_in`, and `explains`. Relationships describe their source and target as written; inverse links are useful but are not automatically generated.

## Adding a concept

Use this structure, keeping the explanation useful to an engineer. The front matter intentionally uses simple scalar values and JSON-style lists, a portable subset of YAML supported by the checker.

```markdown
---
id: stable-concept-name
type: concept
title: "Readable concept name"
aliases: []
domains: ["foundations"]
---

# Readable concept name

## What it is and why it matters
Explain the purpose and the problem it addresses.

## Mechanism
State essential equations, notation, assumptions, and tensor shapes.

## Worked example
Use a small numerical example that can be checked by hand.

## Engineering implications
Explain useful applications, tradeoffs, and failure modes.

## Graph connections
- **requires:** [Existing concept](existing-concept.md)
- **supported_by:** [Selected milestone](../papers/existing-paper.md)
```

For a paper, include `id`, `type: paper`, `title`, `authors`, `year`, `venue`, and a short `selection` reason in front matter. Its body should contain primary source links, why it belongs, contribution and limits, a reading route, and links to concepts. Record a historical origin only when the evidence supports it.

## Checking and exporting the graph

The dependency-free checker in `tools/check_graph.py` verifies node metadata, relative targets, relationship labels, prerequisite cycles, index reachability, connectivity, and research paths. It can also generate `graph.json` for a future viewer or analysis tool. Markdown remains the source of truth.

```bash
python3 tools/check_graph.py --expected-concepts 25 --export graph.json
```

Omit `--expected-concepts 25` after deliberately growing the seed. The checker validates local structure, not scientific correctness, external website availability, or every possible Markdown extension. It reads the ordinary inline-link convention used here and ignores fenced examples.

## Growth after the seed

Choose the next branch around a concrete question: image recognition, a forecasting problem, language-model adaptation, generative modeling, or an RL environment. Add the smallest useful set of missing concepts and selected milestone papers. Likely later branches include autoencoders/VAEs, GANs, diffusion, deep Q-networks, and policy gradients; they are intentionally not empty nodes in this first batch.
